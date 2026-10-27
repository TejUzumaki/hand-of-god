# ✋ The Hand of God

A hand-tracked arcade game that runs entirely in your browser. Your real hands are the controller: catch glowing energy spheres with an open palm, throw them into a golden ring with a closed fist, chain combos, and duel a friend online.

Built as a single `index.html` file with Three.js, MediaPipe Hands and PeerJS. No build step, no backend.

## Features

- **Hand-tracked gameplay**: open palm to catch, fist to throw, with a full 21-point hand skeleton overlay.
- **Ink-bleed trail**: your fingertip leaves a soft ink trail that spreads and fades.
- **Solo mode**: reach 200 points in 3 minutes.
- **Online duel**: peer-to-peer match with a 6-character room code.
  - See your opponent's hand skeleton in the play field.
  - Friend's camera shown picture-in-picture, like a video call.
- **Power-ups**: bonus points, +10 seconds, and 8 seconds of double points.
- **Difficulty ramp**: spawn rate and orb speed increase over the match.
- **Auto-hide UI**: after about 2.5 seconds without a screen touch, menus fade out. Only a small scoreboard and the opponent's tracking remain. Any tap brings the UI back.
- **Fullscreen**: ⛶ button, plus auto-fullscreen when you start playing.
- **First-run tutorial**: practice screen with a hand/palm/fist check and a **Reinitialize hand tracking** button, so you never need to reload the page.
- **Tracker watchdog**: if tracking stalls for 6 seconds, it restarts automatically.
- **Offline tracker**: save the MediaPipe files on your device (Cache Storage) for faster, more reliable loading.
- **Match history**: every match is saved with date, time, mode, result and score.

## How to play

| Gesture | Action |
| --- | --- |
| ✋ Open palm over a sphere | Catch it (power-ups are collected the same way) |
| ✊ Close your fist | Throw the held sphere |
| ☝️ Move your fingertip | Draw an ink trail |

Throw spheres through the **golden ring** to score. Consecutive hits build your combo (up to ×8). A throw that misses the ring resets your combo.

## Online duel

1. Both players open the deployed site and tap **Online Duel**.
2. One player taps **Create Room** and shares the 6-character code.
3. The other player enters the code and taps **Join Room**.
4. Both tap **I'm Ready** (this starts the camera) and the match begins.

The host is authoritative for orbs, scoring and the match clock. The guest sends its hand data and renders host snapshots. Packets carry a match ID and sequence number so stale data is ignored.

> Video and online play use public STUN servers. Some strict mobile or corporate networks may need a TURN server for a direct connection.

## Run locally

Camera access requires **HTTPS or localhost**.

```bash
# from the project folder
npx serve .
# or
python3 -m http.server 8000
```

Then open `http://localhost:3000` (or `:8000`) in a modern browser.

## Deploy

The project is a static site and deploys directly to Vercel:

```bash
git add .
git commit -m "Update The Hand of God"
git push
```

With the GitHub repo connected to Vercel, every push to the main branch deploys automatically over HTTPS.

## Tech stack

- [Three.js](https://threejs.org/) r128: 3D orbs, goal ring and particles
- [MediaPipe Hands](https://developers.google.com/mediapipe) 0.4.1675469240: hand landmark tracking
- [PeerJS](https://peerjs.com/) 1.5.4: WebRTC data and video connections
- Vanilla JavaScript, HTML and CSS in one file

## Troubleshooting

- **No skeleton appears**: tap **↻ Reinitialize hand tracking** (tutorial screen) or **↻ Tracking** (in game). Saving the tracker on your device from the tutorial also helps.
- **Camera not starting**: make sure the site is served over HTTPS and camera permission is allowed.
- **Fullscreen does nothing on iPhone**: Safari doesn't support it. Use Share → Add to Home Screen.
- **Can't connect to a friend**: check the room code, and try a different network if you're behind a strict firewall.

## Project structure

```
.
├── index.html   # the entire game
└── README.md
```

## Browser support

Latest Chrome, Edge, Safari and Firefox with WebGL and webcam support. Best experienced on a device with a front camera in good lighting.

## License

Add your preferred license here (for example, MIT).
