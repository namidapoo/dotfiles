# dotfiles

Personal macOS development environment configuration files (dotfiles) repository.

## Overview

This repository contains various configuration files for setting up a development environment. Currently, there are no installation scripts, so manual setup is required. Automation scripts will be added in the future.

## Structure

```
dotfiles/
├── Brewfile              # Homebrew package definitions
├── claude/              # Claude AI configuration
│   ├── CLAUDE.md        # Global instructions for Claude
│   ├── settings.json    # Claude permissions and hooks
│   └── commands/        # Custom Claude command templates
├── config/
│   └── mise/            # mise (development tools manager) configuration
├── git/                 # Git global configuration
│   ├── .gitconfig
│   └── .gitignore_global
└── zsh/                 # Zsh shell configuration
    ├── .zprofile
    ├── .zshenv
    └── .zshrc
```

## Future Plans

- [ ] Create automated installation scripts
- [ ] Automatic symlink creation for configuration files
- [ ] OS-specific configuration support
- [ ] Add backup functionality

## License

No license is set as these are personal configuration files.
