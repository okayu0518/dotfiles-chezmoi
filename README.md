# My Dotfiles

[![chezmoi](https://img.shields.io/badge/chezmoi-managed-ff69b4)](https://www.chezmoi.io)
[![Hyprland](https://img.shields.io/badge/WM-Hyprland-58C4DD)](https://hyprland.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Arch Linux をベースにした Hyprland Wayland 環境の dotfiles です。
[chezmoi](https://www.chezmoi.io) で管理し、一発で環境を再現できます。

## 構成

| カテゴリ | ツール |
|---|---|
| **ウィンドウマネージャ** | Hyprland (hypridle, hyprlock, hyprpaper, hyprsunset) |
| **シェル** | Zsh, Bash |
| **ターミナル** | Alacritty, Foot, Ghostty, WezTerm, xfce4-terminal |
| **エディタ** | Neovim (lazy.nvim), Vim, Emacs |
| **バー / ランチャー** | Waybar, Rofi, wlogout |
| **通知 / 画面** | swaync, kanshi |
| **マルチプレクサ** | tmux |
| **Git** | gitconfig |
| **共通シェル設定** | エイリアス (`aliases.sh`), 環境変数 (`env.sh`), 関数 (`functions.sh`) |

## インストール

### 前提条件

- **Git** がインストールされていること
- インターネット接続（chezmoi のダウンロードとパッケージインストールに必要）

### ワンライナー

```bash
sh -c "$(curl -fsLS get.chezmoi.io)" -- -b $HOME/.local/bin init --apply git@github.com:okayu0518/dotfiles-chezmoi.git
```

このコマンド1つで以下の処理が自動実行されます。

1. chezmoi バイナリを `$HOME/.local/bin` にダウンロード
2. このリポジトリをクローン
3. `run_onchange_install-packages.sh.tmpl` を実行（パッケージ自動インストール）
4. `chezmoi apply` で全設定ファイルを `$HOME` に展開

> **Tip**: 初回実行後、`export PATH="$HOME/.local/bin:$PATH"` を `~/.bashrc` などに追加すると便利です。

### 既存の chezmoi ユーザー向け

```bash
chezmoi init --apply gh:okayu0518/dotfiles-chezmoi
```

## カスタマイズ方法

### 現在の環境で設定を編集する

```bash
# 管理下のファイルをエディタで開く
chezmoi edit ~/.zshrc

# 変更を確認
chezmoi diff

# 変更を適用
chezmoi apply
```

### リポジトリに変更を反映する

```bash
chezmoi re-add    # 変更を追跡
chezmoi cd        # chezmoi の管理ディレクトリに移動
git add . && git commit -m "update config"
git push
```

### テンプレートについて

環境依存の値を埋め込みたい場合は `dot_*.tmpl` ファイルを作成します。

```bash
# 例: ホスト名によって分岐
chezmoi add --template ~/.config/hypr/hyprland.conf
```

詳しくは [chezmoi のテンプレートドキュメント](https://www.chezmoi.io/user-guide/templating/) を参照してください。

## 更新

```bash
chezmoi update      # リモートの変更を取得 → apply
```

## トラブルシューティング

| 症状 | 対処 |
|---|---|
| `chezmoi` コマンドが見つからない | `export PATH="$HOME/.local/bin:$PATH"` を実行 |
| パッケージがインストールされない | `chezmoi run-onchange` を実行してスクリプトを再実行 |
| 設定が反映されない | `chezmoi diff` で差分を確認 → `chezmoi apply` |
| 特定のファイルだけ適用をスキップしたい | `.chezmoiignore` を作成してパターンを指定 |

## 参考リンク

- [chezmoi 公式ドキュメント](https://www.chezmoi.io/docs/)
- [chezmoi テンプレートガイド](https://www.chezmoi.io/user-guide/templating/)
- [Hyprland Wiki](https://wiki.hyprland.org/)

