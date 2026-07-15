---
name: write-session-handoff
description: 在任务或会话结束、暂停、交接、切换到新会话、上下文即将压缩，或用户要求收尾、保存上下文、总结进度、编写交接文档时，创建或更新一份独立完整的 HANDOFF.md，使完全没有上下文的新会话能够继续当前任务。也适用于用户说“结束会话”“先到这里”“暂停”“交接”“换个会话继续”或“写 HANDOFF”等场景。
---

# Write Session Handoff

Create a truthful, current snapshot of the work and save it to `HANDOFF.md`. Write for a capable successor that has no access to the current conversation.

## Workflow

1. Locate the target directory.
   - Prefer the active Git repository root.
   - Otherwise use the current task or project root.
   - If there is no project, use the current working directory.
   - Write to `<target>/HANDOFF.md`.

2. Reconstruct the state from evidence.
   - Use the current request and conversation as context.
   - Inspect an existing `HANDOFF.md`, relevant source and task files, `git status`, the current branch and commit, the diff, recent commits, and available test or command results when applicable.
   - Distinguish completed, in-progress, planned, and blocked work. Do not convert an intention into a completed claim.
   - Record exact file paths, identifiers, commands, errors, and verification results when they help the next session resume.
   - State uncertainty explicitly instead of guessing.

3. Update the handoff.
   - Replace stale status with the current snapshot; do not append a second competing handoff.
   - Preserve still-valid decisions, unresolved blockers, and hard-won pitfalls from an existing handoff.
   - Match the user's working language. Prefer concise, concrete wording over a chronological diary.
   - Never include secrets, credentials, tokens, or unnecessary personal data.
   - Do not stage, commit, revert, clean, stop services, or otherwise change the project solely to prepare the handoff. Only create or update `HANDOFF.md` unless the user explicitly requests more.

4. Verify the result.
   - Re-read `HANDOFF.md` after writing it.
   - Remove placeholders and stale statements.
   - Ensure every required section below is present, even when the honest entry is "None" or "No known blocker".
   - In the final response, link to the file and summarize the most important current state in one or two sentences.

## Required Format

Use this structure, adapting labels to the user's language:

```markdown
# HANDOFF

> Updated: YYYY-MM-DD HH:MM TZ

## 1. Task

- Objective and intended outcome
- Scope, constraints, and acceptance criteria

## 2. Completed

- Concrete finished work with relevant files or behavior
- Verification commands and their results

## 3. Current State and Blockers

- Work in progress and uncommitted or unverified changes
- Exact blocking condition, error, dependency, or missing decision
- Failed approaches that are relevant to the blocker

## 4. Next Steps

1. First executable action, including the file or command to start with
2. Subsequent actions in dependency order
3. Final verification or acceptance check

## 5. Pitfalls: Do Not Repeat

- What was tried, why it failed, and the correct or safer approach

## 6. Key Context

- Workspace or repository root
- Branch and commit, when applicable
- Important files, decisions, dependencies, running services, and useful commands
```

Make the next step executable, not vague. For each pitfall, capture enough cause and evidence to prevent repetition; do not invent pitfalls merely to fill the section.
