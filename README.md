# EchoCipher

**Send pictures through sound, and seal voice messages inside encrypted noise.**

EchoCipher is a single-file web app with two tools — an SSTV picture radio and an audio cipher. It runs entirely in your browser: no server, no uploads, no accounts. Open it once and it works fully offline.

🌐 **Live:** https://ettayea01.github.io/echocipher/

## The tools

### 📻 SSTV Picture Radio
Slow-scan television: a picture becomes sound, one line at a time.

- **Transmit** — pick a photo (or use the built-in test pattern). It is resized to 320 × 240 and sung out as **Robot36** tones (VIS code **8**, ≈ 37.7 seconds). Play it through your speaker, or download the tones as a WAV file.
- **Receive** — hold your phone near a speaker and press **Listen** (microphone), or decode an existing SSTV audio file. The picture paints itself line by line on the screen, then can be saved as a PNG.

Every pixel is a tone between 1500 Hz (black) and 2300 Hz (white), with a 1200 Hz sync pulse per line — sturdy analogue tones that survive noisy rooms and cheap speakers.

### 🔐 Audio Cipher
Seal a voice message so only your password can open it.

- **Encrypt** — record your voice (or load an audio file), set a password, and EchoCipher produces a *coded sound*: a WAV of pure noise. Download it and send it **as a file** (e.g. as a document in your chat app).
- **Decrypt** — load a coded WAV, type the same password, and hear the original voice again. Wrong password or a single damaged byte → decryption refuses, by design.

> ⚠️ Send the coded sound as a file, not speaker-to-microphone. Room noise and speaker distortion corrupt encrypted data, and one damaged byte makes the whole message undecryptable. (SSTV tones are built for that journey — encrypted data is not.)

## Tech

- **SSTV:** Robot36 mode, VIS header code 8, WebAudio API encode/decode, microphone via `getUserMedia`, canvas rendering.
- **Cipher:** AES-256-GCM authenticated encryption (WebCrypto), key derived with PBKDF2 — 100,000 rounds of SHA-256 — with a fresh random salt and IV per message, stored inside the coded WAV itself.
- **App:** one self-contained `index.html` — zero dependencies, zero external requests, works offline by just opening the file.

## Privacy

Everything happens locally on your device. Pictures, voice recordings and passwords are never uploaded anywhere — there is no server to upload them to.

## Use it

Just open the live link above, or download `index.html` and open it in any modern browser. On a phone you can "Add to Home Screen" for an app-like shortcut.
