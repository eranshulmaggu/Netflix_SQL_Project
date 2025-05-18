# Netflix Movies and TV Shows Data Analysis using SQL
<img src="https://github.com/eranshulmaggu/Netflix_SQL_Project/blob/4fd16477fdc44b8e38a003a4e18c9ce58459e7c0/logo.png">

## Overview
This project involves a comprehensive analysis of Netflix's movies and TV shows data using SQL. The goal is to extract valuable insights and answer various business questions based on the dataset. The following README provides a detailed account of the project's objectives, business problems, solutions, findings, and conclusions.

## Objectives
* Analyze the distribution of content types (movies vs TV shows).
* Identify the most common ratings for movies and TV shows.
* List and analyze content based on release years, countries, and durations.
* Explore and categorize content based on specific criteria and keywords.

## Dataset
The data for this project is sourced from the Kaggle dataset:
* Dataset Link: [Movies Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows?resource=download)

## Schema

```
`DROP TABLE IF EXISTS NETFLIX1;
CREATE TABLE NETFLIX1
(
    show_id      VARCHAR(5),
    typess         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);
```

## Business Problems and Solutions

### 1. Count the number of Movies vs TV Shows

```
SELECT
    TYPESS, COUNT(*)
FROM NETFLIX1
GROUP BY TYPESS;
```

### 2. Find the most common rating for movies and TV shows

```
WITH CTE AS
    (
    SELECT TYPESS, RATING, COUNT(*) AS AVG_RATINGS
    FROM NETFLIX1
    GROUP BY TYPESS, RATING
    ),
CTE1 AS
    (
    SELECT TYPESS, RATING, RANK() OVER(PARTITION BY TYPESS ORDER BY AVG_RATINGS DESC) AS RANKING
    FROM CTE
    )
SELECT TYPESS, RATING, RANKING
FROM CTE1
WHERE RANKING = 1;
```

### 3. List all movies released in a specific year (e.g., 2020)

```
SELECT
    *
FROM NETFLIX1
WHERE RELEASE_YEAR = '2020'
    AND TYPESS = 'Movie';
```

### 4. Find the top 5 countries with the most content on Netflix

```
SELECT 
    UNNEST(STRING_TO_ARRAY(COUNTRY,','))AS COUNTRY_WISE,
    COUNT(SHOW_ID) AS MOST_CONTENT
FROM NETFLIX1
GROUP BY COUNTRY_WISE
ORDER BY MOST_CONTENT DESC
LIMIT 5;
```

### 5. Identify the longest movie

```
SELECT
    * FROM NETFLIX1
 WHERE  TYPESS = 'Movie'
    AND DURATION = (SELECT MAX(DURATION)FROM NETFLIX1) ;
```

### 6. Find content added in the last 5 years

```
SELECT
    * FROM NETFLIX1
WHERE TO_DATE(DATE_ADDED,'MONTH DD, YYYY')>= CURRENT_DATE - INTERVAL '5 YEARS';
```

### 7. Find all the movies/TV shows by director 'Rajiv Chilaka'!

```
SELECT *
FROM NETFLIX1
WHERE DIRECTOR ILIKE '%RAJIV CHILAKA%';
```

### 8. List all TV shows with more than 5 seasons

```
SELECT
    *
FROM NETFLIX1
WHERE TYPESS = 'TV Show'
    AND  SPLIT_PART (DURATION,' ',1)::INT > 5;
```

### 9. Count the number of content items in each genre

```
SELECT
    UNNEST(STRING_TO_ARRAY (LISTED_IN, ','))AS NEW_LIST,
    COUNT(SHOW_ID) AS TOTALCON 
FROM NETFLIX1
GROUP BY NEW_LIST;
```

### 10.Find each year and the average numbers of content release in India on Netflix. Return top 5 year with highest avg content release!

```
SELECT
    EXTRACT (YEAR FROM TO_DATE(DATE_ADDED, 'MONTH DD,YYYY'))AS YEARS, 
    COUNT(*), ROUND(COUNT(*):: NUMERIC /
    (
        SELECT COUNT(*)
        FROM NETFLIX1
        WHERE COUNTRY = 'India')* 100,2
    ) AS AVG_CONT
FROM NETFLIX1
WHERE COUNTRY = 'India'
GROUP BY YEARS 
ORDER BY AVG_CONT DESC
LIMIT 5;
```

### 11. List all movies that are documentaries

```
SELECT
    *
FROM NETFLIX1
WHERE LISTED_IN ILIKE '%DOCUMENTARIES%'
    AND TYPESS = 'Movie'
```

### 12. Find all content without a director

```
SELECT
    *
FROM NETFLIX1
WHERE DIRECTOR IS NULL;
```

### 13. Find how many movies actor 'Salman Khan' appeared in last 10 years!

```
SELECT
    *
FROM NETFLIX1
WHERE CASTS ILIKE '%SALMAN KHAN%'
    AND RELEASE_YEAR >= EXTRACT (YEAR FROM CURRENT_DATE) - 10;
```

### 14. Find the top 10 actors who have appeared in the highest number of movies produced in India.

```
SELECT
    UNNEST (STRING_TO_ARRAY(CASTS, ','))AS ACTORS, 
    COUNT(*) AS HIGHEST_NUMBER 
FROM NETFLIX1
WHERE COUNTRY ILIKE '%INDIA%'
GROUP BY ACTORS
ORDER BY HIGHEST_NUMBER DESC
LIMIT 10;
```

### 15.Categorize the content based on the presence of the keywords 'kill' and 'violence' in the description field. Label content containing these keywords as 'Bad' and all other content as 'Good'. Count how many items fall into each category.

```
WITH CTE AS (SELECT *, 
    CASE
        WHEN DESCRIPTION ILIKE '%KILL%' OR DESCRIPTION ILIKE '%VIOLENCE%' THEN 'BAD'
        ELSE 'GOOD'
        END AS CATEGORY
    FROM NETFLIX1)
SELECT
    CATEGORY, COUNT(*) AS TOTAL_MOVIES
FROM CTE
GROUP BY CATEGORY;
```


## Findings and Conclusion
* Content Distribution: The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
* Common Ratings: Insights into the most common ratings provide an understanding of the content's target audience.
* Geographical Insights: The top countries and the average content releases by India highlight regional content distribution.
* Content Categorization: Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.
* This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.

