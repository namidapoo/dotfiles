# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a personal dotfiles repository for managing development environment configuration on macOS. The repository contains configuration files for various tools and applications.

## Structure

- `Brewfile` - Homebrew package definitions (CLI tools, GUI apps, VS Code extensions)
- `config/mise/` - mise configuration for development tool version management
- `git/` - Git global configuration files
- `zsh/` - Zsh shell configuration files

## Key Development Tools Managed

### Via Homebrew (Brewfile)
- Development tools: aws-cdk, gh (GitHub CLI), bun, deno, mise
- Utilities: bat, fd, ripgrep, shellcheck, jq
- Applications: Claude, Cursor, VS Code, Arc, 1Password

### Via mise (config/mise/config.toml)
- Runtime versions: Node.js (lts), Bun (latest), Deno (latest), pnpm (latest)

## Defined Tasks

The following tasks are available via mise:

```bash
mise run create-next-use-pnpm  # Create Next.js project with pnpm
mise run create-next-use-bun   # Create Next.js project with Bun
mise run cdk-init             # Initialize AWS CDK TypeScript project
mise run aws-session          # Check AWS authentication status
```

## Common Operations

### Installing/Updating Packages
```bash
# Install Homebrew packages
brew bundle

# Update mise tools
mise install
```

### Managing Dotfiles
When modifying configuration files:
1. Edit files directly in their respective directories
2. Changes to shell configuration (zsh/) require reloading the shell
3. Git configuration changes in git/ are applied globally

## Architecture Notes

- This repository uses a directory-based organization where each tool's configuration is grouped together
- The Brewfile manages both CLI tools and GUI applications, including VS Code extensions
- mise is used for managing development tool versions dynamically
- No symlink management script exists yet - files need to be manually linked to their proper locations
