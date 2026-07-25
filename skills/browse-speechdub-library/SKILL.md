---
name: browse-speechdub-library
description: List or open documents in the user's Speechdub library when they want to see saved titles, search by name, or read full document text.
---

# Browse Speechdub library

Use this skill when the user asks to see, search, or read documents they already saved in Speechdub (not when they only want new text pasted in chat).

## Tools

- `speechdub_list_documents` — paginated list; optional `query` for title search, `limit` (max 100), `cursor`, `include_archived`.
- `speechdub_get_document` — full title, language, and body for one `document_id` (UUID).

## Workflow

1. Prefer `speechdub_list_documents` when the user does not give an id. Use a reasonable `limit` (e.g. 10–20) unless they ask for more.
2. If they name a document, pass `query` on list, then `speechdub_get_document` on the best match.
3. If they provide a UUID, call `speechdub_get_document` directly.
4. Summarize titles and languages clearly; when they ask for content, quote or summarize the returned text without inventing library items.

## Boundaries

- Read-only: do not create, update, delete, or synthesize unless the user clearly asks for those actions (use other skills).
- Never expose API keys or raw OAuth tokens. The MCP connection is already authenticated as the user.
