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


### v2.7.58
- **Interpreter mode**: turn-based conversation translation with a three-tier
  cascade (van Scout, Groq cloud, on-device ML Kit — always available offline)
- **Laughing & emotions engine** with a one-tap self-test; **Dual Voice** mode
- **BCPA9 Bluetooth fix**: Scout reuses the phone's existing stereo connection
  instead of failing; new routed-device diagnostic shows where Scout's voice
  actually plays
- **Always listen** over the lock screen (VAD-gated) with diagnostics
- **Mirror + Cast to Shield**, **phone theft-recovery** layer, and a
  screen-aware **Shield control** screen (Outpost v2, pairing code from the TV)
- Removed YouTube music search; added a selectable Edge voice (Kokoro stays
  the default voice); name sync with the laptop Scout
- Bug-hunt fixes: interpreter on-device tier initialization, theft-PIN
  per-device salt, Bluetooth permission guards, translation timeouts
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
- **v1.6** — Screen-aware control: authenticated /v2 API (pairing code shown
  on the TV), UI-tree reading + tap-by-element, screenshots, gestures,
  guided setup checklist with on-TV deep links, mDNS discovery, and
  Universal Outpost device profiles (Shield / Google TV / Fire TV tiers)

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

## v2.7.39 (2026-10-12)
- Clean-rebuild recovery: v2.7.36-38 crashed on startup due to stale Gradle build state, not app code. Rebuilt from scratch (fresh daemon, clean task) — confirmed working on device.
- Offline text classifier remains disabled as a precaution; all input routes directly to the LLM until the MediaPipe model path is properly fixed with diagnostics.

