

## Run services up
```bash
docker-compose up -d
```

## Create Persons table
```bash
docker exec -it <mysql container id> /bin/bash
mysql -u root -p # set password pass
CREATE DATABASE test;
CREATE TABLE test.persons (person_id VARCHAR(100) NOT NULL, first VARCHAR(100) NOT NULL, last VARCHAR(100) NOT NULL, age INT NOT NULL, PRIMARY KEY (person_id));
CREATE USER 'demouser'@'%' IDENTIFIED BY 'Password123!';
FLUSH PRIVILEGES;
GRANT ALL PRIVILEGES ON test.* to 'demouser'@'%';
FLUSH PRIVILEGES;
```

# Test
Using redis-cli perform:
```bash
redis-cli
> hset person:1 first_name foo last_name bar age 20  
OR  
> hset __{person:1} first_name foo last_name bar age 20
```

Make sure data reached MySql server:
```bash
docker exec -it <mysql container id> /bin/bash
mysql -u root -p # set password pass
mysql> select * from test.persons;
+-----------+-------+------+-----+
| person_id | first | last | age |
+-----------+-------+------+-----+
| 1         | foo   | bar  |  20 |
+-----------+-------+------+-----+
1 row in set (0.00 sec)

```
