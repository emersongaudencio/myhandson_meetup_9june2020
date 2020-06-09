# myhandson_meetup_9june2020
Performance Schema Tips and Tricks - MyHandsOn Meetup 9th June 2020

## Links and references:

### MySQL Performance Schema
* [MySQL 5.6 Performance Schema DOCS](https://dev.mysql.com/doc/refman/5.6/en/performance-schema.html)
#### reporting of memory consumption
- 177K per connection in 5.6 (multiplied by max_connections) with other settings default.

* [MySQL 5.6 Profiling with Performance Schema - Presentation by Oracle](aaaa)

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

### Tips - SYS Schema

* [Github MySQL SYS Schema](https://github.com/mysql/mysql-sys)

### Tips - MariaDB SYS Schema (not standard feature)

* [Github MariaDB SYS Schema](https://github.com/FromDual/mariadb-sys)
