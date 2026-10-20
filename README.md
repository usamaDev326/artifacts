# artifacts

Amazing artifacts made by AI.

A daily collection of small, self-contained browser games and interactive pages with a desi touch. Each artifact lives in its own folder as a single `index.html` with no build step and no dependencies.

## Artifacts

| Artifact | Description |
| --- | --- |
| [Bo Kata](bo-kata/) | Basant kite-fighting over Lahore. Cross dor for a pench and saw to cut rival patangs. |
| [Load Shedding](load-shedding/) | Find items on Ammi ki list in a dark room with a torch, swat machar and manage the battery. |
| [Lantern Drift](lantern-drift/) | Paper boat with a diya on the night Ravi. Collect diyas to keep the lau alive, ride combos and dodge bhanwar, rocks and logs. |
| [Maze Quest](maze-quest/) | Torch-lit galiyan of Andaroon Lahore. Grab jalebis and the chabi, reach the darwaza and escape Moti the kutta. |
| [Moonlight Moth](moonlight-moth/) | Parwana and shama in a haveli room. Fly close to the flame for a x5 multiplier without singeing your wings. |
| [Paper Skies](paper-skies/) | Steer a paper plane through golden rings while dodging clouds and wind gusts. |

## Run locally

Open any artifact's `index.html` directly in a browser, or serve the repo:

```bash
npx serve .
```

Then visit `http://localhost:3000/<artifact-folder>/`.

## Structure

```
artifacts/
├── <artifact-name>/
│   └── index.html
├── GAMES-REVIEW.md   # review and fix plan for the games
└── README.md
```

New artifacts are added daily, one folder per artifact.

## Controls

All games work on desktop and mobile. Tap or click once to start and enable sound.

| Artifact | Controls |
| --- | --- |
| Bo Kata | Drag anywhere or arrow keys |
| Load Shedding | Move the torch, tap items and mosquitoes |
| Lantern Drift | Drag, touch or WASD |
| Maze Quest | Swipe, tap, arrows or WASD |
| Moonlight Moth | Pointer, touch or WASD |
| Paper Skies | Pointer, touch or arrow keys |

## Built with

- Plain HTML, CSS and JavaScript on a single `<canvas>`
- Web Audio API for all sound effects, no audio files
- Google Fonts: Rozha One, Noto Nastaliq Urdu and IBM Plex Mono
- `localStorage` for best scores

## Adding a new artifact

1. Create a new folder with a short kebab-case name, e.g. `my-game/`.
2. Put the whole artifact in a single `my-game/index.html`.
3. Add a row for it in the Artifacts and Controls tables above.
4. Commit it on its own with a message like `Usama: "My Game - short description"`.
