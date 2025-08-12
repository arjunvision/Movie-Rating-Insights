# Movie-Rating-Insights

# MOVIE RATING INSIGHTS

Reading from sample data

import pandas as pd
​
# Sample movies dataset

movies = pd.read_excel("C:\\Users\\admin\\Downloads\\movies.xlsx")
​
# Sample ratings dataset

ratings = pd.read_excel("C:\\Users\\admin\\Downloads\\ratings.xlsx")

print("Movies Data:")

print(movies.head())

print("\nRatings Data:")

print(ratings.head())
​
​# Analyze Average Ratings per movie

# Merge ratings with movies to get titles

merged = pd.merge(ratings, movies, on='movie_id')
​
# Calculate average rating per movie

average_ratings = merged.groupby('title')['rating'].mean().sort_values(ascending=False)
​
print("🎬 Average Ratings per Movie:")

print(average_ratings)

op Rated & Worst Rated Movies

print("\n🏆 Top Rated Movie(s):")

top_rating = average_ratings.max()

print(average_ratings[average_ratings == top_rating])
​
print("\n Worst Rated Movie(s):")

lowest_rating = average_ratings.min()

print(average_ratings[average_ratings == lowest_rating])

Most Rated Movies

rating_counts = merged.groupby('title')['rating'].count().sort_values(ascending=False)

print("\n📊 Most Rated Movies:")

# User Rating of a Movie

def rate_movie(user_id, movie_title, user_rating):

    # Find movie ID
    
    movie = movies[movies['title'] == movie_title]
    
    if movie.empty:
    
        print("Movie not found.")
        
        return
        
    movie_id = movie.iloc[0]['movie_id']
    
    # Add to ratings
    
    global ratings
    
    new_rating = pd.DataFrame({'user_id': [user_id], 'movie_id': [movie_id], 'rating': [user_rating]})
    
    ratings = pd.concat([ratings, new_rating], ignore_index=True)
    
    print(f"✅ Added rating {user_rating} for '{movie_title}' by User {user_id}")
​
# Simulate user rating

rate_movie(106, 'Inception', 5)

# Visualization

import matplotlib.pyplot as plt
​
# Plot average ratings

average_ratings.plot(kind='bar', title='Average Movie Ratings', color='skyblue')

plt.ylabel('Rating')

plt.xlabel('Movie')

plt.tight_layout()

plt.show()

print(rating_counts)
