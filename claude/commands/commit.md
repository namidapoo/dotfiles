---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git commit:*)
argument-hint: [additional explanation]
description: Create a git commit
model: claude-sonnet-4-20250514
---

## TODO

1. Review the current staged changes:

   ```bash
   git status
   git diff --staged
   ```

2. Check the commit history to determine the language for the commit message:

   ```bash
   git log -n 10 --pretty=format:"%s"
   ```

   - If the majority are in English, write in English
   - If the majority are in Japanese, write in Japanese

3. Analyze the changes and identify if there are any critical issues:

   - Check for sensitive information (passwords, API keys, etc.)
   - Verify that the changes are complete and coherent
   - If issues are found, confirm with the user before proceeding

4. Create and execute the commit with an appropriate message:

   ```bash
   git commit -m "<message>"
   ```

   refer to the **Commit Message Guidelines** section below when writing the message

5. Verify the commit was successful:

   ```bash
   git status
   ```

6. Provide a summary of what was committed to the user

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
