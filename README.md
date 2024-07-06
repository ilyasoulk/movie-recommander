 # Movie Recommender

### Data Processing

In this project, I utilized two distinct data sources with the primary aim to merge these datasets. I integrated the common movies from IMDb into the MovieLens dataset, using MovieLens for the ratings. A challenge arose with movies having the same title and genre but different start years. I opted to retain only the most recent versions, as they generally have more ratings.

### Feature Engineering

One potential feature was the inclusion of notable individuals involved in each movie. However, I decided against it due to the complexity of encoding. With over 150,000 unique individuals, simple one-hot encoding was impractical. Although I experimented with TF-IDF encoding, the challenge remained in managing a large number of columns while still representing multiple individuals per movie. I improved the movie features by incorporating their average ratings and employed one-hot encoding for genres. For user features, I added the average rating they assigned and the number of movies rated per genre.

### Model Methodology

Initially, I attempted to create a comprehensive interaction matrix for each user pair and their average rating. This approach proved computationally prohibitive, yielding millions of pairs even after eliminating duplicates and pairs without shared movie ratings. An alternative, such as using ALS with a distributed system like Spark, was considered but dismissed as it relies solely on past ratings without leveraging user and movie features. Instead, I opted for a neural network encoder that processes a pair of users and a movie directly to predict their rating. This setup involves three separate neural networks: one for users, one for movies, and one for combining the encoded representations of both users. The training dataset includes every user pair with commonly rated movies, calculating the average rating and compiling it as: User_1, User_2, Movie, Rating. Given the extensive dataset size, a lower learning rate was chosen to facilitate learning in initial epochs. However, the model struggled to learn efficiently, possibly due to its parameters being relatively small compared to the dataset size.

### Results

As mentioned, the model faced difficulties with prolonged learning, potentially underfitting due to the small size of model parameters relative to the dataset. Nonetheless, I achieved a test loss of 0.09 on my scaled mean squared error metric, indicating reasonable precision in rating predictions. My recommender system rated all unwatched movies for each user pair and recommended the top-rated ones.

### Conclusion

Ultimately, I developed a model capable of accurately predicting ratings for a given movie relative to a user pair. Managing large data matrices and fine-tuning model parameters posed significant challenges, particularly in training efficacy over a few epochs. The learning rate significantly impacted performance due to frequent optimization steps needed for the large dataset and small batch sizes. Future enhancements could include incorporating directors to further refine movie features, potentially improving prediction accuracy.
