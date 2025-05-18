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
`ROP TABLE IF EXISTS netflix;
CREATE TABLE netflix
(
    show_id      VARCHAR(5),
    type         VARCHAR(10),
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


```

### 3. Find the most common rating for movies and TV shows

```


```

### 4. List all movies released in a specific year (e.g., 2020)

```


```

### 5. Find the top 5 countries with the most content on Netflix

```


```

### 6. Identify the longest movie

```


```

### 7. Find content added in the last 5 years

```


```

### 8. Find all the movies/TV shows by director 'Rajiv Chilaka'!

```


```

### 9. List all TV shows with more than 5 seasons

```


```

### 10. Count the number of content items in each genre

```


```

### 10.Find each year and the average numbers of content release in India on Netflix. Return top 5 year with highest avg content release!

```


```

### 11. List all movies that are documentaries

```


```

### 12. Find all content without a director

```


```

### 13. Find how many movies actor 'Salman Khan' appeared in last 10 years!

```


```

### 14. Find the top 10 actors who have appeared in the highest number of movies produced in India.

```


```

### 15.Categorize the content based on the presence of the keywords 'kill' and 'violence' in the description field. Label content containing these keywords as 'Bad' and all other content as 'Good'. Count how many items fall into each category.

## Findings and Conclusion
* Content Distribution: The dataset contains a diverse range of movies and TV shows with varying ratings and genres.
* Common Ratings: Insights into the most common ratings provide an understanding of the content's target audience.
* Geographical Insights: The top countries and the average content releases by India highlight regional content distribution.
* Content Categorization: Categorizing content based on specific keywords helps in understanding the nature of content available on Netflix.
* This analysis provides a comprehensive view of Netflix's content and can help inform content strategy and decision-making.

