# dotfiles

個人用の macOS 開発環境設定ファイル (dotfiles) を管理するリポジトリです。

## 概要

このリポジトリには、開発環境を構築するための各種設定ファイルが含まれています。現在はインストールスクリプトがないため、手動でのセットアップが必要ですが、今後自動化スクリプトを追加予定です。

## 構成

```
dotfiles/
├── Brewfile              # Homebrew パッケージ定義
├── claude/              # Claude AI 設定
│   ├── CLAUDE.md        # Claude へのグローバル指示
│   ├── settings.json    # Claude の権限とフック
│   └── commands/        # カスタム Claude コマンドテンプレート
├── config/
│   └── mise/            # mise (開発ツール管理) 設定
├── git/                 # Git グローバル設定
│   ├── .gitconfig
│   └── .gitignore_global
└── zsh/                 # Zsh シェル設定
    ├── .zprofile
    ├── .zshenv
    └── .zshrc
```

## 今後の予定

- [ ] 自動インストールスクリプトの作成
- [ ] 設定ファイルの自動シンボリックリンク
- [ ] OS 別の設定対応
- [ ] バックアップ機能の追加

## ライセンス

個人用設定ファイルのため、ライセンスは設定していません。
