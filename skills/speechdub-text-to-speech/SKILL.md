---
name: speechdub-text-to-speech
description: Generate spoken audio with Speechdub preset voices when the user wants text read aloud, a voice preview, or audio output from their content.
---

# Speechdub text-to-speech

Use when the user wants **audio** or **read aloud** via Speechdub voices, not only silent text in chat.

## Tools

- `speechdub_get_account` — plan and wallet (`wallet_cents`, `display_credits`). Call before synthesis to avoid `payment_required`.
- `speechdub_list_voices` — optional `gender` filter (`male` | `female`).
- `speechdub_get_voice` — metadata for one `voice_id`. Ids are presets `F1`–`F5` and `M1`–`M5` (for example F1, M3). Display names such as Sophie are not valid ids.
- `speechdub_synthesize_speech` — required `input` (max 5000 chars) and `voice_id`; optional `language` (ISO 639-1), `audio_format` (`wav` | `mp3`), `idempotency_key`, `include_audio_data`.

MCP synthesis is non-streaming and capped at 5000 characters. For streaming or inputs up to 20,000 characters, the user (or a REST client) must call `POST https://api.speechdub.com/v1/audio/stream`. Do not invent an MCP streaming tool.

## Workflow

1. Call `speechdub_get_account` and mention remaining display credits if the balance is low.
2. Always call `speechdub_list_voices` (or `speechdub_get_voice` if they named a preset id) **before** synthesis unless a valid `voice_id` such as `F1` is already confirmed. If they name a person (Sophie, Nathan), look up the matching `id` from `speechdub_list_voices` — never pass the display name as `voice_id`.
3. Pick a voice that matches the user’s language or preference; say which **id** you chose.
4. Split long text into chunks under 5000 characters if needed; synthesize per chunk. Use `idempotency_key` when retrying the same chunk after a timeout.
5. Report billing context briefly: synthesis uses the user’s Speechdub credit wallet (same as the web app). Do not quote API keys.
6. If `include_audio_data` is false or omitted, describe the result (duration, format, request id) per tool output; follow the client’s rules for playing or attaching audio.

## Boundaries

- Do not create or delete library documents unless the user also asked for library changes.
- Prefer synthesis on user-supplied or document text they explicitly want heard; do not synthesize huge documents without narrowing scope.
