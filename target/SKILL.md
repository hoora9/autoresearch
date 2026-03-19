---
name: webgl-3d-dev
description: >
  Comprehensive guide for WebGL and 3D web development skills. Use this skill whenever the user asks about
  learning or building with WebGL, Three.js, React Three Fiber, GLSL shaders, 3D modeling for the web,
  Blender-to-web pipelines, or real-time 3D graphics in the browser. Also trigger when the user mentions
  GPU programming, shader writing, 3D asset optimization, glTF workflows, procedural generation, WebGPU,
  or wants to create interactive 3D experiences, product configurators, data visualizations in 3D,
  immersive web experiences, or portfolios with 3D elements. If the user references Three.js, Babylon.js,
  R3F, or any WebGL-related library, use this skill.
  Do NOT trigger for: 2D scroll animations without 3D (use kinetic-minimalism), general frontend UI (use frontend-design), Figma-to-code (use figma-designer), GSAP-only animation reference (use gsap-cheat-sheet-skills), or video-to-website conversions (use video-to-website).
---

# WebGL & 3D Web Development Skill Guide

A structured reference for mastering WebGL and 3D web development — from foundational math to production-ready immersive experiences.

---

## 1. Core Technical Foundation

### 3D Mathematics
- **Linear algebra**: vectors, matrices (model, view, projection), quaternions for rotation
- **Coordinate systems**: world space, object space, camera space, clip space, screen space
- **Transformations**: translation, rotation, scaling, and combining via matrix multiplication
- **Interpolation**: lerp, slerp, easing functions for smooth animations

### The Rendering Pipeline
Understand the full GPU pipeline:

```
Vertex Data → Vertex Shader → Primitive Assembly → Rasterization → Fragment Shader → Framebuffer
```

Key concepts: draw calls, GPU state management, depth buffering, stencil operations, blending modes.

---

## 2. WebGL & Shaders

### Raw WebGL
- Creating and managing WebGL contexts
- Buffers: vertex buffers, index buffers, uniform buffers
- Textures: 2D, cubemaps, data textures, texture units
- Framebuffer objects (FBOs) for off-screen rendering and post-processing
- Extensions and capability detection

### GLSL (OpenGL Shading Language)
- **Vertex shaders**: transform geometry, pass varyings
- **Fragment shaders**: compute pixel color, lighting, effects
- Uniforms, attributes, varyings
- Built-in functions: `mix`, `smoothstep`, `clamp`, `dot`, `cross`, `normalize`
- Precision qualifiers and mobile considerations

**Example — basic vertex shader:**
```glsl
attribute vec3 position;
uniform mat4 modelViewMatrix;
uniform mat4 projectionMatrix;

void main() {
  gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
}
```

---

## 3. 3D Frameworks & Libraries

### Three.js (Primary)
The dominant library for web 3D. Key areas:
- Scene graph: Scene, Camera, Mesh, Light, Group
- Geometries: BufferGeometry, instanced geometry
- Materials: MeshStandardMaterial, ShaderMaterial, RawShaderMaterial
- Loaders: GLTFLoader, DRACOLoader, KTX2Loader
- Controls: OrbitControls, FlyControls, custom controls
- Post-processing: EffectComposer, render passes

### React Three Fiber (R3F)
Declarative Three.js in React. Key ecosystem:
- `@react-three/fiber` — core renderer
- `@react-three/drei` — helpers (Html, Environment, ContactShadows, etc.)
- `@react-three/postprocessing` — effects
- `@react-three/rapier` — physics

### Other Frameworks
- **Babylon.js** — full-featured alternative, strong editor tooling
- **PlayCanvas** — editor-driven, good for collaborative teams
- **Spline** — no-code 3D for designers, exportable to web

---

## 4. 3D Modeling & Asset Pipeline

### Blender (Primary Tool)
- Modeling: box modeling, sculpting, modifiers
- UV unwrapping and texture baking
- Rigging and animation for web export
- glTF export settings and optimization

### Asset Optimization (Critical for Web)
Transform heavy 3D assets into web-ready formats:

| Technique | Purpose | Tool |
|-----------|---------|------|
| Mesh decimation | Reduce polygon count | Blender Decimate modifier |
| Draco compression | Compress geometry | `gltf-pipeline`, Three.js DRACOLoader |
| KTX2/Basis textures | GPU-compressed textures | `toktx`, KTX2Loader |
| Texture atlasing | Reduce draw calls | Blender bake, custom tools |
| LOD (Level of Detail) | Distance-based quality | Three.js LOD object |
| glTF/GLB format | Standard web 3D format | Blender, glTF-Transform |

**Target budgets:**
- Hero model: < 500KB (compressed)
- Full scene: < 2–5MB total
- Textures: 1K or 2K max, use KTX2 where possible
- Draw calls: < 50 for mobile, < 200 for desktop

---

## 5. Performance Optimization

### Rendering Performance
- **Instanced rendering**: draw thousands of identical objects in one call
- **Draw call batching**: merge static geometries
- **Frustum culling**: skip objects outside camera view
- **Occlusion culling**: skip objects hidden behind others
- **Texture compression**: KTX2/Basis Universal for GPU-native formats

