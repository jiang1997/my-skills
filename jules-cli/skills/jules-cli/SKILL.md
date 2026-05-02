---
name: jules-cli
description: Delegate suitable coding tasks from Claude Code to Google Jules CLI, monitor sessions, and pull/review results.
---

# Jules CLI workflow

Use this skill when the user wants to delegate work to Google Jules from Claude Code.

## Preconditions

Before using Jules:

1. Check that `jules` is installed:
   `jules version`

2. If not installed, suggest:
   `npm install -g @google/jules`

3. Check authentication:
   `jules remote list --repo`

4. If authentication fails, ask the user to run:
   `jules login`

## When to use Jules

Prefer Jules for:

- isolated bug fixes
- test generation
- dependency upgrades
- documentation updates
- small-to-medium feature implementation
- tasks that can be reviewed as a patch or PR

Avoid Jules for:

- tasks requiring local secrets
- tasks requiring private runtime state not available in GitHub
- highly interactive debugging
- changes that need many design decisions from the user
- urgent edits that Claude Code can complete locally faster

## Task delegation flow

1. Inspect the current git repository:
   - `git status`
   - `git branch --show-current`
   - `git remote -v`

2. Summarize the task clearly.

3. Create a high-context Jules prompt containing:
   - goal
   - repository context
   - files/modules likely involved
   - constraints
   - expected tests
   - definition of done
   - request for minimal, reviewable changes

4. Start Jules:

   `jules remote new --repo . --session "<prompt>"`

5. Record the returned session ID.

6. Check sessions:

   `jules remote list --session`

7. When complete, pull the result:

   `jules remote pull --session <session_id>`

8. Review locally before accepting:
   - `git diff`
   - run relevant tests
   - inspect changed files
   - do not blindly commit or merge

## Prompt template

Use this template when creating a Jules session:

```text
You are working on repository: <repo>

Task:
<task>

Context:
<context from codebase>

Relevant files or areas:
<files>

Constraints:
- Keep the change minimal and reviewable.
- Preserve existing public APIs unless necessary.
- Follow existing style and patterns.
- Add or update tests where appropriate.
- Do not introduce unrelated refactors.

Validation:
- Run relevant tests if possible.
- Explain what was changed and why.
- Mention any tests that could not be run.

Definition of done:
<done criteria>
```