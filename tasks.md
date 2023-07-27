# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

```sql
SELECT * FROM matches WHERE season = 2017;


```

2) Find all the matches featuring Barcelona.

```sql
SELECT * FROM matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona'; 


```

3) What are the names of the Scottish divisions included?

```sql
 SELECT name FROM divisions WHERE country = 'Scotland'; 

Scottish Premiership
Scottish Championship
Scottish League One


```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

```sql
SELECT code FROM divisions WHERE name = 'Bundesliga';
SELECT division_code, COUNT(*) FROM matches WHERE hometeam = 'Freiburg' OR awayteam = 'Freiburg'  GROUP BY division_code; 

SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');

count = 374


```

5) Find the teams which include the word "City" in their name. 

```sql
SELECT awayteam FROM matches WHERE LOWER(awayteam) LIKE LOWER ('%City%') GROUP BY awayteam; 
or can do 
SELECT DISTINCT awayteam FROM matches WHERE LOWER(awayteam) LIKE LOWER ('%City%'); -- this does not retain any of the underlying information but the first solution does
Bath City
Man City
Edinburgh City
Bristol City


```

6) How many different teams have played in matches recorded in a French division?

```sql
SELECT code FROM divisions WHERE country = 'France';
SELECT COUNT(*) FROM (SELECT hometeam FROM matches WHERE division_code = 'F1' OR division_code = 'F2' GROUP BY hometeam) I

OR TAREK'S SOLUTION 
SELECT COUNT(*) FROM (SELECT DISTINCT matches.hometeam FROM divisions JOIN matches ON divisions.code=matches.division_code AND divisions.country = 'France') I

or LAB REVIEW 
SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division_code IN ()'F1', 'F2')

so the answer is 61


```

7) Have Huddersfield played Swansea in any of the recorded matches?

```sql
SELECT * FROM matches WHERE hometeam = 'Huddersfield' AND awayteam = 'Swansea' OR hometeam = 'Swansea' AND awayteam = 'Huddersfield';

Yes - returns 12 matches

```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

```sql
SELECT code FROM divisions WHERE name = 'Eredivisie';
SELECT COUNT(id) FROM matches WHERE division_code = 'N1' AND season BETWEEN 2010 AND 2015 AND ftr = 'D';

answer = 431

```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
SELECT code FROM divisions WHERE name = 'Premier League';
SELECT * FROM matches WHERE division_code = 'E0' ORDER BY (fthg + ftag) DESC, fthg DESC;


```

10) In which division and which season were the most goals scored?
```sql
SELECT division_code, season FROM matches ORDER BY (fthg + ftag) DESC, fthg DESC LIMIT 1;
SELECT name FROM divisions WHERE code = 'N1';

Eredivisie and 2021

```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)