# Installation
```
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply gh:yourusername/dotfiles
```

1. chezmoi バイナリを /tmp に取得
2. GitHub から dotfiles を clone
3. run_once_ / run_onchange_ スクリプトを実行（パッケージインストール等）
4. chezmoi apply で全設定ファイルを $HOME に展開
