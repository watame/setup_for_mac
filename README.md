# setup_for_mac
Mac設定用Ansibleレポジトリ

# 1. Ansibleを利用するための前設定
1. HomeBrewのインストール
    - https://brew.sh/index_ja
2. Ansibleのインストール
    - Terminalを起動し、下記のコマンドでインストール
    - ```brew install ansible```

# 2. 設定したツールのインストール
```zsh
ansible-playbook setup.yml -i inventory
```

# 3. Terminalを再起動する
ツールインストール直後はbrewのパス定義が読み込まれないので、ターミナルを再起動する必要がある

# 4. 再ログイン
Macの設定を適用させる場合は、再ログインが必要！

# +α スクリプトが利用できるかの構文チェック
```zsh
ansible-playbook --syntax-check setup.yml -i inventory
```

# +α 特定のタグが付与されたスクリプトだけ実行する
下記のようにタグを指定し、特定のタグに紐づく処理を呼び出すことも可能
```zsh
ansible-playbook setup.yml -i inventory --tags tag_name
```

- 例：`preference`タグの設定スクリプトだけを実施する
    - `ansible-playbook setup.yml -i inventory --tags preference`

複数タグを呼び出す場合は以下
```zsh
ansible-playbook setup.yml -i inventory --tags tag_name1,tag_name2
```

- 例：`dotfiles`->`initialize_shell`タグの順番で設定スクリプトを実施する
    - `ansible-playbook setup.yml -i inventory --tags dotfiles,initialize_shell`


# 参考サイト
- [AnsibleでMacの環境構築をしてみた](https://rightcode.co.jp/blog/information-technology/ansible-mac-environment-setup)
- [Ansibleでタグをつかって特定の処理のみ実行する](https://www.kabegiwablog.com/entry/2018/02/23/090000)
- [ansible-playbook実行時に複数tagを指定する](https://qiita.com/tommarute/items/5cb93abdc96fa228bc13)
- [Macの環境構築をAnsibleで自動化してみた 2021年版](https://tech.prog-8.com/entry/2021/12/19/setup-mac-ansible)
