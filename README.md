# SELECT-and-ye-shall-receive

## This repository contains two ipython notebooks exploring two different databases. I used python's sqlite3 package since the databases are quite small in size. Currently this is a demonstration of how one can ask and answer interesting questions using SQL. You can expect addition of vizualtions in the future.

**1. An economic guide to picking college majors**

The databse being accessed is titled "jobs.db". It contains a single table containing data from the American Community Survey 2010-2012 Public Use Microdata Series. (Attached in CSV format)

You can find metadata about the csv file here (See recent_grads.csv): https://github.com/fivethirtyeight/data/tree/master/college-majors

The notebook in itself demonstrates simple queries, each trying to utilise a fundamental SQL concept.

Sample queries:-

Q. Return the top 20 Majors where females were a minority
A. 
SELECT 
    Major as "Female minority majors"
FROM recent_grads
WHERE ShareWomen < 0.5
LIMIT 20;

Q. What major categories have at least 10% of the graduates doing low wage jobs? Order from lowest proportion to highest.
A.
SELECT 
    Major_category,
    (CAST(SUM(Low_wage_jobs) as Float)/CAST(SUM(Total) as Float)) as "Proportion"
FROM recent_grads
GROUP BY 1
HAVING Proportion > 0.1
ORDER BY 2;

Q. What proportion of majors have an above average share of women?
A.
SELECT 
    CAST(COUNT(Major) as Float)/CAST((SELECT COUNT(Major) FROM recent_grads) as Float) as "Proportion of all majors having an above average share of women"
FROM recent_grads
WHERE ShareWomen > (SELECT AVG(ShareWomen) FROM recent_grads);

**2. A subset of the pale blue dot**

The databse being accessed is titled "factbook_expanded.db". It contains two relevant tables titled "facts" and "cities" containing data from the CIA world factbook.

- The facts table contains important geographic and demographic data for each country.
- The cities table consists of the major urban areas for some countries present in the facts table.

Primary key in facts: id
Foreign key in cities: facts_id

You can find more information about the CIA world factbook here: https://www.cia.gov/library/publications/the-world-factbook/

The notebook demonstrates simple SQL concepts (upto joining two tables) and yet answers some interesting questions.

Sample queries:-

Q. Return each country and its capital city for the top 10 cities with the highest population.
A.
SELECT 
    ft.name as "Country",
    ct.name as "Capital city"
FROM facts as ft
INNER JOIN cities as ct
ON ft.id = ct.facts_id
WHERE ct.capital = 1
ORDER BY ft.migration_rate
LIMIT 10;

Q. Return Country, Capital city, and city population for all capital cities that have a population greater than 10,000,000. Limit to 5 rows and order by highest to lowest city population.
A.
SELECT 
    ft.name as "Country",
    tct.name as "City",
    tct.population as "City population"
FROM facts as ft
INNER JOIN 
    (SELECT 
        name,
        population,
        facts_id
    FROM cities 
    WHERE population > 10000000 AND capital = 1) 
    AS tct
ON ft.id = tct.facts_id
ORDER BY 3 DESC
LIMIT 5;


