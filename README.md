# dotfiles

GNU Stow で管理する個人 dotfiles。

## 前提

```bash
brew install stow
```

## 使い方

リポジトリ直下に `.stowrc` があるため、`--target` / `--dir` の指定は不要。

```bash
cd ~/IdeaProjects/dotfiles

# パッケージを展開 (symlink 作成)
stow <package>

# ドライラン (実際には作らず動作確認)
stow -nv <package>

# 解除 (symlink 削除)
stow -D <package>

# 再展開
stow -R <package>
```

## パッケージ構成

各パッケージ配下のディレクトリ構造は `$HOME` 配下にそのまま symlink される。

```
dotfiles/
└── <package>/
    └── <$HOME からの相対パス>
```

例: `dotfiles/claude/.claude/settings.json` → `~/.claude/settings.json`

## 競合した場合

既に実体ファイルが target に存在すると stow はエラーで停止する。
退避してから再実行する:

```bash
mv ~/.foo ~/.foo.backup
stow <package>
```
