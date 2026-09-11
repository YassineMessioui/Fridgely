# Fridgely development journal

This journal records how Fridgely is designed and developed, not just what the final code looks like. Its purpose is to preserve the reasoning, tradeoffs, experiments, setbacks, and lessons that will be useful during retrospective reviews or when telling the project's story later.

## Opt-in rule

The journal changes only after an explicit request such as:

- “Document this session.”
- “Log this decision.”
- “Add today's work to the development journal.”

Normal implementation requests do not trigger journal updates. This keeps the history intentional and prevents routine agent activity from generating noisy or misleading entries.

## Entry workflow

1. Work proceeds normally through issues, branches, and pull requests.
2. The product owner explicitly requests a journal update.
3. The agent reconstructs the requested work from verified conversation and repository artifacts.
4. The entry separates confirmed decisions from proposals and open questions.
5. The entry is reviewed through the normal pull-request workflow.

If an active pull request already contains the work being documented, its journal update may be included there. Otherwise, the journal update should use a focused documentation branch and pull request.

## Entry format

- Store entries in `docs/development-journal/entries/`.
- Name entries `YYYY-MM-DD-short-topic.md`.
- Use the [entry template](TEMPLATE.md) as a guide rather than a rigid form.
- Write for a future reader who does not have access to the original Codex session.
- Summarize commands and conversations; do not paste raw transcripts.
- Link primary artifacts wherever possible.

## Journal index

- [2026-09-09 — Project foundation](entries/2026-09-09-project-foundation.md)
