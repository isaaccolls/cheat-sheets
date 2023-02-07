- [sql](#sql)
- [postgresql](#postgresql)
- [mysql](#mysql)

# sql

## show tables

```sql
SHOW TABLES FROM database_name;
SHOW TABLES LIKE pattern;
SHOW TABLES LIKE 'permissions%';
```

## create a new table

```sql
CREATE TABLE table_name(
  id INT(11) AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(50),
  email VARCHAR(50),
  register_date DATE,
);
```

## fetch data from table

```sql
SELECT * FROM table_name WHERE id=420;
SELECT * FROM table_name WHERE name='marielis';
SELECT * FROM table_name WHERE name like '%marielis%';
```

## update data

```sql
UPDATE table_name SET name='marielis' WHERE email='marielis@email.com';
```

## delete table

```sql
SET FOREIGN_KEY_CHECKS = 0;
DROP TABLE table_name;
SET FOREIGN_KEY_CHECKS = 1;
```

## delete database

```sql
DROP DATABASE db_name;
```

## joins

### inner join

Use a inner join when you want data belonging to both tables. The data must be present in both tables for it to be shown in rows returned (null values skipped)

```sql
SELECT * FROM TableA a LEFT JOIN TableB b on a.id = b.id;
```

### right outer join

To det all the data from table B and the shared data from table A Use this when you want all values returned even null values from the right side table (tableB)

```sql
SELECT * FROM TableA a RIGHT JOIN TableB b on a.id = b.id;
```

### full outer join

To get all the data back from table A and table B, even the null values from both sides that have no matches to the other side

```sql
SELECT * FROM TableA a FULL OUTER JOIN TableB b ON a.id = b.id;
```

## find some foreign key

```sql
SELECT
  REFERENCED_TABLE_SCHEMA, TABLE_NAME,COLUMN_NAME,CONSTRAINT_NAME, REFERENCED_TABLE_NAME,REFERENCED_COLUMN_NAME
FROM
  INFORMATION_SCHEMA.KEY_COLUMN_USAGE
WHERE
CONSTRAINT_NAME like 'FK_e%'
```

### delete it

```sql
alter table `template_manager_2`.`section_positions` drop foreign key FK_e718991059d15956316121485fb;
```

# postgresql

- install: `sudo apt-get install postgresql-10 postgresql-contrib`
- check version: `psql --version` `psql -v`
- start the database server: `/usr/lib/postgresql/10/bin/pg_ctl -D /var/lib/postgresql/10/main -l logfile start` (check it 🤔)
- _set password_ to user postgresql `sudo -u postgres psql postgres`

## assign user and password

```bash
sudo -u postgres psql -c "ALTER USER postgres PASSWORD 'postgres';"
sudo -u postgres psql -c "CREATE DATABASE testdb;"
```

## start automatically on boot

```
sudo systemctl enable [SERVICE]
sudo systemctl enable postgresql
```

## manage daemon

```bash
sudo service postgresql start
sudo service postgresql stop
sudo service postgresql status
```

## pgadmin

- install `sudo apt-get install pgadmin3`

# mysql

- install: `apt-get install mysql-client`
- log in: `mysql -u root -h 127.0.0.1 -p12345678`
- show databases: `show databases;`
- create database: `create database db_name;`
- acces/use a database: `USE db_name;`
- check tables: `SHOW tables;`
- processlist : `SHOW PROCESSLIST;`
  - kill one: `KILL [id]`
