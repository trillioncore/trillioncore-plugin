---
name: use-trillioncore
description: Answer questions from a business's connected data in Trillioncore (email, meetings, messages, tables), keep its organization files, run requested account actions, and answer questions about Trillioncore itself (what it does, what it connects to, setup, plans, errors). Use when the user names Trillioncore (also called TC), asks about data connected to it, or asks how it works or how to set it up; not for local repository tasks.
---

Use the Trillioncore MCP tools from this plugin. Some clients show only tool names
until a tool is loaded, so this skill lists them. Do not install or call the CLI
as a fallback, invent a tool, or bypass a refused operation. Never ask for tokens,
passwords or verification codes in chat.

Call `get_context` first in each session. Its guidance holds the standing rules;
follow them, including its last line about your first reply.

For questions about Trillioncore itself, get path trillioncore/docs/llms.txt and read only the page that fits.

Tools not connected yet? Read https://www.trillioncore.com/SKILL.md and follow its
setup steps. The same pages are on the web: https://www.trillioncore.com/llms.txt.

## Tools

| Tool | What it does | When to call it |
| --- | --- | --- |
| `get_context` | Returns this organization's own setup files (organization.md, the person's profile and the data cheat sheet), its skills files and accounts, and what the person can write. | Call it first in each session, with organizationId when you have more than one organization, before any data question. |
| `organizations` | Lists the organizations this connection is approved to use. | Call it when you have more than one organization or do not know the organization id; pass the id to get_context and the data tools. |
| `index` | Shows the structure of the connected data: organizations, accounts, tables and models, never record content. | Call it after get_context to find an account and its tables; then use sql for tables that offer SQL, or search then get for stored records. |
| `search` | Searches stored records from connected accounts by words: email, meeting transcripts, messages, time entries, GitHub pull requests and published tables. | Use it to find records, then get to read one before you rely on it. For live PostgreSQL rows use index then sql; search does not read live rows. |
| `get` | Reads one record or document by the ref or path that search, index or get_context returned. | Use it after search to read the evidence before a claim, to open a skills file that the cheat sheet or the skills list points to, and to read a Trillioncore docs page. |
| `sql` | Runs one read-only PostgreSQL SELECT or WITH query on the approved tables of a connected account that offers SQL. | Before writing it, read the cheat sheet from get_context, then inspect the table with index (account path plus resourceKey) for exact columns. |
| `write_document` | Creates or replaces a Trillioncore document by path, or appends to a Markdown log. | Use it only after the person has seen the full draft and said yes to it; read the current file first. |
| `move_document` | Moves or renames a Trillioncore document. | Use it when the person asks to move or rename a file; system files cannot move. |
| `delete_document` | Deletes one Trillioncore document: it is hidden and its path is freed, not destroyed. | Use it only when the person asks to delete that file: name the path back and wait for a clear yes. |
| `act` | Performs one action on a connected account, such as sending an email. | Use it only when the person asks for that action; index on the account lists its actions and their input fields. |
| `create_organization` | Starts creating a new Trillioncore organization and returns a link the person opens to confirm it. | Use it only when the person asks for a new organization. |
