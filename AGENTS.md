# Agent Instructions

## Commit Messages

All commits — whether regular, merge, or amend — must have detailed, structured commit messages. This applies even when creating merge commits via `git commit --amend --no-edit` or `git merge --no-edit`.

### Merge Commit Format

Every merge commit must include:

1. **Title line**: `Merge PR #NNNNN: <type>: <short description>` using conventional commit format (`feat:`, `fix:`, `refactor:`, etc.)
2. **Summary paragraph**: 1-2 sentences explaining what the PR does in plain language
3. **`## What this PR does` section**: Bullet points or subsections explaining the changes
4. **`## Technical Details` section**: Implementation specifics — what files changed, how the fix works, API changes, etc.
5. **`## Impact` section**: Before/after behavior, user-facing effects
6. **`## Merge Notes` section**: Conflict resolution details, build verification status
7. **PR reference**: Link back to the PR

### Example

```
Merge PR #27075: fix: persist raw streaming errors in chat history

This PR fixes a bug where raw streaming errors were silently dropped
instead of being saved to chat history.

## What this PR does

### Bug Fix: Missing await on async database write

In `backend/open_webui/utils/middleware.py`, the
`Chats.upsert_message_to_chat_by_id_and_message_id()` call was missing
the `await` keyword, causing streaming errors to be silently lost.

## Impact

- **Before**: Raw streaming errors from LLM providers were silently dropped
- **After**: Errors are properly persisted to chat history

## Merge Notes

- Clean merge with no conflicts
- Build verified passing after merge

PR: https://github.com/open-webui/open-webui/pull/27075
```

### Regular Commits

Regular (non-merge) commits should also be detailed but can be shorter:

1. **Title line**: `<type>: <description>` in imperative mood
2. **Body**: What changed and why, not what the code does line-by-line
3. Reference issues/PRs where relevant

### Rules

- Never use generic messages like "fix", "update", "merge", "wip", "changes"
- Always explain _why_ something changed, not just _what_
- Include file paths when relevant for discoverability
- Reference upstream PRs with full URLs
- Verify the build passes before committing when possible
