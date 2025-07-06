# CLAUDE.ja.md

このファイルは、このリポジトリでコードを扱う際の Claude Code (claude.ai/code) へのガイダンスを提供します。

## リポジトリ概要

これは macOS 上の開発環境設定を管理するための個人用 dotfiles リポジトリです。このリポジトリには、さまざまなツールやアプリケーションの設定ファイルが含まれています。

## 構造

- `Brewfile` - Homebrew パッケージ定義（CLI ツール、GUI アプリ、VS Code 拡張機能）
- `config/mise/` - 開発ツールのバージョン管理のための mise 設定
- `git/` - Git グローバル設定ファイル
- `zsh/` - Zsh シェル設定ファイル

## 管理されている主要な開発ツール

### Homebrew 経由 (Brewfile)
- 開発ツール: aws-cdk, gh (GitHub CLI), bun, deno, mise
- ユーティリティ: bat, fd, ripgrep, shellcheck, jq
- アプリケーション: Claude, Cursor, VS Code, Arc, 1Password

### mise 経由 (config/mise/config.toml)
- ランタイムバージョン: Node.js (lts), Bun (latest), Deno (latest), pnpm (latest)

## 定義済みタスク

以下のタスクが mise 経由で利用可能です：

```bash
mise run create-next-use-pnpm  # pnpm で Next.js プロジェクトを作成
mise run create-next-use-bun   # Bun で Next.js プロジェクトを作成
mise run cdk-init             # AWS CDK TypeScript プロジェクトを初期化
mise run aws-session          # AWS 認証ステータスを確認
```

## 一般的な操作

### パッケージのインストール/更新
```bash
# Homebrew パッケージをインストール
brew bundle

# mise ツールを更新
mise install
```

### Dotfiles の管理
設定ファイルを変更する際：
1. 各ディレクトリ内のファイルを直接編集
2. シェル設定 (zsh/) の変更にはシェルの再読み込みが必要
3. git/ 内の Git 設定変更はグローバルに適用される

## アーキテクチャに関する注記

- このリポジトリは、各ツールの設定をディレクトリごとにグループ化する構成を採用
- Brewfile は CLI ツールと GUI アプリケーション（VS Code 拡張機能を含む）の両方を管理
- mise は開発ツールのバージョンを動的に管理するために使用
- シンボリックリンク管理スクリプトはまだ存在しない - ファイルは適切な場所に手動でリンクする必要がある
