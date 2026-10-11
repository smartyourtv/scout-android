# Scout + Outpost — Credits & Changelog

## Credit to the original author

**Scout** (the Android app) is a downstream fork of
[ai-assistant-android](https://github.com/vifork/ai-assistant-android) by
**ViFork** — an MIT-licensed open-source Android voice assistant with an
on-device voice pipeline (Silero VAD, Sherpa-ONNX speech recognition) and
support for any OpenAI-compatible LLM endpoint.

Everything in the original project — the voice pipeline, the app
architecture, the build setup — is ViFork's work and the work of that
project's contributors. This repository contains our heavily modified
downstream version. **Outpost** (the Android TV companion app) is our own
original code, written for this project.

Thank you, ViFork, for open-sourcing the foundation.

---

## What we changed and added — Scout (Android app)

### v2.2
- Rebranded the app as **Scout** (name, launcher label, launcher icon)
- "Hey Scout" wake word (openWakeWord) with custom trigger support
- Voice commands, expanded settings customization
- Home-screen mic widget
- Long-press "Remember that…" → saves to memory
- "Ask the Cloud" one-tap Groq escalation
- Kokoro TTS with selectable voices (Supertonic/Piper fallback work)

### v2.3
- Appearance themes (System / Light / Dark / Midnight blue)
- Room snapshot + PC intercom (app side)
- Kokoro multi-language voice models (correct American voices)

### v2.4 – v2.6
- TTS download/extraction reliability fixes, true-black background

### v2.7 — the big one
- **Outpost**: new Android TV companion app — voice control of the Shield/TV
  from the phone (launch any installed app including sideloaded ones, media
  transport, volume, wake/sleep) over the local network
- One-tap Bluetooth stereo toggle (van stereo; remembers recent devices)
- Selectable translator language pairs (models download on demand)
- Drive-mode voice commands
- God's Eye voice navigation ("Talk to It")
- Plain-language "dummy-proof" pass across the app + in-app user guide
- Anti-theft hooks (voice lock, duress phrase)

### v2.7.1 – v2.7.9
- Wake-word reliability: on-device spotter, survives backgrounding,
  VAD thread-safety, wake+command in one breath
- Wake-word **diagnostics card** (listener state, mic liveness, counters,
  one-tap self-test)
- TTS "never speaks" fixes, Outpost download reliability
- Shield app-launch voice intents

### v2.7.10
- New default persona: honest, human, sarcastic when it fits
  ("either he knows or he doesn't" — never fabricate)
- Voice-pipeline audit fixes, wake-word aliases ("pay/hay Scout")
- LLM taught about Shield/Outpost control; honesty fix — the app never
  claims an action it didn't take

### v2.7.11 – v2.7.16
- Scout↔Outpost command contract alignment (launch/media/volume/power)
- Shield command punctuation tolerance, 5s command timeout (was 600ms)
- Real Shield error messages surfaced to the user (no more generic
  "didn't answer")
- NetworkOnMainThreadException fix
- Outpost install via Shield browser method (one-tap ADB is dead on
  Android 11+)

### v2.7.17
- **Settings redesign**: Simple/Advanced two-tier settings, technical
  sliders replaced with 5 plain-word choices, 4-screen first-run wizard,
  settings search, "Reset to recommended"
- Sideloaded-app discovery (Scout side)

### v2.7.18
- Crash hardening: defensive preference loads, slider NaN/out-of-range
  coercion, guarded TTS/Bluetooth initialization
- On-device **crash reporter** (last_crash.txt, chat-screen banner,
  Settings → Advanced "Last crash report" card)

### v2.7.19
- Fixed the Settings crash (nested vertical scrolling)
- Fixed ghost/jumbled text at the top of Settings when switching
  Simple/Advanced views

---

## What we changed and added — Outpost (Android TV app, our original code)

- **v1.0** — Initial release: launch apps by package name (bypasses the
  Leanback launcher), media transport keys, volume, wake/sleep — all over
  a local HTTP API
- **v1.1** — Command contract alignment with Scout
- **v1.2 / v1.3** — Real on-TV self-test (auto-runs on resume; the old
  "listening" indicator was cosmetic)
- **v1.4** — `/apps` endpoint listing all installed apps including
  sideloaded ones; Android 11+ package-visibility fix (LEANBACK_LAUNCHER
  in the manifest `<queries>` block) so TV apps aren't hidden from the API

---

## Distribution

- Stable download URLs (these never change):
  - Scout: `https://github.com/smartyourtv/scout-android/releases/latest/download/Scout-latest.apk`
  - Outpost: `https://github.com/smartyourtv/scout-android/releases/latest/download/Outpost-latest.apk`
- Downloader (by AFTVnews) numeric codes are published with each release
  in the release notes.
- Every new build is published here as a GitHub Release; the
  `*-latest.apk` filenames stay constant so install codes and links keep
  working across versions.
