# Phonebook Agent Instructions

## What This Is

Phonebook is a local, human-readable relationship database operated through natural language. It stores contact details and personal context so users can find people, understand connections, and maintain relationships. The file system is the database, command-line search is retrieval, and you are the interface.

`phonebook.jsonl` contains the data: one person per line as a valid JSON object. There is no required primary key; identify people from names, contact details, and context.

## Rules

- Preserve unknown fields and existing information unless explicitly asked to remove it.
- Keep each record on one line and validate the entire file after edits.
- Do not invent missing facts. Store useful unstructured context in `notes`.
- Use ISO 8601 dates (`YYYY-MM-DD`); birthdays may omit the year (`MM-DD`).
- New fields are allowed when needed; document them here.

## Fields

All fields are optional.

- `names`: string[] — names, aliases, and usernames
- `emails`: string[]
- `phones`: string[]
- `socials`: object[] — `{platform, handle?, url?}`
- `birthday`: string
- `organizations`: object[] — `{name, role?, start?, end?}`
- `schools`: object[] — `{name, program?, start?, end?}`
- `locations`: string[]
- `relationships`: object[] — `{person, type, note?}`
- `interests`: string[]
- `notes`: string[]
- `last_contact`: string
- `reminders`: object[] — `{date?, text}`

Prefer arrays for repeatable values and omit empty fields.
