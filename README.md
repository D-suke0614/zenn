# Zenn CLI

* [📘 How to use](https://zenn.dev/zenn/articles/zenn-cli-guide)

## 記事の作成
```bash
$ npx zenn new:article

# ただこの形式だとハッシュ値みたいなファイル名になるので、自分で作成する方が良さそう...
```

```yml
---
title: "" # 記事のタイトル
emoji: "😸" # アイキャッチとして使われる絵文字（1文字だけ）
type: "tech" # tech: 技術記事 / idea: アイデア記事
topics: [] # タグ。["markdown", "rust", "aws"]のように指定する
published: true # 公開設定（falseにすると下書き）
---
ここから本文を書く
```

## プレビューする
```bash
$ npx zenn preview

# portを指定することもできる
npx zenn preview --port 3000
```
