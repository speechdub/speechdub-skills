---
name: speechdub-text-to-speech
description: Generate spoken audio with Speechdub preset voices when the user wants text read aloud, a voice preview, or audio output from their content.
---

# Speechdub text-to-speech

Use when the user wants **audio** or **read aloud** via Speechdub voices, not only silent text in chat.

## Tools

- `speechdub_list_voices` — optional `gender` filter (`male` | `female`).
- `speechdub_get_voice` — metadata for one `voice_id` (presets like `F1`, `M3`).
- `speechdub_synthesize_speech` — required `input` (max 5000 chars) and `voice_id`; optional `language`, `audio_format` (`wav` | `mp3`), `include_audio_data`.

## Workflow

1. Always call `speechdub_list_voices` (or `speechdub_get_voice` if they named a preset) **before** synthesis unless a valid `voice_id` is already confirmed.
2. Pick a voice that matches the user’s language or preference; say which voice you chose.
3. Split long text into chunks under 5000 characters if needed; synthesize per chunk.
4. Report billing context briefly: synthesis uses the user’s Speechdub credit wallet (same as the web app). Do not quote API keys.
5. If `include_audio_data` is false or omitted, describe the result (duration, format, request id) per tool output; follow the client’s rules for playing or attaching audio.

## Boundaries

- Do not create or delete library documents unless the user also asked for library changes.
- Prefer synthesis on user-supplied or document text they explicitly want heard; do not synthesize huge documents without narrowing scope.
