# <p align="center">Netflix Shows and Movies </p>
# <p align="center">![Pic](https://i.pcmag.com/imagery/reviews/05cItXL96l4LE9n02WfDR0h-5.fit_scale.size_760x427.v1582751026.png)</p>

**Tools Used:** Excel, MySQL, Tableau

[Datasets Used](https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv)

[SQL Analysis (Code)](https://github.com/SharifAthar/Netflix-Shows-and-Movies-SQL/blob/main/Netflix_SQL_Analysis.sql)

[Netflix Dashboard - Tableau](https://public.tableau.com/app/profile/sharif.athar/viz/NetflixShowsMoviesDashboard/Dashboard1)

- **Business Problem:** Netflix wants to gather useful insights on their shows and movies for their subscribers through their datasets. The issue is, they are working with too much data (approximately 82k rows of data combined) and are unsure how to effectively analyze and extract meaningful insights from it. They need a robust and scalable data analytics solution to handle the vast amount of data and uncover valuable patterns and trends.

- **How I Plan On Solving the Problem:** In helping Netflix gather valuable insights from their extensive movies and shows dataset, I will be utilizing SQL and a data visualization tool like Tableau to extract relevant information, and conduct insightful analyses. By leveraging SQL's functions, I can uncover key metrics such as viewer ratings, popularity trends, genre preferences, and viewership patterns. Once the data has been extracted and prepared, I will leverage Tableau to present the findings. This will allow for interactive exploration of the data, enabling stakeholders at Netflix to gain actionable insights through visually appealing charts, graphs, and interactive visualizations. I plan on creating a dynamic dashboard in Tableau that enables users to delve into specific movie genres, viewer demographics, or geographical regions.

## Questions I Wanted To Answer From the Dataset:

## 1. Which movies and shows on Netflix ranked in the top 10 and bottom 10 based on their IMDB scores?
- Top 10 Movies
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'MOVIE'
ORDER BY imdb_score DESC
LIMIT 10
```
Result: 

![Q1](https://i.ibb.co/6mQWCw9/Screen-Shot-2023-07-09-at-9-38-11-PM.png)

- Top 10 Shows
```mysql
SELECT title, 
type, 
imdb_score
FROM shows_movies.titles
WHERE imdb_score >= 8.0
AND type = 'SHOW'
ORDER BY imdb_score DESC
LIMIT 10
```
Result: 

![Q2](https://i.ibb.co/QppHsN2/Screen-Shot-2023-07-09-at-9-45-58-PM.png)





## 2. How many movies and shows fall in each decade in Netflix's library?
```mysql
SELECT CONCAT(FLOOR(release_year / 10) * 10, 's') AS decade,
	COUNT(*) AS movies_shows_count
FROM shows_movies.titles
WHERE release_year >= 1940
GROUP BY CONCAT(FLOOR(release_year / 10) * 10, 's')
ORDER BY decade;
```
Result: 

![Q5](https://i.ibb.co/8dTzVZ3/Screen-Shot-2023-07-09-at-10-02-18-PM.png)


## 3. How did age-certifications impact the dataset?
```mysql
SELECT DISTINCT age_certification, 
ROUND(AVG(imdb_score),2) AS avg_imdb_score,
ROUND(AVG(tmdb_score),2) AS avg_tmdb_score
FROM shows_movies.titles
GROUP BY age_certification
ORDER BY avg_imdb_score DESC
```
Result: 

![Q6](https://i.ibb.co/SvJyjgF/Screen-Shot-2023-07-09-at-10-16-52-PM.png)

```mysql
SELECT age_certification, 
COUNT(*) AS certification_count
FROM shows_movies.titles
WHERE type = 'Movie' 
AND age_certification != 'N/A'
GROUP BY age_certification
ORDER BY certification_count DESC
LIMIT 5;
```
Results: 

![Q7](https://i.ibb.co/T0f5cNq/Screen-Shot-2023-07-09-at-10-20-23-PM.png)



## 4. Which genres are the most common? 
- Top 10 most common genres for MOVIES
```mysql
SELECT genres, 
COUNT(*) AS title_count
FROM shows_movies.titles 
WHERE type = 'Movie'
GROUP BY genres
ORDER BY title_count DESC
LIMIT 10;
```
Result:

![Q8](https://i.ibb.co/VWrgd8m/Screen-Shot-2023-07-10-at-12-25-40-PM.png)

- Top 10 most common genres for SHOWS
```mysql
SELECT genres, 
COUNT(*) AS title_count
FROM shows_movies.titles 
WHERE type = 'Show'
GROUP BY genres
ORDER BY title_count DESC
LIMIT 10;
```
Result: 

![Q9](https://i.ibb.co/P59s4X7/Screen-Shot-2023-07-10-at-12-27-41-PM.png)

- Top 3 most common genres OVERALL
```mysql
SELECT t.genres, 
COUNT(*) AS genre_count
FROM shows_movies.titles AS t
WHERE t.type = 'Movie' or t.type = 'Show'
GROUP BY t.genres
ORDER BY genre_count DESC
LIMIT 3;
```
Result: 

![Q10](https://i.ibb.co/qMvMBGf/Screen-Shot-2023-07-10-at-12-30-04-PM.png)


