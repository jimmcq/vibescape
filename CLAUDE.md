# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**VibeScape** is an audio-reactive 3D landscape built using the "vibe coding" methodology - a conversational, improvisational development approach popularized by Andrej Karpathy. The project transforms music into flowing, organic 3D visuals where terrain pulses with bass, particles dance to melodies, and colors shift with different instruments.

## Development Commands

**No build system required** - This is a single-file HTML application:
- **Run locally**: Open `index.html` directly in a browser or serve via any static server
- **Development**: Edit `index.html` and refresh browser to see changes
- **Deploy**: Upload `index.html` to any static hosting service
- **Test audio**: Requires microphone access - use `https://` or `localhost` for browser permissions

## Architecture

### Single-File Application Structure
All code lives in `index.html` with embedded CSS and JavaScript. Core architecture:

```javascript
class VibeScape {
  // 3D Rendering (Three.js)
  scene, camera, renderer, terrain
  
  // Audio Processing (Web Audio API)
  audioContext, analyser, microphone, dataArray
  
  // Audio Analysis Bands
  bassLevel, midLevel, highLevel, overallLevel
}
```

### Technology Stack
- **Three.js r128** (CDN) - 3D rendering and scene management
- **Web Audio API** - Real-time frequency analysis
- **Vanilla JavaScript** - No frameworks or build tools
- **HTML5 Canvas** - WebGL rendering surface

### Audio Processing Pipeline
1. **Microphone capture** → MediaStream
2. **Web Audio API** → Frequency analysis (FFT 512)
3. **Band separation**: Bass (0-10%), Mids (10-60%), Highs (60-100%)
4. **Visual mapping**: Bass → terrain displacement, Mids → colors, Highs → particles

### Visual Components
- **Terrain**: PlaneGeometry (200x200, 50x50 segments) with vertex displacement
- **Camera**: Orbital movement responding to audio energy
- **Lighting**: Ambient + directional with dynamic color shifts
- **Materials**: Phong materials with HSL color mapping

## Vibe Coding Methodology

This project follows vibe coding principles:

### Development Approach
- **Aesthetic over architecture** - Visual impact prioritized over code structure
- **Conversational iteration** - Describe desired effects in natural language, implement quickly
- **Immediate feedback** - Every change should be visible instantly
- **Embrace emergence** - Unexpected visual effects become features
- **Flow state focus** - Maintain momentum, avoid perfectionism

### Implementation Pattern
1. **Start broad** - "Make terrain pulse with music"
2. **Refine through conversation** - "Make the pulsing smoother and more wave-like"
3. **Layer complexity** - Add particles, colors, camera movement iteratively
4. **Visual-first decisions** - If it looks amazing, the code is working

## Development Phases

### Completed (Phase 1-2)
- ✅ Audio foundation with microphone input and frequency analysis
- ✅ Basic 3D terrain responsive to bass frequencies
- ✅ Dynamic color shifting based on mid frequencies
- ✅ Camera movement synchronized with overall audio energy

### Next Phases
- **Phase 3**: Particle systems for mid/high frequency visualization
- **Phase 4**: Enhanced color dynamics and gradient mapping
- **Phase 5**: Advanced camera flow and user controls
- **Phase 6**: Visual polish (lighting effects, post-processing)
- **Phase 7**: Multiple audio sources (file upload, samples, SoundCloud)

## Key Implementation Details

### Audio Analysis
```javascript
// Frequency band extraction
bassLevel = dataArray[0...10%] average / 255
midLevel = dataArray[10%...60%] average / 255  
highLevel = dataArray[60%...100%] average / 255
```

### Terrain Animation
```javascript
// Vertex displacement based on audio
wave = sin(distance * 0.02 + time) * bassLevel * amplitude
position.setZ(i, wave)
```

### Color Mapping
```javascript
// HSL color shifts with audio
hue = midLevel * 0.8 + 0.5
material.color.setHSL(hue, 0.8, 0.5 + overallLevel * 0.3)
```

## Browser Requirements
- **WebGL support** for Three.js rendering
- **Web Audio API** support (modern browsers)
- **Microphone permissions** for audio input
- **HTTPS or localhost** required for microphone access

## Performance Targets
- **60fps rendering** for smooth audio-visual synchronization
- **Real-time audio processing** with minimal latency
- **Responsive design** for various screen sizes
- **Smooth interpolation** for all visual transitions