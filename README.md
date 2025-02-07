
## NPR Pipeline Plugin

  - **G-buffer Pass** to store geometry (color, normals, velocity, depth)
  - **Subsequent Passes** (Phong, Outline, Hatching, Watercolor, Final) read from G-buffer
- **Dynamic Objects**:
  - For animated meshes, vertex data is updated from `.dat` files each frame
  - Efficient approach avoids re-loading entire geometry
---

### Scene Preparation
- **Starting Point**:
  - Used Blender demo “Tree Creature” scene
  - Reorganized objects, combined UV maps for fewer textures
- **Baking & Exporting**:
  - Baked diffuse colors into textures in Blender
  - Exported to Houdini, triangulated the meshes
  - **Houdini Node Setup**: Exports per-frame data (`.dat` files for positions, normals, velocities, UVs)
- **Scene Data**:
  - `scene.dat` file lists objects, their triangle and point count, and flags for static/animated

---



### Multi-Pass Rendering

| **Pass**         | **Purpose**                                                                       | **Input**                                         | **Output (Images)**                             |
|------------------|-----------------------------------------------------------------------------------|---------------------------------------------------|-------------------------------------------------|
| **1. G-buffer**  | Collect geometry data (base color, normals, velocity, depth) into multiple attachments | Scene geometry and baked textures       | *(Placeholder for G-buffer image)*             |
| **2. Phong**     | Basic Phong lighting to get a lit color pass                                      | G-buffer (base color, normals, depth)            | *(Placeholder for Phong pass image)*           |
| **3. Outline**   | Edge detection using Sobel on normals, outline thickness                          | Normals                      | *(Placeholder for Outline pass image)*         |
| **4. Hatching**  | Diagonal cross-hatching pattern in dark areas, controlled by a uniform            | Phong pass             | *(Placeholder for Hatching pass image)*        |
| **5. Watercolor**| Painterly or noise-based watercolor effect                                        | Phong pass              | *(Placeholder for Watercolor passs image)*      |
| **6. Final**     | Combines Outline, Hatching, Watercolor, toon quantization & grayscale        | Outline, Hatching, Watercolor passes             | *(Placeholder for Final composite image)*      |

---

### **Slide 4: UI & Key Controls**
**Title**: *User Interface & Dynamic Objects*
- **Playback**: Play, Pause, Stop; adjustable FPS
- **Camera**: Orbit controls; adjustable FoV, clipping planes
- **Lighting**: Editable direction (longitude/latitude), distance
- **Effects**:
  - Outline thickness
  - Hatching intensity
  - Watercolor mode (simple/painterly), radius, strength
  - Toon quantization (bands, grayscale option)
- **Debug View**: Switch among G-buffer, Phong, Outline, etc.
