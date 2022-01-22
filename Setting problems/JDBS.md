#### **Prepare in terminal**

```bash
$ mysql -u root -p

mysql> create database met520;

show databases;

use met520;

create table HW5 (bullet_point VARCHAR(20), category VARCHAR(100), category_url VARCHAR(200), clickthrough_url VARCHAR(200), close_date DATE, currency VARCHAR(20));

show tables;

describe HW5;
```

#### Prepare in Eclipse

Add mysql-connector-java

Project -> property -> java build path ->libraries -> Add external JARs



Get the year from the date: year()

"select * from HW5 where year(close_date) = '"+date+"'"