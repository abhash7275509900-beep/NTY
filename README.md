# Nova by Aditya

Premium video player for laptop and Android. Source is in `www/` (plain HTML/CSS/JS, no build step).

## Laptop (Windows / Mac / Linux)
1. Run `run-on-laptop.bat` (Windows) or `./run-on-laptop.sh` (Mac/Linux). Needs Python.
2. In Chrome or Edge, click **Install app** (or the install icon in the address bar). Nova then opens as its own window and appears in "Open with" for video files.

## Android — install without building
Host the `www/` folder on any HTTPS host (GitHub Pages, Netlify, Cloudflare Pages), open it in Chrome on your phone, then Menu > **Install app**.

## Android — build the APK
Option A (no setup): push this folder to a GitHub repo. The workflow in `.github/workflows/build-apk.yml` builds `app-debug.apk`; download it from the Actions run's Artifacts.
Option B (local): install Node 20, JDK 21 and Android Studio, then
```
npm install
npx cap add android
cp native/*.java android/app/src/main/java/com/aditya/nova/
npx cap sync android
cd android && ./gradlew assembleDebug
```
APK: `android/app/build/outputs/apk/debug/app-debug.apk`. Transfer it to the phone and allow "install unknown apps".

## Features
Immersive playback (APK): the status and navigation bars hide while a video is loaded; swipe down from the top to show them briefly. This needs the files in `native/`, which the GitHub workflow copies in automatically.
Smooth audio: heavy spatial processing only runs when a Spatial mode is on, and audio uses large buffers. Also: subtitles auto-load by matching file name, adjustable skip step (5-30s), sleep timer at end of video, screen stays awake while playing.
Redesign: home screen with Continue watching, bottom navigation on phones, big centre play controls, bookmarks (B), stats overlay, auto-fullscreen when you rotate to landscape.
Premium look: frosted-glass controls, ambient glow around the video, seek-bar thumbnail preview, live audio visualizer for music, 4K/HD badge, four colour themes (Nova, Aurora, Ember, Mono), subtitle styles, theater mode (T).
Spatial audio tab: Cinema, Music, Dialogue and Night modes with virtual rear speakers, overhead cue, room depth, stereo width and voice clarity. Nova's own Web Audio engine, best on headphones; it is not licensed Dolby Atmos decoding.
Touch gestures: swipe the left half for brightness and the right half for volume, drag sideways to seek, pinch to zoom, hold for 2× speed, double-tap sides to skip. Also: control lock, open stream links, frame step (, and .), sound presets, warm night tone, accent colours, video info.
Queue, drag-and-drop, folders, resume playback, speed 0.25–3×, A–B loop, loop/shuffle, subtitles (.srt/.vtt) with delay and size, brightness/contrast/saturation, volume boost to 300%, bass/treble, mirror, aspect modes, picture-in-picture, screenshot, sleep timer, double-tap seek, keyboard shortcuts, lock-screen controls.
Codecs depend on the device's browser engine (MP4/H.264, WebM and most MP3/AAC work; some MKV audio/video tracks may not).
