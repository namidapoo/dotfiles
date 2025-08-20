---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git branch:*), Bash(git commit:*)
argument-hint: [additional explanation]
description: Create a git commit
model: claude-sonnet-4-20250514
---

## Context

- Current git status: !`git status`
- Staged changes: !`git diff --staged`
- Recent commits (for language detection): !`git log -n 10 --pretty=format:"%s"`
- Current branch: !`git branch --show-current`

## Your Task

Based on the above context:

1. Analyze the staged changes for any critical issues:

   - Review the **Staged changes** from context above
   - Check for sensitive information (passwords, API keys, etc.)
   - Verify that the changes are complete and coherent
   - If issues are found, confirm with the user before proceeding

2. Determine the commit message language:

   - Based on the **Recent commits** from context above
   - If the majority are in English, write in English
   - If the majority are in Japanese, write in Japanese
   - If `$ARGUMENTS` includes a language instruction, follow that instead

3. Create and execute the commit:

   - Refer to the **Commit Message Guidelines** section below when writing the message
   - Use `git commit -m` with an appropriate message

4. Verify the commit was successful:

   - Execute `git status` to verify the commit was successful
   - Provide a summary of what was committed to the user

## Commit Message Guidelines

- Follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:
  - Format: `<type>(optional scope): <description>`
  - Example: `feat(auth): add OAuth2 login support`
- **Allowed types**: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `chore`
- Use the **imperative mood** in the description (e.g., "add", not "added" or "adds").
- Keep the **summary concise** (max ~72 characters).
- **Body rules**:

  - By default, always include a body.
  - Exception: if the change is extremely simple and self-explanatory, a summary alone is acceptable.
  - Insert one blank line after the summary, then write the body in **bullet points**.
  - Each bullet should describe a reason, context, or detail of the change.
  - Example:

    ```
    feat(auth): add OAuth2 login support

    - implement login with OAuth2
    - update user model with providerId
    - add tests for OAuth2 flow
    ```

- **Language rule**:
  - Use the same language as the majority of recent commits
  - If `$ARGUMENTS` includes a language instruction, follow that instead
- **Focus rule**:
  - Do **not** write vague phrases like "fixed review comments", or "minor fix".
  - Always describe **what was actually changed** (e.g., "remove unused import", "fix null check in auth flow").
- **Arguments rule**:
  - Treat `$ARGUMENTS` as additional context or instruction for the commit message

## Important Notes

- Do not execute `git add`
- The changes are already staged with the correct granularity and responsibility.
- Do not execute `git push`
