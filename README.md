## 📂 **Golden_Age_Video_Game**
In this project, we'll explore the top 400 best-selling video games created between 1977 and 2020.
Our database contains two tables. We've limited each table to 400 rows for this project.

### 📌 **Databases Detail**

![image](https://github.com/abahpolban/Golden_Age_Video_Game/assets/87195694/a4db78b7-8a85-402a-85c0-460b56ac89f6)



### 📌 **Let's find the ten best-selling video games in game_sales**

**steps**
- Select all columns for the top ten best-selling video games (based on games_sold) in game_sales.
- Order the results from the best-selling game down to the tenth best-selling game.

**query :**
```sql
select * 
from game_sales  
order by game_sales.games_sold desc
limit 10;
```
**result:**

   ![image](https://github.com/abahpolban/Golden_Age_Video_Game/assets/87195694/ad5d7a6b-53fb-4916-8d50-270488b16690)

### 📌 **Let's determine how many games in the game_sales table are missing both a user_score and a critic_score**

**steps**
- Join the game_sales and reviews tables together so that all games from the game_sales table are listed in the results, whether or not they have associated reviews.
- Select the count of games where both the associated critic_score and the associated user_score are null.

**query :**
```sql
select count(g.game) 
from game_sales as g 
left join reviews as r
on g.game=r.game
where r.critic_score IS NULL and r.user_score IS NULL;
```
**result:**

  ![image](https://github.com/abahpolban/Golden_Age_Video_Game/assets/87195694/3e6fadcf-d496-436f-bd09-94b53abd69b2)

### 📌 **Find the years with the highest average critic_score**

**steps**
- Select release year and average critic score for each year; average critic score for each year will be rounded to two decimal places and aliased as avg_critic_score.
- Join the game_sales and reviews tables so that only games which appear on both tables are represented.
- Group the data by release year.
- Order the data from highest to lowest avg_critic_score and limit the results to the top ten years.

**query :**
```sql
select 
    g.year, 
    avg(r.critic_score) as avg_critic_score
from game_sales as g 
inner join reviews as r 
on r.game=g.game
group by g.year 
order by avg_critic_score DESC
limit 10;
```
**result:**

  ![image](https://github.com/abahpolban/Golden_Age_Video_Game/assets/87195694/b4634ff1-a8d8-458b-a47d-4837b477c78d)

### 📌 **Find game critics' ten favorite years, this time with the stipulation that a year must have more than four games released in order to be considered.**

**steps**
- Starting with your query from the previous task, update it so that the selected data additionally includes a count of games released in a given year, and alias this count as num_games.
- Filter your query so that only years with more than four games released are returned.

**query :**
```sql
SELECT g.year,
    COUNT(g.game) AS num_games, 
    ROUND(AVG(r.critic_score),2) AS avg_critic_score
FROM game_sales g
INNER JOIN reviews r
ON g.game = r.game
GROUP BY g.year
HAVING COUNT(g.game) > 4
ORDER BY avg_critic_score DESC
LIMIT 10;
```
**result:**

  ![image](https://github.com/abahpolban/Golden_Age_Video_Game/assets/87195694/45a934d2-631c-4709-91fb-26ad3123b7e1)




