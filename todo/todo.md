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

おそらくORDERが原因なので、DBにindexを作成する
