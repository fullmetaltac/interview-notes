# Table of Contents
- [Table of Contents](#table-of-contents)
  - [0 SELECT basics](#0-select-basics)
  - [1 SELECT name](#1-select-name)
  - [References](#references)



## 0 SELECT basics

**Introducing the world table of countries**

```sql
SELECT population FROM world
WHERE name = 'Germany'
```

**Scandinavia**

```sql
SELECT name, population FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

**Just the right size**

```sql
SELECT name, area FROM world
WHERE area BETWEEN 200000 AND 250000
```

## 1 SELECT name

**Find the country that start with Y**

```sql
SELECT name FROM world
WHERE name LIKE 'Y%'
```

**Find the countries that end with y**

```sql
SELECT name FROM world
WHERE name LIKE '%y'
```

**Find the countries that contain the letter x**

```sql
SELECT name FROM world
WHERE name LIKE '%x%'
```

**Find the countries that end with land**

```sql
SELECT name FROM world
WHERE name LIKE '%land'
```

**Find the countries that start with C and end with ia**

```sql
SELECT name FROM world
WHERE name LIKE 'C%ia'
```

**Find the country that has oo in the name**

```sql
SELECT name FROM world
WHERE name LIKE '%oo%'
```

**Find the countries that have three or more a in the name**

```sql
SELECT name FROM world
WHERE name LIKE '%a%a%a%'
```

**Find the countries that have "t" as the second character.**

```sql
SELECT name FROM world
WHERE name LIKE '_t%'
ORDER BY name
```

**Find the countries that have two "o" characters separated by two others.**

```sql
SELECT name FROM world
WHERE name LIKE '%o__o%'
```

**Find the countries that have exactly four characters.**

```sql
SELECT name FROM world
WHERE name LIKE '____'
```

**Find the country where the name is the capital city.**

```sql
SELECT name
FROM world
WHERE name = capital
```

**Find the country where the capital is the country plus "City".**

```sql
SELECT name
FROM world
WHERE capital LIKE concat(name, ' City')
```

## References
- https://sqlzoo.net/wiki/SQL_Tutorial