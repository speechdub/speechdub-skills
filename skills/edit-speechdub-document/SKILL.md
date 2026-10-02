---
name: edit-speechdub-document
description: Rename or update the text and language of a Speechdub document the user owns, archive or unarchive it, or permanently delete it when they explicitly ask to remove it.
---

# Edit or remove Speechdub documents

Use when the user wants to change a saved document (title, body, language), archive or unarchive it, or delete one they identify by name or id.

The user's instructions take precedence over this skill. If they conflict, follow the user.

## Tools

- `speechdub_list_documents` / `speechdub_get_document`: resolve `document_id` from a title or other reference.
- `speechdub_update_document`: `document_id` plus any of `title`, `text`, `language`, `is_archived`.
- `speechdub_delete_document`: `document_id` only. Permanent.

## Workflow

1. Resolve the document id from a list or get call. Do not guess UUIDs.
2. For a rename or content edit, call `speechdub_update_document` with only the fields that should change. Replacing `text` overwrites the current body.
3. To hide a document from the default library list, set `is_archived` to true. To restore it, set `is_archived` to false. Do not delete when they asked to archive.
4. Delete only when they explicitly ask to remove the document. If the target is ambiguous, confirm the title before calling `speechdub_delete_document` once.
5. After a delete, say the document was removed and cannot be restored through the API.

## Boundaries

- Do not use `speechdub_delete_document` for archive or for clearing the chat.
- Do not create a new document in this skill.
