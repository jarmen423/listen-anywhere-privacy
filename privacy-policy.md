# Privacy Policy — Listen Anywhere

**Last updated:** 4 October 2026  
**Product:** Listen Anywhere — Web to Speech (Chrome extension)

This policy describes how the Listen Anywhere Chrome extension (“the extension”) handles information on your device. The extension is **bring-your-own-key (BYOK)**. The developer does not run a Listen Anywhere cloud service, does not create user accounts, and does not receive your page text, audio, or API keys.

## What the extension does

The extension captures text from a web page or a selection you choose, optionally rewrites that text for spoken delivery using an LLM you configure, splits it into chunks, and sends those chunks to a text-to-speech (TTS) provider you configure. Audio is played in the browser (an offscreen document) and can be saved to a file on your computer.

## What stays on your device

The following stay in this browser profile on this computer unless you copy them out yourself:

- **API keys** you paste in Settings (`chrome.storage.local`). They are not written to `chrome.storage.sync`, not logged by the extension, and not sent to the developer.
- **Settings** (chosen TTS/LLM providers, voice, playback speed, crawl defaults).
- **Job state** for the current listen (title, URL, status, chunk text) in `chrome.storage.session`. This is cleared when the browser session ends.
- **Downloaded audio files** you explicitly save with Download audio (they are written via Chrome’s download UI to a location you pick).
- **Temporary audio** held in memory / blob URLs inside the offscreen player while a job is playing.

Uninstalling the extension or using **Clear all settings & keys** in Settings removes the extension’s `chrome.storage` data. Downloaded files on disk are not deleted.

## What is sent off the device — and to whom

Nothing is sent to a Listen Anywhere server. There isn’t one.

### 1. Page or selection text → your TTS provider (required to listen)

When you start a listen job, captured text is sent to **the TTS provider you selected**, using **the API key you pasted for that provider**. That is how speech is synthesized.

TTS providers the extension can call (only if you choose them and provide a key):

| You select | Request goes to |
|---|---|
| OpenAI | `https://api.openai.com/` |
| ElevenLabs | `https://api.elevenlabs.io/` |
| Gemini | `https://generativelanguage.googleapis.com/` |
| xAI Grok Voice | `https://api.x.ai/` |
| Fish Audio | `https://api.fish.audio/` |
| OpenRouter | `https://openrouter.ai/` |
| Mistral Voxtral | `https://api.mistral.ai/` |

Those companies process the text (and return audio) under **their** terms and privacy policies, not ours. We do not see the request.

### 2. Page or selection text → your LLM enhancer (optional)

If you enable **LLM Enhancer**, paste an enhancer API key, and start a listen job, the captured text is sent to **that LLM provider** first so it can rewrite the script for speech. If you leave the enhancer key empty, captured text is not sent to an LLM; it is sent only to TTS (raw).

Enhancer providers the extension can call (only if you choose them and provide a key):

| You select | Request goes to |
|---|---|
| OpenAI | `https://api.openai.com/` |
| Gemini | `https://generativelanguage.googleapis.com/` |
| OpenRouter | `https://openrouter.ai/` |
| xAI | `https://api.x.ai/` |
| Cerebras | `https://api.cerebras.ai/` |
| NVIDIA | `https://integrate.api.nvidia.com/` |

If enhancement fails and **If enhancement fails, read the raw extracted text** is on (the default), the extension falls back to sending the raw capture to TTS instead of stopping.

### 3. Voice lists and model lists (only when you click Sync / Fetch)

- **Sync voices** calls the selected TTS provider’s voices endpoint with your TTS key (ElevenLabs, xAI, Fish Audio, Mistral).
- **Fetch models** calls the selected enhancer provider’s models endpoint with your enhancer key.

### 4. Audio bytes

TTS responses (MP3/WAV/PCM) are received by the offscreen player in this browser. They are not uploaded to the developer. If you click Download audio, Chrome saves a local file.

### 5. What we do not send

- No analytics, crash telemetry, or advertising IDs.
- No automatic sync of keys to other devices.
- `chrome://` pages, the Chrome Web Store, and PDFs are not read (the UI disables listen there).

## Host permission (`<all_urls>`)

The extension declares `<all_urls>` so it can:

1. Extract readable text on the http(s) page **you asked it to read**.
2. Call the provider APIs above from extension pages (service worker, offscreen player, Settings) without being blocked by the web page’s CORS policy.

It does not use that permission to scrape the web in the background or to send browsing history to a server.

## Notifications, downloads, and other Chrome permissions

- **Notifications:** optional local desktop notices when a job finishes or errors; content is the job title/error, not sent to us.
- **Downloads:** only when you click Download audio.
- **Tabs / scripting / contextMenus / offscreen / alarms / storage / activeTab:** used locally to run the listen pipeline described above.

## Children

The extension is not directed at children. Do not paste a child’s personal data into a page and then send that page to a third-party speech API.

## Changes

If the data practices change (for example a first-party server is added), this policy must be updated **before** that version is published, and the Chrome Web Store privacy fields must be updated to match.

## Contact

Use the support URL listed on the Chrome Web Store item. The publisher of the store listing is responsible for this policy once the item is published.
