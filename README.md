# Head Parallax

Your laptop screen becomes a window into a 3D room. The webcam tracks your head,
and the view is redrawn from your eye position, so moving left, right, up or down
changes the perspective like looking through real glass.

**Live demo:** https://martinerlam.github.io/head-parallax/

## How it works

- **Face tracking:** [MediaPipe Face Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/face_landmarker)
  runs in the browser and finds your eyes. Their midpoint gives your head position;
  the distance between them estimates how far you are from the screen.
- **Off-axis projection:** [three.js](https://threejs.org/) renders the scene with
  a camera at your eye, and the screen edges are treated as the window frame. That
  is what makes it look deep rather than just sliding.
- **Scene:** a grid-lined room with an image on the back wall, lit objects floating
  at different depths (some in front of the screen) and soft shadows on the floor.

Everything is in a single file, `index.html`. There is no build step.

## Running it

Browsers only allow the camera on `https://` or `http://localhost`, so opening
`index.html` directly won't track your head (it falls back to the mouse).

Either use the live demo link above, or run it locally:

```bash
python3 -m http.server 8123
```

Then open http://localhost:8123 and allow camera access. If it's still refused,
check System Settings → Privacy & Security → Camera.

## Controls

| Control | What it does |
| --- | --- |
| Sensitivity | How much a head movement shifts the view |
| Use my image / drag and drop | Put your own picture on the back wall |
| Camera | Retry the camera, or show/hide the webcam preview |
| Recenter | Make your current head position the neutral one |
| Back image | Show or hide the back-wall picture |
| Shape, Solid / Wireframe | Spheres, cubes, rings or discs, lit or as outlines |
| Gloss, Count, Pop out, Size | Object finish, number, how far they come forward, size |
| Shuffle | New random layout |
| Pulse, Glow | Objects swell and shrink, and light up as they swell |
| Ripple / Random / Together | Pulse as a wave from back to front, each on its own beat, or all in sync |
| Pulse speed, Pulse amount | How fast and how big the pulse is |
| Lighting (dropdown) | Ambient, key light strength/direction/height/warmth, room tone, shadows, head lamp, coloured rim lights |
| H key | Hide the panel |

**Tip:** close one eye and move slowly. The view is calculated for a single
point, so the depth is much stronger with one eye.

## Working on it

Make a branch for each experiment so `main` always works:

```bash
git switch -c try-something
```

Commit as you go, then merge into `main` if it worked or delete the branch if it didn't.
The live demo updates automatically from `main`.
