## このリポジトリについて
[locust](https://locust.io/)でサーバーに対して負荷試験を行うためのコードを管理するディレクトリのテンプレートです。<br>
**以下からREADME.mdのテンプレートとして使えます。**

## このディレクトリについて
このディレクトリでは、[locust](https://locust.io/)というpythonのライブラリを利用してAPIサーバーをターゲットとした負荷試験を行うためのコードを管理しています。</br>
負荷試験はlocalhostに建てたlocustサーバーのwebUIから実行できます。

## 環境構築

### 1. python(>=3.13)のインストール
python3.13もしくはそれより新しいバージョンをインストールしてください。</br>
[asdf](https://asdf-vm.com/)や[pyenv](https://github.com/pyenv/pyenv)などのバージョン管理ツールを利用できます。

**asdfの場合**
```shell
brew install asdf
asdf plugin-add python
asdf install python 3.13.1
asdf global python 3.13.1
python -V
# output
# Python 3.13.1
```

**pyenvの場合**
```shell
brew install pyenv
pyenv install 3.13.1
pyenv global 3.13.1
python -V
# output
# Python 3.13.1
```

### 2. poetryのインストール
pythonのパッケージマネジャー[poetry](https://python-poetry.org/)をインストールしてください。

**asdfの場合**
```shell
asdf plugin-add poetry https://github.com/asdf-community/asdf-poetry.git
asdf install poetry latest
asdf global poetry <version>
poetry --version
# output
# Poetry (version <version>)

poetry self add poetry-plugin-shell
```

**pyenvの場合**
```shell
pip install poetry
poetry --version
# output
# Poetry (version <version>)

poetry self add poetry-plugin-shell
```

### 3. 依存関係インストール & 仮想環境への出入り
```shell
poetry install

# 仮想環境に入る
poetry shell

# 仮想環境から抜ける
exit
```

## 負荷試験の実行

### .envファイルの設定
.envファイルを作成し、負荷試験のターゲットとなるホストを.envに追記してください。</br>
APIキーなど、各自必要な環境変数を.envに追記してください。

```shell
touch .env
echo LOCUST_HOST=https://example.com >> .env
# echo API_KEY=sample-api-key >> .env
# locustサーバー立ち上げの簡素化
echo "alias locust='locust --config ./locust/locust.conf -H \${LOCUST_HOST}'" >> .env
```

### ローカルlocustサーバの立ち上げ
```shell
poetry shell
source .env
locust
```
[http://localhost:8089](http://localhost:8089)にアクセス。

## 負荷試験の設定変更

### locustサーバーの設定変更
./locust/locust.confを編集してください。</br>
[ドキュメント](https://docs.locust.io/en/stable/configuration.html)

### 負荷試験内容の設定変更
./locust/locustfile.pyを編集してください。</br>
[ドキュメント](https://docs.locust.io/en/stable/writing-a-locustfile.html)
