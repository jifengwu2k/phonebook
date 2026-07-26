# Phonebook

## 1. Motivation

Relationships require maintenance. Small gestures—remembering a birthday, following up after a meeting, or reaching out after a long absence—can make a meaningful difference.

However, information about people is often scattered across contacts, social platforms, notes, messages, and memory. A useful phonebook should help preserve not only contact details, but also the context needed to maintain relationships.

## 2. The Problem

People data is heterogeneous and difficult to fit into a rigid contact schema:

- A person may use multiple names, aliases, or usernames.
- A person may have several email addresses or phone numbers.
- Different people use different social media and messaging platforms.
- Relevant details may include schools, employers, organizations, locations, relationships, interests, and free-form notes.
- Some information is explicit, while other useful connections must be inferred.

Traditional contact applications tend to impose a fixed schema and offer limited ways to query or transform the data.

## 3. Why an Agentic System?

A coding agent can work directly with simple files while understanding natural-language requests. This avoids the need to build a specialized interface for every possible operation.

The core model is:

> **The file system is the database, grep is retrieval, the coding agent is the harness, and `AGENTS.md` is the source code.**

The agent can:

- Search the phonebook using standard text-processing tools.
- Interpret flexible natural-language requests.
- Add, update, merge, or remove information.
- Extract structure from free-form data.
- Identify relationships that are not stored explicitly.
- Adapt as the schema evolves.

## 4. Design Principles

### Human- and agent-readable

The data should be understandable and editable without specialized software. Users should be able to inspect the phonebook with a text editor, search it with command-line tools, and version it with Git.

### Flexible rather than rigid

The system should support heterogeneous records. Fields may be optional, repeated, or extended as new needs arise.

### Local and portable

The phonebook should consist of ordinary files rather than depend on a proprietary application or hosted database.

### Natural-language interaction

Users should be able to describe what they want without learning a query language or navigating a complex interface.

### Inspectable behavior

The data model and agent instructions should be documented in `AGENTS.md`, making the system’s behavior visible and modifiable.

### Progressive structure

Information can begin as free-form notes and become more structured when useful. The system should not require every detail to be normalized in advance.

## 5. Data Design

### Storage

Use a single JSON Lines file for fast, simple searching:

```text
phonebook.jsonl
```

Each line contains one JSON object representing a person:

```json
{"names":["Alice Chen","Alice C."],"emails":["alice@example.com"],"organizations":["Example Labs"],"notes":["Met at the systems workshop in 2025."]}
```

### Identity

Records do not require a conventional primary key. A person is described through available attributes such as:

- Names and aliases
- Email addresses
- Phone numbers
- Social media accounts
- Organizations
- Schools
- Locations
- Relationships
- Notes

The agent can use combinations of these attributes to locate records and resolve identity when handling updates.

### Schema

`AGENTS.md` lists:

- All recognized fields
- The expected type of each field
- Formatting conventions
- Instructions for searching and modifying records
- Rules for adding new fields
- Guidance for handling ambiguity and duplicates

The schema is intentionally editable. As new kinds of information become useful, users can update `AGENTS.md` without migrating to a new application.

## 6. Use Cases

### Natural-language CRUD

Users can create, retrieve, update, and delete records through flexible requests:

- “Add Sam, whom I met at the conference yesterday.”
- “Update Priya’s phone number.”
- “Who do I know at Mozilla?”
- “Add a note that I should ask Jordan about their new project.”
- “Merge these two records; they refer to the same person.”
- “Remove Taylor’s old work email.”

### Recovering forgotten contact methods

A user may remember contextual information but not a person’s exact name or contact details:

- “I’m trying to remember someone from the robotics meetup who worked at Stripe.”
- “How can I contact the person I met through Lena last summer?”
- “Find the designer from Toronto I spoke with about accessibility.”

The agent can search across names, notes, organizations, locations, and relationships.

### Extracting latent networks

The system can construct groups and relationships on demand, even when those groups are not stored explicitly:

- People who attended the same school
- Former colleagues at the same organization
- People living in the same city
- Contacts connected through a mutual acquaintance
- People associated with the same event or community

For example:

- “Who in my phonebook went to Stanford?”
- “Show connections between people who have worked at the same company.”
- “Which of my contacts might know someone at Anthropic?”

### Relationship maintenance

The system can surface small but meaningful opportunities to reconnect:

- Birthday reminders
- Follow-up reminders
- Contacts not spoken to recently
- Notes about important life events
- Suggested reasons to reach out

Examples:

- “Whose birthday is coming up this month?”
- “Who have I not contacted in over a year?”
- “Remind me to ask Mia how her move went.”

## 7. Minimal System

An initial version needs only three components:

```text
phonebook/
├── AGENTS.md       # Schema and operating instructions
├── phonebook.jsonl # One JSON object per person
└── README.md       # Purpose, setup, and usage examples
```

This keeps the system small while allowing its capabilities to grow through better instructions, additional fields, and agent-driven workflows.

## 8. Core Value Proposition

Phonebook is not merely an address book. It is a simple, inspectable personal relationship database that uses an agent to make heterogeneous people data searchable, editable, and useful through natural language.
