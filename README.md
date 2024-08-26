# 概要
開発やMacの初期設定に必要なツールをAnsible経由で一気に追加するためのレポジトリ

# 導入するツール・設定

## CLI (homebrew)
- Terminal関連
    - tree
        - ディレクトリ構造をTerminalで良い感じに表示してくれる
        - http://mama.indstate.edu/users/ice/tree/
    - peco
        - 取り込んだ入力を検索できる（sedコマンドの強化版）
        - https://github.com/peco/peco
- 開発環境整備
    - git
        - バージョン管理ツール
        - https://git-scm.com/downloads/guis/
    - anyenv
        - 各プログラミング言語で独立してバージョン管理ができる
        - https://github.com/anyenv/anyenv

## GUI (homebrew cask)
- Terminal関連
    - iTerm2
        - MacのTerminalを使いやすくしたTerminal
        - https://iterm2.com/
- 開発環境整備
    - Visual Studio Code
        - 拡張に優れたエディター
        - https://code.visualstudio.com/
    - Docker
        - 開発環境・アプリケーション環境をコンテナ形式で提供可能にするツール
        - https://www.docker.com/
    - Google Chrome
        - GoogleのWebブラウザ
        - https://www.google.com/intl/ja_jp/chrome/
    - Figma
        - 画面ワイヤーフレーム作成や、ブレストなどに利用するツール
        - https://www.figma.com/ja/
    - draw.io
        - ER図や構成図を手軽に作成できるツール
        - https://www.diagrams.net/
    - Postman
        - 手軽にPostなどのHTMLメソッドを発行できるツール
        - https://www.postman.com/
- その他便利ツール
    - Slack
        - リアルタイムチャットツール
        - https://slack.com/intl/ja-jp/
    - Rectangle
        - Macのウィンドウを良い感じで配置できるツール
        - https://rectangleapp.com/
    - Skitch
        - キャプチャに書き込みができるツール
        - https://evernote.com/intl/jp/products/skitch
    - Clipy
        - クリップボードの履歴を残し、コピーした情報を再利用できるツール
        - https://clipy-app.com/

## Mac本体の設定
- 隠しファイルを常に表示させる
- キーボード長押し時のアクセント表示を削除して、連続入力を可能にする

# 利用方法

## 1. Ansibleを利用するための前設定
1. HomeBrewのインストール
    - https://brew.sh/index_ja
2. Ansibleのインストール
    - Terminalを起動し、下記のコマンドでインストール
    - ```brew install ansible```

## 2. 設定したツールのインストール
```zsh
ansible-playbook setup.yml -i inventory
```

## 3. Terminalを再起動する
ツールインストール直後はbrewのパス定義が読み込まれないので、ターミナルを再起動する必要がある

## 4. 再ログイン
Macの設定を適用させる場合は、再ログインが必要！

## ※実行に失敗した場合は。。。
`brew cask` でインストールするGUIツールは既に導入されている場合があり `homebrew_cask` 以降に進めない場合がある。

その際は `Tips/特定のタグが付与されたスクリプトだけ実行する` に示しているタグ指定のインストールを別途実施すれば、続きから導入できる。

# Tips
## スクリプトが利用できるかの構文チェック
```zsh
ansible-playbook --syntax-check setup.yml -i inventory
```

## 特定のタグが付与されたスクリプトだけ実行する
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
