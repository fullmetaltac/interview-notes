# Table of Contents
- [Table of Contents](#table-of-contents)
  - [0 SELECT basics](#0-select-basics)
  - [1 SELECT name](#1-select-name)
  - [2 SELECT from World](#2-select-from-world)
  - [3 SELECT from Nobel](#3-select-from-nobel)
  - [4 SELECT within SELECT](#4-select-within-select)
  - [5 SUM and COUNT](#5-sum-and-count)
  - [6 JOIN](#6-join)
  - [7 More JOIN operations](#7-more-join-operations)
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


**Find the capital and the name where the capital includes the name of the country.**

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, ' %') OR capital = name
```

**Find the capital and the name where the capital is an extension of name of the country.**

```sql
SELECT capital, name
FROM world
WHERE capital LIKE concat(name, ' %')
```

**Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.**

```sql
SELECT name, REPLACE(capital, name, '')
FROM world
WHERE capital LIKE concat(name, ' %')
```

## 2 SELECT from World

**Large Countries**

```sql
SELECT name FROM world
WHERE population >= 200000000
```

**Per capita GDP**

```sql
SELECT name, gdp / population FROM world
WHERE population >= 200000000
```

**South America In millions**

```sql
SELECT name, population / 1000000 FROM world
WHERE continent = 'South America'
```

**France, Germany, Italy**

```sql
SELECT name, population FROM world
WHERE name = 'France' OR name = 'Germany' OR name = 'Italy'
```

**United**

```sql
SELECT name FROM world
WHERE name LIKE '%United%'
```

**Two ways to be big**

```sql
SELECT name, population, area FROM world
WHERE population > 250000000 OR area > 3000000
```

**One or the other (but not both)**

```sql
SELECT name, population, area FROM world
WHERE (area > 3000000 AND population <= 250000000)
OR (area <= 3000000 AND population > 250000000)
```

**Rounding**

```sql
SELECT name,
ROUND(population / 1000000.0, 2),
ROUND(gdp / 1000000000.0, 2)
FROM world
WHERE continent = 'South America'
```

**Trillion dollar economies**

```sql
SELECT name, ROUND(gdp / population, -3)
FROM world
WHERE gdp > 1000000000000
```

**Name and capital have the same length**

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital)
```

**Matching name and capital**

```sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital
```

**All the vowels**

```sql
SELECT name
FROM world
WHERE name LIKE '%a%' 
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
AND name NOT LIKE '% %'
```

## 3 SELECT from Nobel

**Winners from 1950**

```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

**1962 Literature**

```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature'
```

**Albert Einstein**

```sql
SELECT yr, subject
  FROM nobel
WHERE winner = 'Albert Einstein'
```

**Recent Peace Prizes**

```sql
SELECT winner
FROM   nobel
WHERE  subject = 'peace'
       AND yr >= 2000 
```

**Literature in the 1980's**

```sql
SELECT yr,
       subject,
       winner
FROM   nobel
WHERE  subject = 'literature'
       AND yr >= 1980
       AND yr <= 1989 
```

**Only Presidents**

```sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt',
                 'Thomas Woodrow Wilson',
                 'Jimmy Carter',
                 'Barack Obama')
```

**John**

```sql
SELECT winner
FROM nobel
WHERE winner like 'John %'
```

**Chemistry and Physics from different years**

```sql
SELECT yr,
       subject,
       winner
FROM nobel
WHERE (yr = 1984
       AND subject = 'chemistry')
  OR (yr = 1980
      AND subject = 'physics')
```

**Exclude Chemists and Medics**

```sql
SELECT yr,
       subject,
       winner
FROM nobel
WHERE yr = 1980
  AND subject != 'chemistry'
  AND subject != 'medicine'
```

**Early Medicine, Late Literature**

```sql
SELECT yr,
       subject,
       winner
FROM nobel
WHERE yr = 1980
  AND subject != 'chemistry'
  AND subject != 'medicine'
  SELECT yr,
         subject,
         winner
  FROM nobel WHERE (subject = 'medicine'
                    AND yr < 1910)
  OR (yr >= 2004
      AND subject ='literature')
```

**Umlaut**

```sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```

**Apostrophe**

```sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O\'NEILL'
```

**Knights of the realm**

```sql
SELECT winner,
       yr,
       subject
FROM nobel
WHERE winner like 'Sir%'
ORDER BY yr DESC,
         winner
```

**Chemistry and Physics last**

```sql
SELECT winner,
       subject
FROM nobel
WHERE yr=1984
ORDER BY subject IN ('physics',
                     'chemistry'), subject,
                                   winner
```

## 4 SELECT within SELECT

**Bigger than Russia**

```sql
SELECT NAME
FROM   world
WHERE  population > (SELECT population
                     FROM   world
                     WHERE  NAME = 'Russia') 
```

**Richer than UK**

```sql
SELECT NAME
FROM   world
WHERE  gdp / population > (SELECT gdp / population
                           FROM   world
                           WHERE  NAME = 'United Kingdom')
       AND continent = 'Europe' 
```

**Neighbours of Argentina and Australia**

```sql
SELECT NAME,
       continent
FROM   world
WHERE  continent IN (SELECT continent
                     FROM   world
                     WHERE  NAME IN ( 'Argentina', 'Australia' ))
ORDER  BY NAME; 
```

**Between Canada and Poland**

```sql
SELECT NAME,
       population
FROM   world
WHERE  population < (SELECT population
                     FROM   world
                     WHERE  NAME = 'Germany')
       AND population > (SELECT population
                         FROM   world
                         WHERE  NAME = 'United Kingdom') 
```

**Percentages of Germany**

```sql
SELECT NAME,
       Concat(Round(population / (SELECT population
                                  FROM   world
                                  WHERE  NAME = 'Germany') * 100), "%") AS
       percentage
FROM   world
WHERE  continent = 'Europe' 
```

**Bigger than every country in Europe**

```sql
SELECT NAME
FROM   world
WHERE  gdp > (SELECT Max(gdp)
              FROM   world
              WHERE  continent = 'Europe'
                     AND gdp > 0) 
```

**Largest in each continent**

```sql
SELECT 
 w1.continent,
 w1.name,
 w1.area
FROM world AS w1
WHERE w1.area = (
  SELECT MAX(w2.area)
  FROM world AS w2
  WHERE w1.continent = w2.continent
  );
```

**First country of each continent (alphabetically)**

```sql
SELECT w1.continent,
       w1.NAME
FROM   world AS w1
WHERE  w1.NAME = (SELECT Min(w2.NAME)
                  FROM   world AS w2
                  WHERE  w1.continent = w2.continent); 
```

**Difficult Questions That Utilize Techniques Not Covered In Prior Sections**

```sql
SELECT NAME,
       continent,
       population
FROM   world
WHERE  continent IN (SELECT continent
                     FROM   world
                     GROUP  BY continent
                     HAVING Max(population) <= 25000000); 
```

**Three time bigger**

```sql
SELECT 
  w1.name,
  w1.continent
FROM world w1
WHERE w1.population / 3 > ALL (
  SELECT w2.population
  FROM world w2
  WHERE w1.continent = w2.continent
    AND w1.name <> w2.name
);
```

## 5 SUM and COUNT

**Total world population**

```sql
SELECT SUM(population)
FROM world
```

**List of continents**

```sql
SELECT DISTINCT continent
FROM   world 
```

**GDP of Africa**

```sql
SELECT SUM(gdp)
FROM   world
WHERE  continent = 'Africa' 
```

**Count the big countries**

```sql
SELECT COUNT(*)
FROM   world
WHERE  area >= 1000000 
```

**Baltic states population**

```sql
SELECT SUM(population)
FROM   world
WHERE  NAME IN ( 'Estonia', 'Latvia', 'Lithuania' ) 
```

**Counting the countries of each continent**
```sql
SELECT continent,
       COUNT(NAME)
FROM   world
GROUP  BY continent; 
```

**Counting big countries in each continent**

```sql
SELECT continent,
       COUNT(NAME)
FROM   world
WHERE  population >= 10000000
GROUP  BY continent 
```

**Counting big continents**

```sql
SELECT continent
FROM   world
GROUP  BY continent
HAVING Sum(population) >= 100000000 
```

## 6 JOIN

**Show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'**

```sql
SELECT matchid,
       player
FROM   goal
WHERE  teamid = 'GER' 
```

**Show id, stadium, team1, team2 for just game 1012.**

```sql
SELECT id,
       stadium,
       team1,
       team2
FROM   game
WHERE  id = 1012 
```

**Show the player, teamid, stadium and mdate for every German goal.**

```sql
SELECT player,
       teamid,
       stadium,
       mdate
FROM   game
       JOIN goal
         ON ( id = matchid )
WHERE  teamid = 'GER' 
```

**Show the team1, team2 and player for every goal scored by a player called Mario player LIKE 'Mario%'**

```sql
SELECT team1,
       team2,
       player
FROM   game
       JOIN goal
         ON id = matchid
WHERE  player LIKE 'Mario%' 
```


**Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10**

```sql
SELECT player,
       teamid,
       coach,
       gtime
FROM   goal
       JOIN eteam
         ON teamid = id
WHERE  gtime <= 10 
```

**List the dates of the matches and the name of the team in which ‘Fernando Santos’ was the team1 coach.**

```sql
SELECT mdate,
       teamname
FROM   game
       JOIN eteam
         ON ( team1 = eteam.id )
WHERE  eteam .coach = 'Fernando Santos' 
```

**List the player for every goal scored in a game where the stadium was ‘National Stadium, Warsaw’.**

```sql
SELECT player
FROM   game
       JOIN goal
         ON ( id = matchid )
WHERE  stadium = 'National Stadium, Warsaw' 
```

**Show the name of all players who scored a goal against Germany.**

```sql
SELECT DISTINCT player
FROM   game
       JOIN goal
         ON matchid = id
WHERE  teamid <> 'GER'
       AND ( team1 = 'GER'
              OR team2 = 'GER' ) 
```

**Show teamname and the total number of goals scored.**

```sql
SELECT eteam.teamname,
       COUNT(*) AS goals
FROM   eteam
       JOIN goal
         ON ( id = teamid )
GROUP  BY eteam.teamname 
```

**Show the stadium and the number of goals scored in each stadium.**

```sql
SELECT stadium,
       COUNT(*) AS goals
FROM   game
       JOIN goal
         ON id = matchid
GROUP  BY stadium 
```

**For every match involving ‘POL’, show the matchid, date and the number of goals scored.**

```sql
SELECT matchid,
       mdate,
       COUNT(*) AS goals
FROM   game
       JOIN goal
         ON matchid = id
WHERE  ( team1 = 'POL'
          OR team2 = 'POL' )
GROUP  BY matchid,
          mdate 
```

**For every match where ‘GER’ scored, show matchid, match date and the number of goals scored by ‘GER’.**

```sql
SELECT matchid,
       mdate,
       COUNT(*) AS goals
FROM   game
       JOIN goal
         ON matchid = id
WHERE  ( team1 = 'GER'
          OR team2 = 'GER' )
       AND teamid = 'GER'
GROUP  BY matchid,
          mdate 
```

**List every match with the goals scored by each team as shown. Sort your result by mdate, matchid, team1 and team2.**

```sql
SELECT game.mdate,
       game.team1,
       SUM(CASE
             WHEN goal.teamid = game.team1 THEN 1
             ELSE 0
           end) AS score1,
       game.team2,
       SUM(CASE
             WHEN goal.teamid = game.team2 THEN 1
             ELSE 0
           end) AS score2
FROM   game
       LEFT JOIN goal
              ON matchid = id
GROUP  BY game.id,
          game.mdate,
          game.team1,
          game.team2
ORDER  BY mdate,
          matchid,
          team1,
          team2 
```

## 7 More JOIN operations

**1962 movies**

```sql
SELECT id,
       title
FROM   movie
WHERE  yr = 1962
       AND budget > 2000000 
```

**When was Citizen Kane released?**

```sql
SELECT yr
FROM   movie
WHERE  title = 'Citizen Kane' 
```

**Star Trek movies**
```sql
SELECT id,
       title,
       yr
FROM   movie
WHERE  title LIKE 'Star Trek%'
ORDER  BY yr 
```


**id for actor Glenn Close**

```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close';
```

**id for Casablanca**

```sql
SELECT id 
FROM movie
WHERE title= 'Casablanca' and yr = 1942
```

**Cast list for Casablanca**

```sql

```

## References
- https://sqlzoo.net/wiki/SQL_Tutorial