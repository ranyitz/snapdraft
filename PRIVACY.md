# Snapdraft Privacy Policy

**Last updated: July 3, 2026**

Snapdraft is a local-first writing assistant for macOS. The short version: your writing stays on your Mac unless you explicitly send it somewhere. Snapdraft has no servers of its own, and your drafts are never sent to us.

This page explains exactly what runs locally, what leaves your device and when, and how to control all of it.

## What runs entirely on your Mac

- **Rewriting.** Built-in rewrite modes run locally through `llama.cpp` using the Qwen3-4B model. Your text is processed on-device.
- **Dictation.** Transcription runs locally through `whisper.cpp` using the `base.en` model. Audio is recorded to a temporary file only while you are dictating, transcribed on your Mac, and never uploaded.
- **Draft history.** Drafts are stored locally on your Mac (see "Local storage" below). History retention is configurable, and you can disable or clear it at any time.

## What leaves your device, and when

Snapdraft makes network requests only in these cases:

### 1. Model downloads

The first time you use local rewriting or dictation, Snapdraft downloads the required model files from Hugging Face over HTTPS and verifies them by checksum. These are ordinary file downloads — none of your text or audio is included in the request.

### 2. ChatGPT integration (optional, off unless you connect it)

You can optionally connect your own ChatGPT account and use ChatGPT-powered rewrite modes. When you do:

- The draft text you are rewriting, together with the rewrite-mode prompt, is sent to OpenAI (the chatgpt.com backend API) under **your own account** and is handled according to [OpenAI's privacy policy](https://openai.com/privacy).
- Nothing else is sent — not your draft history, clipboard, or dictation transcripts.
- Your OAuth tokens are stored locally on your Mac (in `~/Library/Application Support/Snapdraft/chatgpt-codex/auth.json`, readable only by your user account). Snapdraft never sees your ChatGPT password.

If you never connect a ChatGPT account, nothing you write ever leaves your Mac as part of rewriting.

### 3. Usage analytics and crash reports (on by default — here's how to turn it off)

Snapdraft sends anonymous usage analytics and crash reports **by default**. You can turn this off at any time in **Settings → Usage Metrics** (switch off "Share anonymous usage metrics"), and Snapdraft works exactly the same without it.

What this includes:

- **Usage analytics (PostHog, hosted at us.i.posthog.com).** Events describe feature usage (for example, "a rewrite was run") and are metadata only. Every event passes through a sanitizer that strips draft text, transcripts, clipboard contents, prompts, file paths, and tokens before anything is sent. You are identified by a random per-install ID that is not tied to your name, email, or any account.
- **Crash and error reports (Sentry).** Crash reports are scrubbed of personal information: no email, username, IP address, or location is sent, and the user identifier is a one-way (SHA-256) hash.

### 4. Update checks

Snapdraft uses [Sparkle](https://sparkle-project.org/) to check for updates against an appcast file hosted on this repository's GitHub Pages site. These are standard update-check requests and contain none of your content.

## What Snapdraft does not do

- No Snapdraft servers — we never receive your drafts, transcripts, or clipboard.
- No clipboard monitoring. Importing from the clipboard happens only when you explicitly press `Cmd + Shift + V`.
- No keystroke capture. Global shortcuts are registered through the standard macOS hotkey APIs, which tell Snapdraft only when its own shortcuts are pressed.
- No accounts, no sign-up, no ads, no selling of data.

## Local storage and how to clear it

Everything Snapdraft stores lives on your Mac:

- **Draft history:** `~/Library/Application Support/Snapdraft/History/` — stored as plaintext JSON. You can set the retention period, disable history, or clear it from within the app. Deleting the folder also removes it.
- **ChatGPT credentials (if connected):** `~/Library/Application Support/Snapdraft/chatgpt-codex/auth.json` — disconnect in the app or delete the file to remove them.
- **Downloaded models:** cached locally so they only download once.

Uninstalling Snapdraft and deleting `~/Library/Application Support/Snapdraft/` removes all of its data.

Note that draft history is plaintext on disk — it is protected by your macOS user account and any disk encryption (FileVault) you have enabled, like other documents on your Mac.

## Permissions

- **Microphone:** requested via the standard macOS permission prompt, and only used when you start dictation (`Ctrl + M`). You can revoke it any time in System Settings → Privacy & Security → Microphone.

## Third-party services

| Service | Used for | When |
| --- | --- | --- |
| Hugging Face | Downloading local AI models | First use of rewriting or dictation |
| OpenAI (ChatGPT) | Optional ChatGPT rewrite modes | Only if you connect your account and pick a ChatGPT mode |
| PostHog | Anonymous usage analytics | On by default; can be turned off in Settings |
| Sentry | Crash and error reports (scrubbed) | On by default; can be turned off in Settings |
| GitHub | Hosting downloads and update checks | On update checks and downloads |

## Changes to this policy

If Snapdraft's data practices change, this document will be updated and the date at the top revised. Meaningful changes will be called out in the release notes.

## Contact

Questions or concerns? Open an issue at [github.com/ranyitz/snapdraft/issues](https://github.com/ranyitz/snapdraft/issues), or contact Ran ([@ranyitz](https://github.com/ranyitz)) at ranyitz@gmail.com.
