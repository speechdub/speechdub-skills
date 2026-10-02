---
name: browse-speechdub-library
description: List or open documents in the user's Speechdub library when they want saved titles, a title search, or the full text of a document they already saved.
---

# Browse Speechdub library

Use this skill when the user asks to see, search, or read documents they already saved in Speechdub.

The user's instructions take precedence over this skill. If they conflict, follow the user.

## Tools

- `speechdub_list_documents`: paginated list. Optional `query` for title search, `limit` (1-100), `cursor`, `include_archived`.
- `speechdub_get_document`: title, language, and body for one `document_id` (UUID).

## Workflow

1. When the user does not give an id, call `speechdub_list_documents`. Use a `limit` of 10–20 unless they ask for more.
2. If they name a document, pass `query`, then call `speechdub_get_document` on the best match.
3. If they provide a UUID, call `speechdub_get_document` directly.
4. If they ask for archived items, set `include_archived` to true.
5. Report titles and languages from the tool result. When they ask for content, quote or summarize that text. Do not invent library items.

## Boundaries

- Do not create, update, delete, or synthesize unless the user also asks for that.
- Do not reveal authentication material. The connection is already signed in as the user.
