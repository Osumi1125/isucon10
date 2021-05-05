#isuumo DBの情報  

## chair table

```
mysql> show columns from chair;
+-------------+---------------+------+-----+---------+-------+
| Field       | Type          | Null | Key | Default | Extra |
+-------------+---------------+------+-----+---------+-------+
| id          | int(11)       | NO   | PRI | NULL    |       |
| name        | varchar(64)   | NO   |     | NULL    |       |
| description | varchar(4096) | NO   |     | NULL    |       |
| thumbnail   | varchar(128)  | NO   |     | NULL    |       |
| price       | int(11)       | NO   |     | NULL    |       |
| height      | int(11)       | NO   |     | NULL    |       |
| width       | int(11)       | NO   |     | NULL    |       |
| depth       | int(11)       | NO   |     | NULL    |       |
| color       | varchar(64)   | NO   |     | NULL    |       |
| features    | varchar(64)   | NO   |     | NULL    |       |
| kind        | varchar(64)   | NO   |     | NULL    |       |
| popularity  | int(11)       | NO   |     | NULL    |       |
| stock       | int(11)       | NO   |     | NULL    |       |
+-------------+---------------+------+-----+---------+-------+
13 rows in set (0.00 sec)

```

## estate table

```
mysql> show columns from estate;
+-------------+---------------+------+-----+---------+-------+
| Field       | Type          | Null | Key | Default | Extra |
+-------------+---------------+------+-----+---------+-------+
| id          | int(11)       | NO   | PRI | NULL    |       |
| name        | varchar(64)   | NO   |     | NULL    |       |
| description | varchar(4096) | NO   |     | NULL    |       |
| thumbnail   | varchar(128)  | NO   |     | NULL    |       |
| address     | varchar(128)  | NO   |     | NULL    |       |
| latitude    | double        | NO   |     | NULL    |       |
| longitude   | double        | NO   |     | NULL    |       |
| rent        | int(11)       | NO   |     | NULL    |       |
| door_height | int(11)       | NO   |     | NULL    |       |
| door_width  | int(11)       | NO   |     | NULL    |       |
| features    | varchar(64)   | NO   |     | NULL    |       |
| popularity  | int(11)       | NO   |     | NULL    |       |
+-------------+---------------+------+-----+---------+-------+
12 rows in set (0.00 sec)
```
