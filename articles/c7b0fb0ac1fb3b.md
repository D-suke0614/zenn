---
title: "PostgreSQLのVACUUMについて"
emoji: "📮"
type: "tech"
topics:
  - "postgresql"
published: true
published_at: "2023-10-14 00:31"
---

## VACUUMとは
公式ドキュメント：https://www.postgresql.jp/document/9.6/html/sql-vacuum.html
公式ドキュメントより

```
VACUUM は、不要タプルが使用する領域を回収します。PostgreSQLの通常動作では、削除されたタプルや更新によって不要となったタプルは、テーブルから物理的には削除されません。 これらのタプルはVACUUMが完了するまで存在し続けます。 そのため、特に更新頻度が多いテーブルでは、VACUUMを定期的に実行する必要があります。
```

PostgreSQLではデータを削除しても、実際には削除フラグがついているだけで完全には削除されておらず、見えなくなっているだけ。
VACUUMをすることで、削除フラグがついたデータを完全に消し去ることができ、それによって空いた領域を再利用可能な状態に変更する。
つまり、更新頻度の高いテーブルに対して行うと効果的ということ。

## タプルとは
テーブル内にINSERT, UPDATE, DELETEで格納する行（row）のことをタプルという。

## VACUUM, VACUUM FULL, VACUUM ANAYZE
バキュームにはVACUUMとVACUUM FULL, VACUUM ANALYZEの３つがある

通常のVACUUMはユーザがバキュームできる権限を持つ、DB内のすべてのテーブルを処理する。
処理速度は速いが、回収した領域はほとんどOSに返されない。

VACUUM FULLはテーブルに対する排他ロックが必要で、処理に時間がかかるがより多くの領域を回収することができる「完全」なバキュームをすることができる。
大きな容量がテーブルから回収されなければいけない場合のみに使用されるべき。

VACUUM ANALYZEはVACUUM後にANALYZEを実行する。
※ANALYZEはDB内のテーブルに関する統計情報を更新するコマンド

## VACUUM

```
VACUUM テーブル名;

-- VERBOSEをつけることで、実行時間等の詳細情報を表示することができる
VACUUM VERBOSE テーブル名;
```

## VACUUM FULL

```
VACUUM FULL テーブル名;
```

## VACUUM ANALYZE

```
VACUUM ANALYZE テーブル名;
```

## AUTOVACUUMなんてものもあるらしい
PostgreSQLの機能で、自動バキュームを行ってくれるらしい。
詳細は[PostGreSQLの公式](https://www.postgresql.org/docs/current/runtime-config-autovacuum.html)を見てほしいが、色々チューニングもできるっぽい。
また、省略することも可能だが、使用することを強く推奨しているようなので、使うようにしよう。

## 参考記事
- https://postgresweb.com/post-5194
- https://qiita.com/neustrashimy/items/b3d64b749582b32ad0ff
