---
name: speechdub-text-to-speech
description: Generate spoken audio with Speechdub preset voices when the user wants text read aloud, a voice preview, or audio from their own content.
---

# Speechdub text-to-speech

Use when the user wants audio or text read aloud with Speechdub voices.

The user's instructions take precedence over this skill. If they conflict, follow the user.

## Tools

- `speechdub_list_voices`: optional `gender` filter (`male` or `female`).
- `speechdub_get_voice`: metadata for one `voice_id`. Ids are presets `F1`-`F5` and `M1`-`M5`. Display names are not valid ids.
- `speechdub_synthesize_speech`: required `input` (max 5000 characters) and `voice_id`. Optional `language` (ISO 639-1), `audio_format` (`wav` or `mp3`), `idempotency_key`, `include_audio_data`.

## Workflow

1. Before synthesis, call `speechdub_list_voices`, or `speechdub_get_voice` if they named a preset id, unless a valid `voice_id` such as `F1` is already confirmed. If they name a person, look up the matching `id` from `speechdub_list_voices`. Never pass a display name as `voice_id`.
2. Tell the user which id you chose.
3. If the text is longer than 5000 characters and they want all of it heard, split it into chunks under 5000 characters and synthesize each chunk. Use `idempotency_key` when retrying the same chunk after a timeout.
4. If speech generation is unavailable for the account, say so and stop. Do not start a checkout or an upgrade.
5. If `include_audio_data` is false or omitted, describe the result from the tool output (duration and format) and follow the client rules for playing or attaching audio.

## Boundaries

- Do not create or delete library documents unless the user also asked for that.
- Do not synthesize a long document unless they asked to hear that scope.
