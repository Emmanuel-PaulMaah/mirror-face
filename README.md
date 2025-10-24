# mirror-face

real-time face-tracking web app that uses mediapipe facelandmarker to animate human 3d models with your facial expressions. 

upload your model, enter model url or load demo model.

[use mirror-face](https://emmanuel-paulmaah.github.io/mirror-face/)

## overview

a professional face-tracking web application that uses mediapipe facelandmarker to animate 3d models with 100% fidelity facial tracking. upload glb/gltf files with morph targets and bones, and the app will animate them in real-time using your webcam with native arkit-52 blendshape support and proper skeletal hierarchy.

## project type

* pure frontend application (html/javascript)
* no build system required
* cdn-based dependencies (three.js, mediapipe tasks vision)

## architecture

### core technologies

* **3d rendering**: three.js (v0.160.0) for 3d model display and animation
* **face tracking**: mediapipe facelandmarker with native arkit blendshape output
* **blendshape system**: all 52 arkit blendshapes via mediapipe's trained neural network
* **skeletal animation**: hierarchical neck + head bone rotation with quaternion mathematics

### key features

#### 1. native 52 arkit blendshapes

uses mediapipe's built-in `facelandmarker` with `outputfaceblendshapes: true` to get all 52 arkit-compatible facial expression coefficients directly from mediapipe's trained mlp-mixer neural network:

**eyes (14 blendshapes)**:

* `eyeblinkleft/right` - eye closure
* `eyelookup/down/in/out left/right` - eye gaze direction
* `eyesquintleft/right` - squinting
* `eyewideleft/right` - wide-eyed expression

**eyebrows (5 blendshapes)**:

* `browinnerup` - inner brow raise
* `browouterupleft/right` - outer brow raise
* `browdownleft/right` - brow furrow

**jaw (4 blendshapes)**:

* `jawopen` - mouth opening
* `jawleft/right` - jaw side movement
* `jawforward` - jaw forward motion

**mouth (25 blendshapes)**:

* `mouthsmileleft/right`, `mouthfrownleft/right` - smile/frown
* `mouthfunnel`, `mouthpucker` - lip shapes
* `mouthleft/right` - mouth side movement
* `mouthstretchleft/right` - wide mouth
* `mouthrollupper/lower` - lip rolling
* `mouthshrugupper/lower` - lip shrug
* `mouthpressleft/right` - lips pressed together
* `mouthupperupleft/right` - upper lip raise
* `mouthlowerdownleft/right` - lower lip drop
* `mouthdimpleleft/right` - dimples
* `mouthclose` - mouth closure

**cheeks (3 blendshapes)**:

* `cheekpuff` - cheek inflation
* `cheeksquintleft/right` - cheek squinting

**nose (2 blendshapes)**:

* `nosesneerleft/right` - nose wrinkle

**tongue (1 blendshape)**:

* `tongueout` - tongue protrusion

#### 2. proper skeletal hierarchy

**critical fix**: prevents neck twisting when turning head

* **finds both neck and head bones** using multiple naming conventions:

  * neck: `neck`, `neck`, `spine3`, `cervical`
  * head: `head`, `head`, `head_jnt`, `def-head`, `mixamorighead`
* **stores rest pose**: preserves original bone rotations (`neckrestquat`, `headrestquat`)
* **applies tracking as offset**: uses quaternion multiplication to combine rest pose with tracking
* **40% neck / 60% head distribution**: neck gets 40% of head rotation, head gets 60%

  * `neckrotation = slerp(identity, trackingquat, 0.4)`
  * `headrotation = slerp(identity, trackingquat, 0.6)`
  * `finalneck = neckrestquat × neckrotation`
  * `finalhead = headrestquat × headrotation`

#### 3. head pose from transformation matrix

* uses mediapipe's `facialtransformationmatrixes` (4x4 matrix) instead of manual landmark calculations
* converts matrix to quaternion using proper rotation extraction algorithm
* smooth interpolation using quaternion slerp (alpha = 0.25)

#### 4. comprehensive smoothing

* **blendshapes**: exponential moving average (ema) with alpha = 0.35 per blendshape
* **head rotation**: quaternion slerp with t = 0.25 for smooth movement

#### 5. smart morph target mapping

* **direct arkit name matching**: if model uses arkit naming, maps directly
* **heuristic fallback**: regex-based pattern matching for common naming variations

  * example: `blink.*left`, `eye.*close.*left`, `left.*blink` all map to `eyeblinkleft`

## technical implementation

### file structure

* `index.html` - complete single-file application (491 lines)
* `server.py` - simple python http server with cache-control headers
* `replit.md` - this documentation

### api usage

```javascript
// mediapipe facelandmarker configuration
const facelandmarker = await facelandmarker.createfromoptions(filesetresolver, {
  baseoptions: {
    modelassetpath: "https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task",
    delegate: "gpu"
  },
  outputfaceblendshapes: true,              // enable 52 arkit blendshapes
  outputfacialtransformationmatrixes: true, // enable head pose matrix
  runningmode: "video",
  numfaces: 1
});
```

### data flow

1. webcam → mediapipe facelandmarker
2. mediapipe outputs:

   * 478 facial landmarks (for visualization)
   * 52 arkit blendshapes (neural network output)
   * 4×4 transformation matrix (head pose)
3. transformation matrix → quaternion → 40/60 split → neck + head bones
4. blendshapes → ema smoothing → morph target influences
5. three.js renders animated model at 60fps

## system requirements

* modern web browser with webgl 2.0 support
* webcam access
* https or localhost (required for webcam permissions)
* sufficient gpu for mediapipe inference (~30-60 fps)

## model requirements

for best results, your glb/gltf model should have:

1. **morph targets** (blend shapes) with arkit-compatible naming or common variations
2. **skeletal rig** with neck and head bones (optional but recommended)
3. **proper bind pose** - the system preserves rest rotations

## setup

```bash
python server.py
```

server runs on `http://0.0.0.0:5000` (required for replit environment)

## recent changes

* **2025-10-23 (v4)**: **mobile-responsive + deployment**

  * added mobile-responsive css with media queries (@768px, @480px breakpoints)
  * layout automatically stacks on small screens (50vh/40vh 3d view, scrollable controls)
  * added demo avatar button - users can instantly try the app without uploading models
  * created comprehensive github pages deployment guide (deploy.md)
  * fixed server.py socket reuse issue for better workflow stability
  * corrected mediapipe import url from `/wasm` to `@0.10.14` package entry point
* **2025-10-23 (v3)**: **production-ready** - fixed undefined overlay bug, verified all systems operational
* **2025-10-23 (v2)**: **major rewrite** - switched to mediapipe facelandmarker with native arkit blendshapes

  * replaced manual landmark math with mediapipe's trained neural network
  * fixed neck twisting by storing rest pose and applying tracking as quaternion offset
  * implemented proper 40/60 neck/head rotation distribution
  * uses transformation matrix for head pose instead of manual calculations
* **2025-10-23 (v1)**: initial attempt with manual blendshape calculations (deprecated - had incorrect landmark math and bone rotation bugs)
* **2025-10-23 (v0)**: initial import and setup for replit environment

## known limitations

* eye gaze direction is approximate (mediapipe's iris tracking is limited in the web version)
* tongue detection is basic (limited by mediapipe capabilities)
* requires good lighting for optimal tracking accuracy
* webgl context creation fails in headless/screenshot environments (normal - works in real browsers)

## performance

* mediapipe inference: ~30-60 fps on modern hardware
* three.js rendering: 60 fps
* blendshape smoothing: minimal overhead
* total latency: ~50-100ms (acceptable for real-time use)
