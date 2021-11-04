# Memo

- チュートリアルの感想とかを書いていく

## チュートリアルを始める前に

> このチュートリアルは実際に手を動かして学びたい人向けに構成されています。
> コンセプトを順番に学んでいきたい人は一段階ずつ学べるガイドを参照してください。
> このチュートリアルとガイドは互いに相補的なものです。

- 他のガイドもあるらしい。。これが終わったら見てみよう

### 前提知識

> JavaScript を復習する必要がある場合は、このガイドを読むことをお勧めします。

- ある程度理解してるつもりだけど、これを機に再学習してもいいかもしれん。

## チュートリアルの準備

> このチュートリアルを最後まで進めるための方法が2種類あります。
> ブラウザでコードを書くか、マシン上にローカルな開発環境をセットアップするかのどちらかです。

- ローカルな開発環境でやりたいな。。
- せっかくなのでdocker上で動かそう

### オプション 2: ローカル開発環境

> これは完全にオプションであり、このチュートリアルを進めるのに必須ではありません！

- 開発環境構築しなくても気軽に試せるのはええですね〜

#### オプション：好きなテキストエディタを使ってローカルでチュートリアルを進める方法

> 最新の Node.js がインストールされていることを確かめる。

環境を準備していく

- Dockerfile

```Dockerfile
FROM node
WORKDIR /usr/src/app
```

- docker-compose.yml
  - とりあえず「tty: true」つけて起動しっぱにしとく
  - 実行しそうなコマンドはコメントアウトで残しとく

```yaml
version: '3.9'

services:
  node:
    build:
      context: .
      dockerfile: Dockerfile
    volumes:
      - ./node:/usr/src/app:cached
    # command: sh -c "cd my-app && npm start"
    tty: true
    ports:
      - "3000:3000"
```

- 起動確認

```shellscript
❯ docker-compose up
[+] Running 1/1
 ⠿ Container react-tutorial-node-1  Created                                                           0.0s
Attaching to react-tutorial-node-1
react-tutorial-node-1  | Welcome to Node.js v16.11.1.
react-tutorial-node-1  | Type ".help" for more information.
```

- 大丈夫そうね

- devcontainerのファイルも作っておく

> Create React App のインストールガイドに従って新しいプロジェクトを作成する。

- コンテナ内に入って以下のコマンドを打つ

```shellscript
root@08789b79df9e:/usr/src/app# npx create-react-app my-app
```

- yes

```shellscript
Need to install the following packages:
  create-react-app
Ok to proceed? (y) y
```

> 新しく作ったプロジェクトの src/ 内にあるファイルをすべて削除する

```shellsript
root@a83ae593e0f0:/usr/src/app/my-app# cd src/
root@a83ae593e0f0:/usr/src/app/my-app/src# rm -f *
root@a83ae593e0f0:/usr/src/app/my-app/src# touch index.css
root@a83ae593e0f0:/usr/src/app/my-app/src# touch index.js
```

> src/ フォルダ内に index.css という名前のファイルを作り、ここの CSS コードを記入する。

> src/ フォルダ内に index.js という名前のファイルを作り、ここの JS コードを記入する。

> src/ フォルダ内の index.js ファイルの先頭に以下の 3 行のコードを加える。

> これでプロジェクトフォルダ内で npm start を実行し、ブラウザで http://localhost:3000 を開くと、空の三目並べの盤面が表示されるはずです。

- なんかエラーが出たな。。

```shellscript
root@a83ae593e0f0:/usr/src/app/my-app# npm start

> my-app@0.1.0 start
> react-scripts start

node:internal/modules/cjs/loader:488
      throw e;
      ^

Error [ERR_PACKAGE_PATH_NOT_EXPORTED]: Package subpath './lib/tokenize' is not defined by "exports" in /usr/src/app/my-app/node_modules/postcss-safe-parser/node_modules/postcss/package.json
    at new NodeError (node:internal/errors:371:5)
    at throwExportsNotFound (node:internal/modules/esm/resolve:416:9)
    at packageExportsResolve (node:internal/modules/esm/resolve:669:3)
    at resolveExports (node:internal/modules/cjs/loader:482:36)
    at Function.Module._findPath (node:internal/modules/cjs/loader:522:31)
    at Function.Module._resolveFilename (node:internal/modules/cjs/loader:919:27)
    at Function.Module._load (node:internal/modules/cjs/loader:778:27)
    at Module.require (node:internal/modules/cjs/loader:999:19)
    at require (node:internal/modules/cjs/helpers:102:18)
    at Object.<anonymous> (/usr/src/app/my-app/node_modules/postcss-safe-parser/lib/safe-parser.js:1:17) {
  code: 'ERR_PACKAGE_PATH_NOT_EXPORTED'
}

Node.js v17.0.1
```