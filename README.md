# myhandson_meetup_9june2020
Performance Schema Tips and Tricks - MyHandsOn Meetup 9th June 2020

## Links and references:

### MySQL Performance Schema
* [MySQL 5.6 Performance Schema DOCS](https://dev.mysql.com/doc/refman/5.6/en/performance-schema.html)
#### reporting of memory consumption

 - 177K per connection in 5.6 (multiplied by max_connections) with other settings default.

* [MySQL 5.6 Profiling with Performance Schema - Presentation by Oracle](https://github.com/emersongaudencio/myhandson_meetup_9june2020/blob/master/profiling_with_performance_schema.pdf)

* [MySQL 5.7 Performance Schema DOCS](https://dev.mysql.com/doc/refman/5.7/en/performance-schema.html)
#### reporting of memory consumption

 - 177K per connection in 5.7 (multiplied by max_connections) with other settings default.

* [MySQL 8.0 Performance Schema DOCS](https://dev.mysql.com/doc/refman/8.0/en/performance-schema.html)
#### reporting of memory consumption

 - 177K per connection in 8.0 (multiplied by max_connections) with other settings default.

### MariaDB Performance Schema (Based on MySQL 5.6 instrumentations)
* [MariaDB Performance Schema](https://mariadb.com/kb/en/performance-schema/)

* [MariaDB 10.4 is using too much memory - Bug Report](https://jira.mariadb.org/browse/MDEV-20216)
#### reporting of memory consumption

 - 177K per connection in 10.1 (multiplied by max_connections) with other settings default.

 - 177K per connection in 10.2 (multiplied by max_connections) with other settings default.

 - 177K per connection in 10.3 (multiplied by max_connections) with other settings default.

 - 250K per connection in 10.4 (multiplied by max_connections) with other settings default.

### Performance Schema / Memory Footprint
* [Link - Performance Schema / Memory Footprint](https://github.com/nethalo/mysql-tools/blob/master/Performance_Schema_Memory_Footprint.md)

### Tips - SYS Schema

* [Github MySQL SYS Schema](https://github.com/mysql/mysql-sys)

 - Learn from the source code (how they read data from Performance Schema)

### Tips - MariaDB SYS Schema (not standard feature)

* [Github MariaDB SYS Schema](https://github.com/FromDual/mariadb-sys)

 - Learn from the source code (how they read data from Performance Schema)

#### Main instruments:
 - 1. Stage
 - 2. Statement
 - 3. Statement Digest
 - 4. Wait

#### Instruments in 5.7 and 8.0:
 - 5. Memory
 - 6. Replication
 - 7. Transactions

#### Consumers
 - 1. Events (based on instruments which it is own filter layer)

#### Actors
 - 1. Users (mysql users)
 - 2. hosts

#### Objects
 - 1. Schema
 - 2. Tables

#### Timers
 - 1. Numeric precision related to time numbers used on the instruments

### Default Consumers
* MySQL 5.7 and 8.0

```
(root@localhost) MySQL[performance_schema]> SELECT * FROM performance_schema.setup_consumers;
+----------------------------------+---------+
| NAME                             | ENABLED |
+----------------------------------+---------+
| events_stages_current            | YES     |
| events_stages_history            | YES     |
| events_stages_history_long       | YES     |
| events_statements_current        | YES     |
| events_statements_history        | YES     |
| events_statements_history_long   | NO      |
| events_transactions_current      | NO      |
| events_transactions_history      | NO      |
| events_transactions_history_long | NO      |
| events_waits_current             | NO      |
| events_waits_history             | NO      |
| events_waits_history_long        | NO      |
| global_instrumentation           | YES     |
| thread_instrumentation           | YES     |
| statements_digest                | YES     |
+----------------------------------+---------+
15 rows in set (0.00 sec)
```

* MariaDB and MySQL 5.6

```
(root@localhost) MariaDB [performance_schema]> SELECT * FROM performance_schema.setup_consumers;
+--------------------------------+---------+
| NAME                           | ENABLED |
+--------------------------------+---------+
| events_stages_current          | YES     |
| events_stages_history          | YES     |
| events_stages_history_long     | YES     |
| events_statements_current      | YES     |
| events_statements_history      | NO      |
| events_statements_history_long | NO      |
| events_waits_current           | NO      |
| events_waits_history           | NO      |
| events_waits_history_long      | NO      |
| global_instrumentation         | YES     |
| thread_instrumentation         | YES     |
| statements_digest              | YES     |
+--------------------------------+---------+
12 rows in set (0.001 sec)
```

### Default Actors
* MySQL 5.7 and 8.0

```
(root@localhost) MySQL[performance_schema]> select * from setup_actors;
+------+------+------+---------+---------+
| HOST | USER | ROLE | ENABLED | HISTORY |
+------+------+------+---------+---------+
| %    | %    | %    | YES     | YES     |
+------+------+------+---------+---------+
1 row in set (0.00 sec)
```

* MariaDB and MySQL 5.6

```
(root@localhost) MariaDB [performance_schema]> select * from setup_actors;
+------+------+------+
| HOST | USER | ROLE |
+------+------+------+
| %    | %    | %    |
+------+------+------+
1 row in set (0.002 sec)
```

### Default Objects
* MySQL 5.7 and 8.0

```
(root@localhost) MySQL[performance_schema]> select * from setup_objects;
+-------------+--------------------+-------------+---------+-------+
| OBJECT_TYPE | OBJECT_SCHEMA      | OBJECT_NAME | ENABLED | TIMED |
+-------------+--------------------+-------------+---------+-------+
| EVENT       | mysql              | %           | NO      | NO    |
| EVENT       | performance_schema | %           | NO      | NO    |
| EVENT       | information_schema | %           | NO      | NO    |
| EVENT       | %                  | %           | YES     | YES   |
| FUNCTION    | mysql              | %           | NO      | NO    |
| FUNCTION    | performance_schema | %           | NO      | NO    |
| FUNCTION    | information_schema | %           | NO      | NO    |
| FUNCTION    | %                  | %           | YES     | YES   |
| PROCEDURE   | mysql              | %           | NO      | NO    |
| PROCEDURE   | performance_schema | %           | NO      | NO    |
| PROCEDURE   | information_schema | %           | NO      | NO    |
| PROCEDURE   | %                  | %           | YES     | YES   |
| TABLE       | mysql              | %           | NO      | NO    |
| TABLE       | performance_schema | %           | NO      | NO    |
| TABLE       | information_schema | %           | NO      | NO    |
| TABLE       | %                  | %           | YES     | YES   |
| TRIGGER     | mysql              | %           | NO      | NO    |
| TRIGGER     | performance_schema | %           | NO      | NO    |
| TRIGGER     | information_schema | %           | NO      | NO    |
| TRIGGER     | %                  | %           | YES     | YES   |
+-------------+--------------------+-------------+---------+-------+
20 rows in set (0.00 sec)
```

* MariaDB and MySQL 5.6

```
(root@localhost) MariaDB [performance_schema]> select * from setup_objects;
+-------------+--------------------+-------------+---------+-------+
| OBJECT_TYPE | OBJECT_SCHEMA      | OBJECT_NAME | ENABLED | TIMED |
+-------------+--------------------+-------------+---------+-------+
| TABLE       | mysql              | %           | NO      | NO    |
| TABLE       | performance_schema | %           | NO      | NO    |
| TABLE       | information_schema | %           | NO      | NO    |
| TABLE       | %                  | %           | YES     | YES   |
+-------------+--------------------+-------------+---------+-------+
4 rows in set (0.000 sec)
```

### Default Instruments

* MySQL 5.7

```
(root@localhost) MySQL[performance_schema]> select count(1) from setup_instruments;
+----------+
| count(1) |
+----------+
|     1021 |
+----------+
1 row in set (0.00 sec)
```

* MySQL 8.0

```
(root@localhost) MySQL[performance_schema]> select count(1) from setup_instruments;
+----------+
| count(1) |
+----------+
|     1208 |
+----------+
1 row in set (0.01 sec)
```

* MariaDB 10.3

```
(root@localhost) MariaDB [performance_schema]> select count(1) from setup_instruments;
+----------+
| count(1) |
+----------+
|      712 |
+----------+
1 row in set (0.000 sec)
```

* MariaDB 10.4

```
(root@localhost) MariaDB [performance_schema]> select count(1) from setup_instruments;
+----------+
| count(1) |
+----------+
|      719 |
+----------+
1 row in set (0.003 sec)
```
