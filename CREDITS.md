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

### v2.7.20
- Camera and screen-vision toggles in the normal chat bar (were
  hands-free-only before)
- In-app update checks: update banner plus a Settings check row, reading
  version.json from the GitHub repo

### v2.7.21
- Settings back navigation hardened: system back from the Memory and User
  Guide sub-screens now returns to Settings (used to exit the app), plus a
  backup system-back path at the chat level so Settings can never strand
  you
- "Set up phone locking" no longer fails silently: errors are reported
  on screen with a fallback to system security settings, and the button
  state refreshes when you return from the system setup screen
- "Save my location now" now asks for location permission when missing
  and always shows what happened ("Location saved." or the reason it
  couldn't)

### v2.7.22
- Killed the ghost "Back to simple settings" text at the top of Settings:
  the Simple/Advanced toggle is now a permanent button in the top bar,
  and the old footer button that kept rendering as jumbled letters is gone
- Manual "Check for updates" now bypasses the CDN cache so a just-published
  version is found on the first tap

### v2.7.23 – v2.7.29
- Settings ghost-text overdraw fixes; footer moved into Scaffold's bottomBar
  with navigation-bar insets so buttons sit above the system nav and stay tappable
- Voice-optimized persona (SCOUT_PERSONA): livelier, more human conversational wording
- In-app update checks (banner + Settings row) reading version.json

### v2.7.30
- TTS sentence-pause fix: Kokoro now synthesizes in 500-char chunks instead of
  per-sentence, removing the unnatural pauses between sentences (maxNumSentences 1→10)
- Settings space-savers: speech-recognition engine and text-to-speech engine
  selectors converted from vertical cards to dropdown menus
- "Use voice-optimized prompt" button: one-tap restore of the built-in voice-first
  persona when a stale saved prompt overrides it

### v2.7.31
- "Warming up…" indicator: the 650MB Parakeet model takes ~30s to load on first
  use — the app now shows a banner with a spinner instead of a mysteriously deaf mic
- Automatic two-way translation: ML Kit Language Identification detects the input
  language, then translates to the other side of the configured pair
- Screen-off "Hey Scout": new foreground service (microphone type) keeps the
  wake word listening with the screen off; persistent notification; "Listen with
  screen off" toggle in Settings → Wake word

### v2.7.33
- **Human-sounding TTS overhaul**: text normalization (expands "Tue." → "Tuesday",
  verbalizes numbers/dates/phone numbers, strips URLs/emojis), phonetic respelling
  for mangles names, pause engineering via punctuation, persona teaches LLM to write
  TTS-friendly text
- **Audio DSP chain**: gentle EQ (tames harshness), subtle room reverb (live feel),
  light compression (even loudness) — all via Android's built-in audio effects
- **Per-chunk rate variation** (±3%): breaks monotone drone, humans never speak at
  exactly the same rate
- **Breath sounds**: subtle inhale between paragraphs — one of the strongest "human" cues

### v2.7.32
- Settings: "Check for updates" button renamed to "Update" (the check was
  working fine — the label was just wordy)
- Shield settings: "Reinstall Outpost on the Shield" now hides itself when
  Outpost is already installed and answering (no more redundant reinstall prompt)

### v2.7.34
- **Slim build**: 67MB, down from 102MB — with zero features removed
  - R8 minification + resource shrinking (native-library keep rules)
  - 26MB MediaPipe classifier model (model.tflite) moved to
    download-after-install — ships as a release asset, cached on first run

### v2.7.35
- **"How Scout talks & listens"** settings group: strength of personality,
  how quickly Scout jumps in, and how well Scout hears you — now three
  dropdowns in one place instead of scattered sliders

### v2.7.36
- Removed the leftover duplicate End-of-speech pause / Ear sensitivity rows
  from Settings (stragglers after the v2.7.35 grouped dropdowns)
- Fixed offline classifier loading: the downloaded model.tflite is now loaded
  via ByteBuffer instead of a filesystem path MediaPipe couldn't resolve
- Classifier failure fallback: if the offline classifier is unavailable,
  Scout now falls back to the LLM instead of showing "Classification failed
  to load" — Scout always responds

### v2.7.37
- Crash fix: reverted the ByteBuffer classifier loading from v2.7.36 — it
  crashed in native code on startup. Back to the safe loading path.
- Kept the LLM fallback: if the offline classifier is unavailable, Scout
  falls back to the LLM instead of showing "Classification failed to load"

### v2.7.38
- Crash fix: disabled the offline text classifier entirely — it was crashing
  on startup in v2.7.36/37. All input now routes directly to the LLM.
- Scout responds to everything; the classifier will be re-enabled once the
  MediaPipe native crash is root-caused

---

- **v1.0** — Initial release: launch apps by package name (bypasses the
  Leanback launcher), media transport keys, volume, wake/sleep — all over
  a local HTTP API
- **v1.1** — Command contract alignment with Scout
- **v1.2 / v1.3** — Real on-TV self-test (auto-runs on resume; the old
  "listening" indicator was cosmetic)
- **v1.4** — `/apps` endpoint listing all installed apps including
  sideloaded ones; Android 11+ package-visibility fix (LEANBACK_LAUNCHER
  in the manifest `<queries>` block) so TV apps aren't hidden from the API
- **v1.5** — In-app update checks on the TV (reads version.json from the
  GitHub repo, same as Scout)

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
