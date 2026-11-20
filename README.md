# Hollow Ward

A first-person horror game that runs in the browser. No install, no build step.

You are the night electrician at St. Aldric Sanatorium. The power failed on the lower ward and the only way out is the service lift, which needs three fuses. They are scattered through a maze that rebuilds itself every run.

## Play

Open `index.html` in a browser, or play it online with GitHub Pages (see below).

## The Warden

The Warden only moves when it is unseen.

- Lit and inside your lamp's cone: it freezes.
- Out of sight or in the dark: it hunts you through the corridors.
- Lamp off or dead: it moves faster than you can walk.
- Every fuse you take makes it quicker.

The lamp drains battery while it is on. Battery cells are hidden around the maze.

## Controls

| Key | Action |
| --- | --- |
| W A S D | Move and sidestep |
| Left / Right arrows | Turn (or move the mouse after clicking the game view) |
| F or Space | Lamp on and off |
| M | Sound on and off |

On a phone, use the buttons under the game view.

## Play online with GitHub Pages

1. Open the repository's Settings, then Pages.
2. Set the source to "Deploy from a branch", with branch `main` and folder `/ (root)`.
3. After a minute or two the game is live at `https://theboyzz.github.io/the-Hellow-ward/`.

## Tuning

All pacing values live in the `CFG` object at the top of the script in `index.html`:

| Setting | What it does |
| --- | --- |
| `drain` | Battery used per second while the lamp is on |
| `batteryGain` | Charge restored by each battery cell |
| `wardenBase`, `wardenPerFuse` | The Warden's speed, and how much faster it gets per fuse |
| `darkBoost` | Speed multiplier when you are in the dark |
| `grace` | Seconds before the Warden starts to move |
| `coneHalf` | How wide the beam counts as "looking at it", in radians |

## How it works

- A canvas raycaster draws the corridors, with sprites for fuses, batteries, the lift and the Warden.
- The maze is generated with a depth-first search, then a few walls are removed to make loops.
- The Warden finds you with a breadth-first search over the maze grid.
- Sound is generated live with the Web Audio API: a low drone, a heartbeat that quickens as the Warden nears, and footsteps.
