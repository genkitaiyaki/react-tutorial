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
