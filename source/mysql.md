# MySQL

## JOIN ON句で結合条件を付けた場合
JOIN ONで絞り込み条件を書くと、「結果を絞るのではなく、結合前のテーブルのレコードを絞る」らしい。

## 指定されたカラム名を持つテーブルを検索
```SQL
SELECT
    table_name,
    column_name
FROM information_schema.columns
where 
    column_name = '検索したいカラム名'
    AND table_schema = '検索対象のデータベース名';
```

## インデックス
### インデックスとは
データの検索速度を向上させるために、どの行がどこにあるかを示した索引のこと。  
データを検索するときに、目的のデータが見つかるまですべての行を一行ずつ調べていくよりも、索引を利用して目的の行の場所を見つけてからその行のデータを読み取る方が効率的だという考えにより、非常によく用いられる方法。  

**特に大きなテーブルでは、インデックスを用いることにより、大幅にそのパフォーマンスが改善されます。**

###  パフォーマンスが向上するケース
* 表の結合条件に使用される列に対してインデックスを作成するとパフォーマンスが向上する。
* 値の分布が大きい(異なる値が多い)列に対してインデックスを作成するとパフォーマンスが向上する。

### パフォーマンスが低下するケース
* 値の分布が小さい列に対してインデックスを作成するとパフォーマンスが低下する。
* テーブルを更新すると、インデックスも更新される。そのため、テーブルが頻繁に更新されるような場合にインデックスを利用するとパフォーマンスは低下する。

### 注意点
* インデックスは表のデータとは別の領域に保存されるので、データベース設計時にはインデックスの領域も見込まなければならない。
* インデックスは表のデータに対して作成するので、ビューのデータに対しては作成できない。ただし、ビューに対してデータを検索する場合は、元のテーブルに作成されたインデックスが利用される。

## dumpファイル作成
tableをdumpする
```
mysqldump -u [ユーザー名] -p [DB名] [テーブル名] > dump.sql
```