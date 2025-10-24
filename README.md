# mirror-face

real-time face-tracking web app that uses mediapipe face mesh to animate human 3d models with your facial expressions. 

upload your model, enter model url or load demo model.

[use mirror-face](https://emmanuel-paulmaah.github.io/mirror-face/)

## features

- **real-time Face Tracking**: uses your webcam and MediaPipe Face Mesh to track facial movements
- **3d model support**: upload glb/gltf files with morph targets
- **automatic mapping**: automatically detects & maps facial features to morph targets
- **custom mapping**: manually configure morph target mappings for your specific model
- **head pose tracking**: smooth head rotation using quaternion interpolation
- **expression support**: tracks jaw open, eye blinks, smiles, & more

## how to use

1. **start the app**: the app loads with a 3d viewport on the left & controls on the right
2. **upload a 3d model**: click "choose file" to upload a glb or gltf file with morph targets
3. **allow webcam access**: grant permission when prompted to enable face tracking
4. **customize mapping** (optional): adjust the morph target mappings in the text fields if needed
5. **animate**: Move your head and make facial expressions to see your 3D model animate in real-time!

## supported morph targets

the app automatically maps to common morph target names:
- jaw/mouth open
- eye blinks (left/right)
- smiles
- mouth funnel/pucker
- cheek puff
- & more...

## technical Details

- **framework**: three.js for 3d rendering
- **face tracking**: mediapipe face mesh
- **no build required**: pure html/javascript, dependencies loaded from cdn
- **webgl required**: needs a browser with webgl support

## requirements

- modern web browser with WebGL support
- webcam access
- https or localhost (required for webcam permissions)

## development

app runs on a simple python http server:

```bash
python server.py
```

server runs on port 5000 by default.