### Profiling Tools
- **Spector.js** — WebGL call inspector
- **Chrome DevTools Performance tab** — frame timing
- **Three.js renderer.info** — draw calls, triangles, textures in memory
- **stats.js** — FPS/MS/MB overlay

### Device Adaptation
Detect GPU capability and adapt quality:
```javascript
const gl = renderer.getContext();
const debugInfo = gl.getExtension('WEBGL_debug_renderer_info');
const gpu = gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL);
// Adjust quality tier based on GPU string
```

---

## 6. Shader Art & Visual Effects

### Post-Processing
- Bloom, depth of field, SSAO (screen-space ambient occlusion)
- Color grading, vignette, chromatic aberration
- Custom passes with ShaderMaterial

### Procedural Techniques
- **Noise functions**: Perlin, Simplex, Worley — for organic textures, terrain, clouds
- **Raymarching**: render complex shapes via signed distance fields (SDFs)
- **Particle systems**: GPU-driven with buffer attributes or compute
- **Generative geometry**: parametric surfaces, L-systems, fractals

### Inspirational Resources
- [Shadertoy](https://shadertoy.com) — shader playground and community
- [The Book of Shaders](https://thebookofshaders.com) — foundational shader guide
- [Inigo Quilez articles](https://iquilezles.org) — SDF and procedural techniques

---

## 7. Physics & Interaction

### Physics Engines
- **Rapier** (WASM) — fast, modern, great R3F integration
- **Cannon.js / cannon-es** — pure JS, good for simple simulations
- **Ammo.js** — Bullet physics compiled to WASM, heavy but full-featured

### Interaction Patterns
- **Raycasting**: detect mouse/touch intersection with 3D objects
- **Drag controls**: TransformControls, DragControls
- **Spatial data structures**: BVH (bounding volume hierarchy), octrees for fast queries
- **Custom cursor feedback**: hover states, click animations on 3D objects

---

## 8. Web Fundamentals for 3D

### JavaScript/TypeScript
- `requestAnimationFrame` render loops
- Web Workers for offloading heavy computation (mesh generation, physics)
- SharedArrayBuffer for zero-copy data transfer
- TypedArrays (Float32Array, Uint16Array) for buffer data

### WebAssembly
- Use for compute-heavy tasks: physics, pathfinding, mesh processing
- Rust → WASM is a popular pipeline (wasm-bindgen, wasm-pack)

### Responsive 3D
- Adapt canvas size, pixel ratio, and quality to device
- Handle resize events and pixel density (`renderer.setPixelRatio`)
- Reduce shadow map size, particle count, post-processing on mobile

---

## 9. Emerging Technologies

### WebGPU
The successor to WebGL with compute shader support:
- Modern API design (closer to Vulkan/Metal/DX12)
- Compute shaders for GPU-driven simulations
- Better performance and lower overhead
- Three.js WebGPURenderer already in development

### Gaussian Splatting
Photogrammetry-based 3D on the web:
- Capture real-world scenes as point clouds
- Render via splatting for photorealistic results
- Libraries: `@mkkellogg/gaussiansplat3d`, Luma AI

### AI-Assisted 3D
- Text-to-3D generation (Meshy, Tripo, Rodin)
- AI texture generation for 3D models
- NeRF and 3D Gaussian Splatting from photos

---

## 10. Design Sensibility

Technical skills alone don't create great 3D web experiences. Develop:

- **Lighting**: three-point lighting, HDRI environments, baked vs. real-time
- **Composition**: camera placement, focal length, rule of thirds in 3D
- **Camera movement**: smooth easing, parallax, scroll-driven camera paths
- **Art direction**: consistent materials, color palettes, mood
- **Motion design**: timing, easing curves, staggered reveals (synergizes with GSAP)

The gap between a tech demo and a premium experience is almost always art direction, not code.

---

## Learning Path (Suggested Progression)

1. **Foundation** → Linear algebra basics + Three.js "Hello Cube"
2. **Geometry & Materials** → Load glTF models, apply PBR materials, add lights
3. **Interaction** → Raycasting, OrbitControls, responsive canvas
4. **Animation** → GSAP + Three.js integration, scroll-driven 3D
5. **Shaders** → The Book of Shaders → custom ShaderMaterial
6. **Asset Pipeline** → Blender basics → export → optimize → load
7. **Performance** → Profiling, instancing, LOD, texture compression
8. **Advanced** → Post-processing, physics, procedural generation
9. **Emerging** → WebGPU, Gaussian splatting, compute shaders
10. **Portfolio** → Build 2–3 showcase projects combining all skills

---

## Key Tools & Resources

| Category | Tools |
|----------|-------|
| 3D Library | Three.js, React Three Fiber, Babylon.js |
| Modeling | Blender, Spline |
| Shaders | Shadertoy, The Book of Shaders, GLSL Sandbox |
| Optimization | glTF-Transform, Draco, toktx, Spector.js |
| Physics | Rapier, Cannon-es, Ammo.js |
| Profiling | Spector.js, Chrome DevTools, stats.js |
| Inspiration | Awwwards, Codrops, Three.js examples gallery |
