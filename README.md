# <p align="center">Netflix Shows and Movies Analysis</p>

<p align="center">![Netflix](https://i.ibb.co/Q81WwRN/92399716.jpg)</p>

### **Tools Utilized:** Excel, MySQL, Tableau

[Dataset Reference](https://www.kaggle.com/datasets/victorsoeiro/netflix-tv-shows-and-movies?select=titles.csv)  
[SQL Analysis Code](https://github.com/SharifAthar/Netflix-Shows-and-Movies-SQL/blob/main/Netflix_SQL_Analysis.sql)  
[Tableau Dashboard](https://public.tableau.com/app/profile/sharif.athar/viz/NetflixShowsMoviesDashboard/Dashboard1)

### **Project Overview:**  
Netflix possesses an extensive dataset containing approximately 82,000 records related to their movies and TV shows. The challenge lies in effectively analyzing this vast information to extract valuable insights that enhance user experience. The goal is to develop a scalable analytics solution to identify meaningful trends, popular content, and user preferences.

### **Approach to Solving the Problem:**  
To derive insights from Netflix’s dataset, SQL was used for data extraction and processing, while Tableau helped in visualizing key trends. SQL queries facilitated the identification of metrics such as IMDB ratings, genre popularity, and content distribution across decades. Tableau was then utilized to create interactive dashboards, allowing stakeholders to explore trends dynamically. This visualization enables Netflix to refine its content strategy, catering to viewer preferences effectively.

## **Key Questions Addressed:**

### **1. What Are the Top and Bottom 10 Movies and Shows Based on IMDB Scores?**

#### **Top 10 Movies:**
```mysql
SELECT title, type, imdb_score FROM shows_movies.titles
WHERE imdb_score >= 8.0 AND type = 'MOVIE'
ORDER BY imdb_score DESC
LIMIT 10;
```
#### **Top 10 Shows:**
```mysql
SELECT title, type, imdb_score FROM shows_movies.titles
WHERE imdb_score >= 8.0 AND type = 'SHOW'
ORDER BY imdb_score DESC
LIMIT 10;
```
#### **Bottom 10 Movies:**
```mysql
SELECT title, type, imdb_score FROM shows_movies.titles
WHERE type = 'MOVIE'
ORDER BY imdb_score ASC
LIMIT 10;
```
#### **Bottom 10 Shows:**
```mysql
SELECT title, type, imdb_score FROM shows_movies.titles
WHERE type = 'SHOW'
ORDER BY imdb_score ASC
LIMIT 10;
```
Analyzing IMDB scores offers insight into highly regarded and poorly received content. Top-ranked titles reflect quality production and strong audience reception, while low-rated titles suggest areas for improvement due to factors like weak storytelling or subpar acting.

### **2. How Are Movies and Shows Distributed Across Different Decades?**
```mysql
SELECT CONCAT(FLOOR(release_year / 10) * 10, 's') AS decade, COUNT(*) AS count
FROM shows_movies.titles
WHERE release_year >= 1940
GROUP BY decade
ORDER BY decade;
```
Results indicate that content availability significantly increased post-2000, with the 2010s and 2020s featuring the highest number of movies and shows. This shift underscores Netflix’s focus on contemporary content, aligning with evolving audience interests.

### **3. How Does Age Certification Influence IMDB and TMDB Scores?**
```mysql
SELECT age_certification, ROUND(AVG(imdb_score),2) AS avg_imdb,
ROUND(AVG(tmdb_score),2) AS avg_tmdb
FROM shows_movies.titles
GROUP BY age_certification
ORDER BY avg_imdb DESC;
```
```mysql
SELECT age_certification, COUNT(*) AS count
FROM shows_movies.titles
WHERE type = 'Movie' AND age_certification != 'N/A'
GROUP BY age_certification
ORDER BY count DESC
LIMIT 5;
```
TV-14 content received the highest IMDB ratings, suggesting it resonates well with audiences. R-rated and PG-13 movies dominate Netflix’s library, highlighting the platform’s focus on mature content. The presence of family-friendly (G, PG) content ensures a well-rounded collection.

### **4. What Are the Most Common Genres?**
#### **Most Popular Movie Genres:**
```mysql
SELECT genres, COUNT(*) AS count
FROM shows_movies.titles
WHERE type = 'Movie'
GROUP BY genres
ORDER BY count DESC
LIMIT 10;
```
#### **Most Popular Show Genres:**
```mysql
SELECT genres, COUNT(*) AS count
FROM shows_movies.titles
WHERE type = 'Show'
GROUP BY genres
ORDER BY count DESC
LIMIT 10;
```
#### **Top 3 Genres Overall:**
```mysql
SELECT genres, COUNT(*) AS count
FROM shows_movies.titles
WHERE type IN ('Movie', 'Show')
GROUP BY genres
ORDER BY count DESC
LIMIT 3;
```
Comedy emerged as the most dominant genre, followed by documentation and drama. The presence of hybrid genres (e.g., comedy + drama) indicates a demand for diverse storytelling styles.

### **Conclusion:**
By examining Netflix’s dataset through SQL queries and visualizations, several key trends emerged:
- **IMDB Scores:** High-rated titles guide users toward quality content, while poorly rated ones highlight improvement areas.
- **Content Across Decades:** A significant increase in titles post-2000 indicates Netflix’s focus on recent productions.
- **Age Certification Impact:** TV-14, R, and PG-13 dominate, with these categories generally receiving higher ratings.
- **Genre Popularity:** Comedy leads Netflix’s content landscape, followed by documentation and drama, demonstrating a preference for diverse entertainment.

These findings provide actionable insights for content recommendations and strategic decision-making, ensuring Netflix continues to cater to evolving viewer preferences.

