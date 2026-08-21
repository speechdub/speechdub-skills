---
name: edit-speechdub-document
description: Rename or update text and language of an existing Speechdub document the user owns, archive or unarchive it, or permanently delete a document when they explicitly request removal.
---

# Edit or remove Speechdub documents

Use when the user wants to **change** a saved document (title, body, language), **archive** or **unarchive** one, or **delete** one they identify by name or id.

## Tools

- `speechdub_list_documents` / `speechdub_get_document` — resolve `document_id` when the user only gives a title or vague reference.
- `speechdub_update_document` — `document_id` plus any of `title`, `text`, `language`, `is_archived`.
- `speechdub_delete_document` — `document_id` only; **permanent**.

## Workflow

1. Resolve the target document id (list + get if needed). Do not guess UUIDs.
2. For renames or content edits, use `speechdub_update_document` with only the fields that should change.
3. For archive / hide from the default library list, set `is_archived` to true. To restore, set `is_archived` to false. Do not delete for archive requests.
4. For deletion, confirm the user intent when ambiguous (title + id). Then call `speechdub_delete_document` once.
5. After delete, state clearly that the document was removed and cannot be restored via the API.

## Boundaries

- `speechdub_delete_document` is destructive; do not use it for “archive” or “clear chat” requests unless they mean delete from Speechdub.
- Do not create new documents here (use import-to-speechdub).
