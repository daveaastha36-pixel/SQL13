1.
Create a table called Orders with columns: order_id, user_id, order_amount, and app_name (e.g., 'Zomato', 'Swiggy', 'Flipkart'). Insert at least 10 sample records with different users and apps. Write an SQL query using the OVER() function to display each order's amount along with the total order amount for all orders.

***SOLUTION***
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    user_id INT,
    order_amount DECIMAL(10,2),
    app_name VARCHAR(20)
);

INSERT INTO Orders VALUES
(1, 101, 350.00, 'Zomato'),
(2, 101, 450.00, 'Swiggy'),
(3, 102, 1200.00, 'Flipkart'),
(4, 103, 280.00, 'Zomato'),
(5, 102, 950.00, 'Flipkart'),
(6, 104, 180.00, 'Swiggy'),
(7, 101, 700.00, 'Flipkart'),
(8, 105, 320.00, 'Zomato'),
(9, 103, 400.00, 'Swiggy'),
(10, 104, 1500.00, 'Flipkart');


2.
Using the Orders table, write an SQL query to show each user's order_id, order_amount, and the average order_amount for that user using the OVER(PARTITION BY user_id) clause.<br><br><em><strong>Hint:</strong> Use AVG(order_amount) OVER(PARTITION BY user_id) to get the per-user average.</em>

***SOLUTION***
SELECT
    order_id,
    user_id,
    order_amount,
    AVG(order_amount) OVER (
        PARTITION BY user_id
    ) AS avg_order_amount_per_user
FROM Orders;

3.
Suppose you have a table called Playlist with columns: song_id, user_id, and duration_sec. Write an SQL query to display each song's duration, and the total duration of songs added by each user using SUM(duration_sec) OVER(PARTITION BY user_id).

***SOLUTION***
SELECT
    song_id,
    user_id,
    duration_sec,
    SUM(duration_sec) OVER (
        PARTITION BY user_id
    ) AS total_user_playlist_duration
FROM Playlist;
4.
Given a table named MovieRatings with columns: rating_id, user_id, movie_name, and rating (1-5), write an SQL query to show each rating, the average rating per movie, and the difference between the user's rating and the movie's average rating using window functions.<br><br><em><strong>Hint:</strong> Use AVG(rating) OVER(PARTITION BY movie_name) and subtract it from the user's rating.</em>

***SOLUTION***
SELECT
    rating_id,
    user_id,
    movie_name,
    rating,
    AVG(rating) OVER (
        PARTITION BY movie_name
    ) AS movie_avg_rating,
    rating -
    AVG(rating) OVER (
        PARTITION BY movie_name
    ) AS rating_difference
FROM MovieRatings;