## v2.7.68 (2026-10-19) — laptop-standard voice upgrade
- **Laugh bank replaces fragment-pulse emotions.** Chuckles, laughs, and sighs are now served from a bank of performed renders in the selected voice: the standard voice (am_adam) carries the same owner-approved 55-entry converted bank as laptop Scout; Duo's June (af_heart) carries a founding 12-entry bank from the same Chatterbox-Turbo pipeline, conditioned on a Kokoro af_heart reference. Fresh draw every time, never the same entry twice in a row, intensity matched (chuckle/laugh/full). Voices without a bank keep the v2.7.63 shaped synthesis and are labeled as such in Settings and the self-test.
- **Serious-context gate (code, not prompt).** A van intruder alert opens a 10-minute serious window: playful emotion requests are refused in words, the self-test announces skips, and the audio path will not render a gated sound. Sigh/empathy are never gated.
- **Pipelined speech.** Queued speech now chunks at ~240 characters at sentence boundaries so synthesis runs a chunk ahead of playback; short replies still speak as one continuous chunk.
- **Speakable rule:** a standalone "911" is spoken "nine one one" (1911, phone numbers, and longer digit strings untouched).
- **Self-test** (Settings → Interpreter, emotions & audio → "Hear the emotion self-test") plays the bank samples in the selected voice and ends with two clearly-announced breath auditions.
- Engine unchanged (int8 Kokoro) after evaluation: the fp32 pack (~340 MB vs the int8 archive's ~132 MB) risks real-time factor on phone CPUs; the upgrade is production, not precision.
- 154 unit tests green, incl. 22 new (bank picking/no-repeat/per-voice routing, gate policy, chunking, 911 rule).

## v2.7.69 (2026-10-19)

- **June's laugh bank is now the full mirrored bank of 55** — every male slot (27 chuckles / 12 laughs / 16 full laughs) has a June-voiced counterpart, replacing her founding set of 12 from v2.7.68. Same source bank Ilona v0.4.0 ships (Chatterbox-Turbo conditioned on af_heart; owner-approved: founding takes by ear/word, the rest under his blanket waiver; the two rejected founding samples are not in the bank).
- Catalog mirrors the male bank slot-for-slot; serving rules unchanged (fresh draw, never back-to-back, intensity fit). Male bank, sighs, breath auditions, EmotionGate, and the labeled shaped fallback for unbanked voices are unchanged.
- 154 unit tests green.

## v2.7.71 (2026-10-20)

- **Mic coexistence fix.** While Scout merely listened for "Hey Scout", he held the phone in call mode (MODE_IN_COMMUNICATION + a voice-communication capture) around the clock — and Android's concurrent-capture policy silences other apps' microphones in that state (proven by ADB dumpsys audio on the owner's phone: Ilona's capture flipped to "silenced" the moment Scout seized call mode). Wake-word listening and the mic self-test now use a voice-recognition capture that never touches call mode, so other voice apps keep their mics while Scout listens. Active conversation sessions keep call mode + echo cancellation exactly as before, released when the session ends. The wake-word diagnostics card now shows the live mic path in plain words.
- **Audited laugh banks.** June's bank now carries the owner's by-ear re-audit (2026-10-20): 9 repaired slots (22, 27, 28, 30, 33, 40, 42, 45, 47 — dead-air cores trimmed; trailing/second lines cut on slots 22, 28 and 45), and the male bank's slot 5 is repaired the same way. All other 100 entries unchanged; files verified byte-exact against the approved audit masters.
- 170 unit tests green (incl. LaughBankTest 10/10).

## v2.7.74 (2026-10-23) — crash fix

- **Native crash fixed (voice engine).** On the morning of Oct 23, v2.7.73 died twice in five minutes: a voice-synthesis call was still running inside the on-device speech engine while the engine was being shut down and rebuilt, and the freed engine crashed the process. Engine shutdown now waits for any in-flight synthesis, synthesis re-checks the engine is alive before starting, and the speech-recognition/VAD objects follow the same ownership discipline — no native speech object is ever used after release or released twice.
- **Worker crashes can no longer kill the app silently.** All four voice-engine workers now report unexpected failures into the crash-report store instead of taking the whole process down, and the one un-owned array the speech engine hands back is read defensively everywhere.
- **Crash reporting actually captures.** v2.7.73's two crashes left no report anywhere — the in-app list was empty and no Downloads file was written. The reporter no longer swallows its own failures (it logs and falls back to the legacy crash file), it checks its store is writable at startup, the Settings "Save a test report" button now exercises the full pipeline (list entry + Downloads file), and on the next launch Scout sweeps the system exit records so even a native crash that no in-app handler could catch becomes a report after the fact.
- **Follow-up speech cut fixed.** A stop command racing a brand-new reply could drain the new reply's first chunks; speech queueing is now atomic against stop.
- 183 unit tests green (177 + 6 new pins for the exit sweep). The R8 mapping for this build is retained with the release records so any future crash retraces exactly.

## v2.7.75 (2026-10-23) — Android Auto Route 1: real navigation + Spotify that plays

- **Navigation reaches the dash.** In drive mode, "navigate to X" / "drive to X" / "directions to X" used to open a Google Maps search on the phone — and Android Auto has nothing to project from a search, so the BCPA9 never showed it. Drive mode now starts real turn-by-turn navigation on the phone, through the same navigation path the rest of the app uses; Android Auto mirrors the phone's active navigation onto the dash. "Show me X on the map" keeps the old search for just looking at a place. (Place names in navigation links are also properly encoded now — multi-word destinations can't break the link.)
- **"Play X in Spotify" actually plays it.** Scout now asks Spotify's own player session to play the request — the channel Android Auto itself uses — launching Spotify first if it isn't running. He only says "playing" when Spotify's session confirms it is; if Spotify is still loading, paused, or never starts, he says that instead. The old search page remains as the last-resort fallback, with its honest "tap a result to play it" wording unchanged.
- **One new permission — yours to grant once.** Reaching Spotify's player needs notification access (Settings → Notifications → Device & app notifications → Scout). Scout reads no notification content; the access exists only because that is how Android lets one app reach another app's media session. Without it, the command explains itself and opens the exact Settings screen. The wake-word diagnostics card (Settings) now shows the grant state, plus what the last Spotify request did — which step ran and what Spotify reported — so one screenshot proves how it behaves in the van.
- Bare "play X" (no app named) is unchanged, as are all other voice commands, the laptop link, and saved settings.
- 206 unit tests green (183 + 23 new pins: drive-mode navigation routing, the Spotify ladder's rung choices and state reading, and the rule that "playing" is never claimed without a playing state). The R8 mapping for this build is retained with the release records.

## v2.7.76 (2026-10-23) — BCPA9 music routing: music commands go to Spotify in the van

- **While your phone is Bluetooth-connected to the BCPA9, music commands bind to Spotify** as the car's music source (owner's call, 2026-10-23). Scout checks the live Bluetooth A2DP connection for the stereo by name; no new permission — the check rides the Bluetooth access Scout already has.
- **"Open Spotify"** makes Spotify the car's source: with a Spotify session live, a paused one resumes — and Scout only says "playing" once Spotify's session confirms it (the same honesty rule as the v2.7.75 ladder). No session yet, he launches Spotify so it comes up on the radio. If Spotify isn't openable, he says so instead of pretending.
- **"Play <song or artist>"** (no app named) now runs the Spotify session ladder while connected, instead of opening a search in your default music app. **"Play X in Spotify"** works exactly as in v2.7.75, connected or not.
- **Bare transport words act on Spotify's player**: "pause", "play"/"resume", "next", "previous", "stop the music" go to Spotify's own controls. When Spotify has no session to act on, the command falls back to the ordinary media keys — never a dead end.
- **Away from the van, nothing changes**: with the BCPA9 not connected, every music command behaves exactly as in v2.7.75, default music app and all.
- Each music command's routing decision — was the BCPA9 connected, where did the command go — is recorded on the wake-word diagnostics card next to the Spotify rows, so one screenshot from the van proves the behavior.
- 220 unit tests green (206 + 14 new pins: the command classification matrix, the connected/disconnected routing table, and the confirmation-wording honesty rules). The R8 mapping for this build is retained with the release records.

