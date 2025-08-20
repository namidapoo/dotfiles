---
allowed-tools: Bash(git status:*), Bash(git diff:*), Bash(git log:*), Bash(git push:*), Bash(git branch:*), Bash(gh pr:*), Bash(gh repo:*)
argument-hint: [additional context]
description: Create a GitHub pull request
model: claude-sonnet-4-20250514
---

## TODO

1. Check the current repository state and ensure all changes are committed:

   ```bash
   git status -sb
   git branch -vv
   ```

   - First command shows uncommitted/staged changes in compact format
   - Second command shows current branch with tracking information
   - Verify no uncommitted changes exist before creating PR

2. Review all changes that will be included in the PR:

   ```bash
   # Get the default branch from GitHub
   BASE_BRANCH=$(gh repo view --json defaultBranchRef --jq '.defaultBranchRef.name')
   # Review changes
   git diff origin/$BASE_BRANCH..HEAD --stat
   git log origin/$BASE_BRANCH..HEAD --oneline
   ```

   - Automatically detects the repository's default branch
   - Shows file changes summary with `--stat`
   - Lists commits that will be included in the PR

3. Ensure the branch is pushed to remote:

   ```bash
   git push -u origin HEAD
   ```

   - Pushes the current branch if not already pushed
   - Sets up tracking relationship with remote branch
   - Safe to run even if already pushed (will show "Everything up-to-date")

4. Check for PR template in the repository:

   ```bash
   gh repo view --json pullRequestTemplates --jq '.pullRequestTemplates[0].body' 2>/dev/null || echo "No PR template found"
   ```

   - Uses GitHub API to fetch PR templates directly
   - Falls back to default template if none exists

5. Determine the language for PR title and description:

   ```bash
   git log -n 10 --pretty=format:"%s"
   ```

   - If the majority are in English, write in English
   - If the majority are in Japanese, write in Japanese
   - If `$ARGUMENTS` includes a language instruction, follow that instead

6. Create the pull request:

   - If a project-specific PR template exists (found in step 4), use that template
   - If no template exists, use the **Default PR Template** section below
   - Create the PR with the appropriate template:

   ```bash
   gh pr create --title "<title>" --body "<PR body following the template>"
   ```

7. Verify the PR was created successfully:

   ```bash
   gh pr view --web
   ```

8. Provide the PR URL and summary to the user

## Default PR Template

Use this template when no repository-specific template is found:

```markdown
<!-- Instructions for GitHub Copilot Code Review: Please provide your comments and review this pull request in Japanese. -->

## Issue

<!--
  If there's a related issue: fixes #123
  If no related issue: N/A - Brief description of the purpose
  Examples:
  - fixes #42
  - N/A - Add TypeScript configuration
  - N/A - Update dependencies
-->

N/A - [brief description of the purpose]

## Changes

<!--
  List the main changes made in this PR using bullet points
  Examples:
  - Add user authentication feature
  - Fix memory leak in data processing
  - Update React from v17 to v18
-->

- [Describe the main changes made]

## Verification

<!-- Check off completed verification steps -->

- [ ] Tests pass successfully
- [ ] No lint/type errors
- [ ] No breaking changes introduced
- [ ] Changeset file created (if needed for version bump)
<!-- Changesets are required when the changes affect the published package (new features, bug fixes, breaking changes). Not needed for internal tooling, docs, or config changes. -->

## Additional Notes

<!-- Any additional context, implementation details, or notes for reviewers -->

```

## Pull Request Guidelines

- **Title format**:

  - Follow the same convention as commit messages if applicable
  - Be descriptive but concise (max ~72 characters)
  - Example: `feat(auth): Add user authentication with OAuth2`

- **Issue section**:

  - Use `fixes #<number>` to automatically close related issues
  - Use `N/A - <description>` if no related issue exists
  - Provide brief context when there's no issue number

- **Changes section**:

  - List all significant changes in bullet points
  - Group related changes together
  - Be specific about what was modified, added, or removed
  - Follow the examples in the template comments

- **Verification section**:

  - Check all applicable verification items
  - Changeset files are required for published packages when:
    - Adding new features
    - Fixing bugs
    - Making breaking changes
  - Not needed for internal tooling, docs, or config changes

- **Additional Notes section**:

  - Include implementation details for complex changes
  - Add context that helps reviewers understand the approach
  - Mention any trade-offs or alternatives considered

- **Language rule**:

  - Use the same language as the majority of recent commits
  - If `$ARGUMENTS` includes a language instruction, follow that instead

- **Arguments rule**:
  - Treat `$ARGUMENTS` as additional context or instruction for the PRtitle/description

## Important Notes

- Always ensure all changes are committed before creating a PR
- Do not force push unless absolutely necessary
- If the PR template exists in the repository, always use it over the default
- Check CI/CD status after creating the PR
- Do not merge the PR unless explicitly instructed
- The GitHub Copilot instruction comment helps ensure reviews are provided in the appropriate language
