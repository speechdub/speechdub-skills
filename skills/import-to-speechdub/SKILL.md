---
name: import-to-speechdub
description: Save new text into the user's Speechdub library when they want a document created from pasted notes, an article, or other text they will listen to later.
---

# Import text into Speechdub

Use when the user wants to add content to their Speechdub library. Do not use it only to read text in chat.

The user's instructions take precedence over this skill. If they conflict, follow the user.

## Tool

- `speechdub_create_document`: required `text` (max 500,000 characters). Optional `title` (max 512 characters), `language` (ISO 639-1, such as `en` or `fr`), `idempotency_key` for a safe retry of the same create.

## Workflow

1. Use the text the user pasted or attached as `text`.
2. If they did not give a title, choose a short plain-text title. Do not put markdown in the title.
3. Set `language` when they name a language or the source language is obvious. Use an ISO 639-1 code, not a regional tag such as `fr-FR`. Otherwise omit `language`.
4. Call `speechdub_create_document` once per document they asked for.
5. Confirm with the returned id, title, and language.

## Boundaries

- Do not delete or overwrite an existing document in this skill.
- Do not synthesize audio unless they also ask to hear it.
