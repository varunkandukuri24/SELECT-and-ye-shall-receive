# SELECT-and-ye-shall-receive

#### This repository contains two ipython notebooks exploring two different databases. I used python's sqlite3 package since the databases are quite small in size. Currently this is a demonstration of how one can ask and answer interesting questions using SQL. You can expect addition of vizualtions in the future.

**1. An economic guide to picking college majors**

The databse being accessed is titled "jobs.db". It contains a single table containing data from the American Community Survey 2010-2012 Public Use Microdata Series. (Attached in CSV format)

You can find metadata about the csv file here (See recent_grads.csv): https://github.com/fivethirtyeight/data/tree/master/college-majors

The notebook in itself demonstrates simple queries, each trying to utilise a fundamental SQL concept.


**2. A subset of the pale blue dot**

The databse being accessed is titled "factbook_expanded.db". It contains two relevant tables titled "facts" and "cities" containing data from the CIA world factbook.

- The facts table contains important geographic and demographic data for each country.
- The cities table consists of the major urban areas for some countries present in the facts table.

Primary key in facts: id
Foreign key in cities: facts_id

You can find more information about the CIA world factbook here: https://www.cia.gov/library/publications/the-world-factbook/

The notebook demonstrates simple SQL concepts (upto joining two tables) and yet answers some interesting questions.
