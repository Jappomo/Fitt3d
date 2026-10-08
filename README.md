# FITT3D

Web tool for fitting 3D garments onto an avatar. Version 0.0.1 (beta).

The whole app is one file, `index.html`. Everything it ships with lives in `assets/`.

## Folder structure

```
index.html                       the app
assets/
  manifest.json                  list of everything shipped (read at startup)
  avatars/
    male_01/
      Male_01.fbx                default avatar
      textures/                  its albedo / normal maps
  animations/                    animation clips (Pose menu)
  garments/                      demo garments + thumbnails (Wardrobe > Demos)
```

## Adding content

Drop the files in `assets/` and list them in `assets/manifest.json`. No code changes.

```json
{
  "version": 1,
  "defaultAvatar": "male_01",
  "avatars": [
    { "id": "male_01", "name": "Male 01", "file": "avatars/male_01/Male_01.fbx",
      "maps": { "albedo": "avatars/male_01/textures/albedo.webp",
                "normal": "avatars/male_01/textures/normal.webp", "normalScale": 1 } }
  ],
  "animations": [
    { "name": "Walk", "file": "animations/walk.glb" }
  ],
  "garments": [
    { "name": "T-shirt", "file": "garments/tshirt/tshirt.glb", "thumb": "garments/tshirt/thumb.webp" }
  ]
}
```

- Paths are relative to `assets/`.
- `defaultAvatar` is the `id` of the avatar that loads at startup.
- Avatar maps apply unless the user loads their own textures in the app. Use `null` for a map you don't have.
- Animations appear under "Clips from file" in the Pose menu. They need the same bone names as the avatar. Only rotations are used (root motion is ignored).
- Demo garments appear under Demos in the Wardrobe. Clicking one opens Adjust fit, and Done saves it to the user's library.
- Formats: meshes .glb, .gltf, .fbx, .obj. Images .png, .jpg, .webp.

## Deploy on GitHub Pages

Commit `index.html` and the `assets/` folder to the repo, then set **Settings → Pages → Source** to deploy from your branch. Test locally with any static server (for example `python -m http.server`), not by double-clicking `index.html`.
