# mirror-face

A real-time face-tracking web application that uses MediaPipe Face Mesh to animate 3D models with your facial expressions.

## Features

- **Real-time Face Tracking**: Uses your webcam and MediaPipe Face Mesh to track facial movements
- **3D Model Support**: Upload GLB/GLTF files with morph targets
- **Automatic Mapping**: Automatically detects and maps facial features to morph targets
- **Custom Mapping**: Manually configure morph target mappings for your specific model
- **Head Pose Tracking**: Smooth head rotation using quaternion interpolation
- **Expression Support**: Tracks jaw open, eye blinks, smiles, and more

## How to Use

1. **Start the Application**: The app loads with a 3D viewport on the left and controls on the right
2. **Upload a 3D Model**: Click "Choose File" to upload a GLB or GLTF file with morph targets
3. **Allow Webcam Access**: Grant permission when prompted to enable face tracking
4. **Customize Mapping** (optional): Adjust the morph target mappings in the text fields if needed
5. **Animate**: Move your head and make facial expressions to see your 3D model animate in real-time!

## Supported Morph Targets

The app automatically maps to common morph target names:
- Jaw/mouth open
- Eye blinks (left/right)
- Smiles
- Mouth funnel/pucker
- Cheek puff
- And more...

## Technical Details

- **Framework**: Three.js for 3D rendering
- **Face Tracking**: MediaPipe Face Mesh
- **No Build Required**: Pure HTML/JavaScript, dependencies loaded from CDNs
- **WebGL Required**: Needs a browser with WebGL support

## Requirements

- Modern web browser with WebGL support
- Webcam access
- HTTPS or localhost (required for webcam permissions)

## Development

The application runs on a simple Python HTTP server:

```bash
python server.py
```

Server runs on port 5000 by default.
