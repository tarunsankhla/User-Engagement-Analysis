# User Engagement Analysis

Analyze and identify which users are the most active based on their interactions (e.g., rating movies). This helps in improving platform personalization, marketing strategies, and user retention.

---

## Objective

In a movie recommendation system such as Netflix, Amazon Prime, or IMDb, **user engagement** is a critical metric. By analyzing which users are the most active, you can:
- **Personalize** content recommendations.
- **Retain** users through targeted rewards and loyalty programs.
- **Monitor** user behavior to spot potential churn.

---

## Use Cases

1. **User Rewards and Loyalty Programs**  
   - Reward the top 1% of users to maintain engagement through gamification, badges, or exclusive content access.

2. **Operational Monitoring**  
   - Track engagement trends to identify potential churn if active users reduce their activity.

---

## Pig Script

```pig
-- Load the data
movies_data = LOAD '/final_project/ratings.csv'
              USING PigStorage(',')
              AS (userId:chararray, movieId:chararray, rating:float, timestamp:long);

-- Group data by userId
grouped_data = GROUP movies_data BY userId;

-- Count the ratings for each user
user_rating_count = FOREACH grouped_data GENERATE
                    group AS userId,
                    COUNT(movies_data) AS rating_count;

-- Sort the users by rating_count in descending order
sorted_users = ORDER user_rating_count BY rating_count DESC;

-- Store or display the result
STORE sorted_users INTO '/user/hdoop/user_engagement'
USING PigStorage(',');
```


![image](https://github.com/user-attachments/assets/dd35276f-bd94-4174-a550-c4cc80fa9758)
