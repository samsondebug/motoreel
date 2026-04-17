# MotoReel

**Authentic rider reels. No hype. Just the ride, the sound, and the road.**

Client-side 9:16 video editor for motorcycle content creators. Everything runs in the browser — no uploads, no server rendering, no cloud bills. Your footage never leaves your device.

## Stack

- Static HTML + Tailwind (CDN) + vanilla JS
- [ffmpeg.wasm v0.11.6](https://github.com/ffmpegwasm/ffmpeg.wasm) for in-browser encoding
- Deployed on Vercel as a static site

## Features

- Drop clips → choose reel style → export clean 9:16 MP4
- 6 riding-mood presets (Classic Iron, Night Run, Hill Country, Raw Throttle, Long Haul, The Burn)
- Text overlays with precise in/out timing
- Optional music track with audio mixing
- Caption-ready for Instagram Reels
- `⌘ + Enter` to export

## Local dev

```bash
npx serve src
```

Open `http://localhost:3000`.

## Deploy

```bash
vercel --prod
```

`vercel.json` sets Cross-Origin Opener/Embedder policies for `SharedArrayBuffer` eligibility (future-proofing for ffmpeg.wasm v0.12+) and rewrites `/` → `/src/index.html`.

## Why ffmpeg.wasm v0.11 (not v0.12)

v0.11 uses the `createFFmpeg` / `ffmpeg.run` / `ffmpeg.FS` API and does **not** require Cross-Origin Isolation. v0.12 uses `new FFmpeg()` / `ffmpeg.exec` and requires `SharedArrayBuffer` → COOP/COEP must be strict, which is fragile on Vercel's edge. v0.11 ships today, v0.12 lives in `vercel.json` when we're ready.

## License

MIT