## v2.7.77 (2026-10-23) — voice fix: replies are heard again + sealed crash reports recovered

- **The silent-reply bug is fixed.** On Oct 23, Scout generated each reply in full — then an internal "flush" stop, landing the moment generation finished, threw the still-unplayed audio away (proven in the phone's own logs: replies of ~3 seconds of speech discarded 19–124 ms after synthesis, three times in a row). Speech is now tagged by generation: a flush may only discard speech older than the newest request, so a reply can never flush itself; playback finishing is measured by the audio track's actual playback position instead of a timer; and the track buffer is a small streaming window instead of one whole reply, so there is no buffer full of unheard speech left to throw away. The diagnostics "cut off while playing" counter now counts only a flush that genuinely cut older speech — normal replies keep it at 0. (Saying "stop" still stops everything, and a newer reply still supersedes an older one.)
- **The two v2.7.73 crashes are recovered.** The Oct 23 exit sweep sealed them instead of reporting them: its "already swept" marker jumped past every exit the system returned — including the install kill, which isn't a crash — and later runs only looked at exits newer than the marker. Recording is now governed by the report store itself (any past crash the store doesn't already have gets recorded, however old), the marker advances only over exits a run actually recorded or already had, the sweep reads more exit history, and it logs what it found on every run. After this build is installed and opened once, the 09:01 and 09:04 crash reports from Oct 23 appear under Settings → Crash & error reports, with copies in Downloads.
- No new permissions, no settings changes. Everything from v2.7.74–v2.7.76 is included.
- 232 unit tests green (220 + 12 new pins: the flush-at-generation-complete scenario, a two-reply sequence keeping the cut-off counter at 0, interruption still cutting, and the sealed-crash recovery scenario — install kill newest, both crashes recorded). The R8 mapping for this build is retained with the release records.
