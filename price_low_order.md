#low_price

alpのログと以下のEXPLAINからこのクエリが遅いことがわかる  
```
mysql> EXPLAIN SELECT * FROM chair WHERE stock > 0 ORDER BY price ASC, id ASC LIMIT 20;
+----+-------------+-------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
| id | select_type | table | partitions | type | possible_keys | key  | key_len | ref  | rows  | filtered | Extra                       |
+----+-------------+-------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
|  1 | SIMPLE      | chair | NULL       | ALL  | NULL          | NULL | NULL    | NULL | 29205 |    33.33 | Using where; Using filesort |
+----+-------------+-------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
1 row in set, 1 warning (0.00 sec)
```  

```
mysql> EXPLAIN SELECT * FROM estate ORDER BY rent ASC, id ASC LIMIT 20;
+----+-------------+--------+------------+------+---------------+------+---------+------+-------+----------+----------------+
| id | select_type | table  | partitions | type | possible_keys | key  | key_len | ref  | rows  | filtered | Extra          |
+----+-------------+--------+------------+------+---------------+------+---------+------+-------+----------+----------------+
|  1 | SIMPLE      | estate | NULL       | ALL  | NULL          | NULL | NULL    | NULL | 29093 |   100.00 | Using filesort |
+----+-------------+--------+------------+------+---------------+------+---------+------+-------+----------+----------------+
1 row in set, 1 warning (0.00 sec)
```  

おそらくORDERが原因なので、DBにindexを作成する(priceとrentをidと組み合わせ)

```
mysql> CREATE INDEX price_id_idx on chair(price, id);
Query OK, 0 rows affected (0.34 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> EXPLAIN SELECT * FROM chair WHERE stock > 0 ORDER BY price ASC, id ASC LIMIT 20;
+----+-------------+-------+------------+-------+---------------+--------------+---------+------+------+----------+-------------+
| id | select_type | table | partitions | type  | possible_keys | key          | key_len | ref  | rows | filtered | Extra       |
+----+-------------+-------+------------+-------+---------------+--------------+---------+------+------+----------+-------------+
|  1 | SIMPLE      | chair | NULL       | index | NULL          | price_id_idx | 8       | NULL |   20 |    33.33 | Using where |
+----+-------------+-------+------------+-------+---------------+--------------+---------+------+------+----------+-------------+
1 row in set, 1 warning (0.00 sec)
```  

```
mysql> CREATE INDEX rent_id_idx on estate(rent, id);
Query OK, 0 rows affected (0.35 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> EXPLAIN SELECT * FROM estate ORDER BY rent ASC, id ASC LIMIT 20;
+----+-------------+--------+------------+-------+---------------+-------------+---------+------+------+----------+-------+
| id | select_type | table  | partitions | type  | possible_keys | key         | key_len | ref  | rows | filtered | Extra |
+----+-------------+--------+------------+-------+---------------+-------------+---------+------+------+----------+-------+
|  1 | SIMPLE      | estate | NULL       | index | NULL          | rent_id_idx | 8       | NULL |   20 |   100.00 | NULL  |
+----+-------------+--------+------------+-------+---------------+-------------+---------+------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)
```

