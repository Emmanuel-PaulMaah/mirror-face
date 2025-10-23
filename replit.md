# mirror-face

## Overview
A face-tracking web application that uses MediaPipe Face Mesh to detect facial movements and map them to morph targets in 3D models. Users can upload GLB/GLTF files with morph targets, and the app will animate the model based on their facial expressions captured through the webcam.

## Project Type
- Pure frontend application (HTML/JavaScript)
- No build system required
- Dependencies loaded from CDNs (Three.js, MediaPipe)

## Architecture
- **Single-file application**: `demo.html`
- **3D Rendering**: Three.js for rendering 3D models
- **Face Tracking**: MediaPipe Face Mesh for facial landmark detection
- **Features**:
  - Upload custom GLB/GLTF models with morph targets
  - Real-time facial tracking via webcam
  - Automatic mapping of facial features to morph targets
  - Customizable morph target mapping
  - Head pose rotation with quaternion smoothing

## Setup
- Requires a simple HTTP server to serve the HTML file
- Uses webcam (requires HTTPS or localhost for browser permissions)

## Deployment
- Configured for autoscale deployment
- Runs Python HTTP server on port 5000
- No build step required

## Recent Changes
- 2025-10-23: Initial import and setup for Replit environment
  - Installed Python 3.11
  - Created server.py to serve the application
  - Renamed demo.html to index.html
  - Set up workflow to run server on port 5000
  - Configured deployment for autoscale
  - Updated README with usage instructions
