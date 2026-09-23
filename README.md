# MindAR + Three.js Dragon Demo

WebAR demo: point your phone at a target image and a low-poly red dragon flies around it, flapping its wings. One HTML file, no build step.

**Live demo:** https://elfarisssaid19.github.io/mindar-demo-/mindar-threejs-demo.html

## Features

- Image tracking with [MindAR](https://github.com/hiukim/mind-ar-js) (sample card target)
- Red Dragon GLB model loaded with three.js `GLTFLoader`
- Procedural animation in a vertex shader (wing flaps, tail sway, body bob), no rig needed
- Circular flight path around the target, with banking into the turn
- Loading screen, camera/HTTPS error overlay, scanning status pill, printable target modal
- Fallback placeholder creature if the model fails to load

## Try it

1. Open the live demo on your phone (Chrome on Android, Safari on iOS).
2. Allow camera access.
3. Show the target image on another screen (tap the thumbnail in the top-right corner) or print it.
4. Point your phone at the target.

> In-app browsers (WhatsApp, Instagram...) often block the camera. Open the link in your real browser.

## Run locally

```bash
git clone https://github.com/ElFarisssaid19/mindar-demo-.git
cd mindar-demo-
python3 -m http.server 8000
```

Open http://localhost:8000/mindar-threejs-demo.html. The camera needs HTTPS or localhost, and opening the file directly (`file://`) won't load the model.

To test on a phone without deploying:

```bash
cloudflared tunnel --url http://localhost:8000
```

## Project structure

```
.
├── mindar-threejs-demo.html   # HTML, CSS and JS in one file
└── assets/
    └── dragon.glb             # Red Dragon model (static mesh)
```

## Customization

All tunables live in the `CONFIG` object at the top of the script:

| Key | What it does |
|---|---|
| `TARGET_SIZE` | Model size relative to the target width (1 = full width) |
| `FLIGHT_RADIUS`, `LAP_SECONDS`, `FLIGHT_HEIGHT` | Flight path around the target |
| `FORWARD_OFFSET` | Fixes the heading if the dragon flies sideways or backwards |
| `BODY_AXIS`, `SPAN_AXIS`, `UP_AXIS`, `TAIL_SIGN` | Override the auto-detected axes used by the wing and tail animation |
| `WING_START`, `TAIL_START` | Where the wings and the tail start bending |
| `DEBUG` | Shows axes and bounding box helpers |

To use another model, replace `assets/dragon.glb`. A model that ships its own animation clips should use an `AnimationMixer` instead of the procedural shader.

## Tech stack

- [MindAR](https://github.com/hiukim/mind-ar-js) 1.2.5 for image tracking
- [three.js](https://threejs.org) as ES modules via importmap, from jsDelivr
- GitHub Pages for hosting

## Credits

- [Red Dragon](https://poly.pizza/m/5SgYrV6nhws) by Tomek Zamojski, CC-BY, via Poly Pizza
- [MindAR](https://github.com/hiukim/mind-ar-js) by HiuKim Yuen (MIT), including the sample target image
- [three.js](https://threejs.org) (MIT)

## Author

Said El Fariss, [@ElFarisssaid19](https://github.com/ElFarisssaid19)
