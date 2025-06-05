# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a JavaScript-based animated space demo called "STELLAR WAVE" that showcases multiple layered visual effects in a single HTML file. The demo features:

- **Scrolling text animation** with sine wave motion and gradient coloring
- **3D rotating star sphere** that bounces around the screen
- **Gaseous cloud particles** floating within the sphere
- **Background starfield** with parallax motion
- **Responsive canvas** that adapts to window size

## Running the Demo

Open `index.html` directly in a web browser or serve it with a local HTTP server:
```bash
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## Code Architecture

The entire application is contained in a single HTML file with embedded CSS and JavaScript. The main components are:

### Animation System
- **Main loop**: `animate()` function using `requestAnimationFrame`
- **Rendering order**: Background stars → Cloud particles → Star sphere → Scrolling text
- **Global state**: Sphere position, rotation angles, particle arrays

### 3D Mathematics
- **Rotation functions**: `rotateX()`, `rotateY()`, `rotateZ()` for 3D transformations
- **Perspective projection**: Using `scale = 500 / (500 + z)` for depth
- **Coordinate systems**: Screen coordinates for canvas, 3D coordinates for sphere objects

### Particle Systems
1. **Star sphere**: 144 points (12x12 grid) distributed on sphere surface using spherical coordinates
2. **Cloud particles**: 150 particles with independent drift animation using sine waves
3. **Background stars**: 75 parallax stars with depth-based speed

### Performance Considerations
- Avoid complex gradients in particle rendering (causes NaN errors)
- Use `isFinite()` checks when creating radial gradients
- Keep particle counts reasonable for smooth animation
- Simple particle physics for smooth motion

## Key Parameters

### Sphere Configuration
- `sphereRadius`: 100px
- `sphereVelocity`: ±4 pixels per frame
- `rotationSpeed`: {x: 0.01, y: 0.02, z: 0.03} radians per frame

### Cloud Particles
- Count: 150 particles
- Size: 1-4px radius
- Distribution: 1.2x sphere radius
- Drift amplitude: 8px sine wave motion

### Text Animation
- Font: 48px Arial bold
- Wave amplitude: 100px
- Character spacing: 30px
- Scroll speed: 2px per frame

## Common Modifications

When adding particle effects:
1. Start with simple colored circles to verify visibility
2. Add transparency and gradients only after basic rendering works
3. Use fixed sizes initially, then add variable sizes
4. Implement basic movement before complex animations