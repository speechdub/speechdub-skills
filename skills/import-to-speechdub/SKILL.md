---
name: import-to-speechdub
description: Save new text into the user's Speechdub document library from pasted content, notes, or articles they want to listen to later in the app.
---

# Import text into Speechdub

Use when the user wants to **add** content to their Speechdub library (import, save, create a document), not merely read it in chat.

## Tool

- `speechdub_create_document` — required `text` (max 500,000 characters); optional `title` (max 512 characters), `language` (ISO 639-1 code such as `en` or `fr`, 2–8 characters), `idempotency_key` for safe retries.

## Workflow

1. Collect the text to import. If the user attached or pasted content, use that as `text`.
2. Choose a short, descriptive `title` if they did not specify one (plain text, no markdown formatting in the title).
3. Set `language` when the user specifies it or when the source language is obvious; pass an ISO 639-1 code, not a regional tag like `fr-FR`. Otherwise omit and let Speechdub detect when possible.
4. Call `speechdub_create_document` once per distinct document they asked for.
5. Confirm success with returned `document_id`, title, and language. Mention that creating documents uses their Speechdub document quota (not the same as speech credits).

## Boundaries

- Do not delete or overwrite existing documents in this skill.
- Do not call speech synthesis unless they also ask to hear audio (use the text-to-speech skill).
