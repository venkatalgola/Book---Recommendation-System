# Book---Recommendation-System
Built a book recommendation system that suggests books to users based on popularity, reading behavior, and book content similarity — using a dataset of 271,360 books, 1.1M+ ratings, and 278,858 users.
📦 Dataset
Source: Book Recommendation Dataset – Kaggle
File            Records              KeyColumns 
Books.csv       271,360              ISBN, Title, Author, Publisher
Ratings.csv     1,149,780            User-ID, ISBN, Book-Rating
Users.csv       278,858              User-ID, Location, Age

🛠️ Tools & Libraries

Python (Pandas, NumPy, Matplotlib, PIL)
scikit-learn — cosine similarity, CountVectorizer
Google Colab / Kaggle Notebooks

🔍 Approach — 4 Recommendation Methods
1. Popularity-Based Filtering

Aggregated ratings by book title
Applied a weighted rating formula (similar to IMDb's formula):
score = (v * R + m * C) / (v + m)
where v = number of votes, R = average rating, C = global mean, m = 90th percentile threshold
Filtered books with fewer than 250 ratings to avoid obscure titles
Output: Top 10 most popular books with cover images

2. Item-Based Collaborative Filtering

Built a User-Item pivot table (rows: User-ID, columns: Book-Title, values: ratings)
Computed Pearson correlation between the target book and all other books
Filtered out rare books (< 200 ratings) and low-rated recommendations (avg < 5)
Output: Top 5 most correlated books with cover images

3. User-Based Collaborative Filtering

Filtered users with > 200 ratings to focus on active readers
Computed cosine similarity across user rating vectors
Found the 5 most similar users, then recommended books they rated highly that the target user hasn't read
Output: Personalized book list based on similar user behavior

4. Content-Based Filtering

Combined Book Title + Author + Publisher into a single feature string
Applied CountVectorizer to create a term-frequency matrix
Computed cosine similarity across all books
Output: 5 most content-similar books for any given title


📊 Results
  Method                 SampleInput                        Top Recommendation
Popularity              —                          Harry Potter series, Da Vinci Code
Item-Based         "Me Talk Pretty One Day"        The Poisonwood Bible (Rating: 8.2)
User-BasedUser     #31556                          Artemis Fowl, Eragon, Guardians of Ga'Hoole
Content-Based      "The Da Vinci Code"             The Firm, The Chamber (John Grisham)

💡 Key Learnings

Sparsity problem: Most users rate very few books — handled by filtering low-activity users
Cold start problem: New books with few ratings get fallback random recommendations
Weighted ratings vs simple averages: A book with 10,000 ratings at 7.5 is more reliable than one with 5 ratings at 10.0
Cosine similarity vs Pearson correlation: Pearson works better for collaborative filtering (handles scale differences in user ratings)

# How to Run
bash# Clone the repository
git clone https://github.com/yourusername/book-recommender

# Open in Google Colab or Jupyter
# Download dataset from Kaggle and place in /input/book-recommendation-dataset/

# Run all cells in book-recommender.ipynb


🔮 Future Improvements

Integrate a vector database (FAISS/ChromaDB) for faster similarity search at scale
Add a RAG layer to answer natural language queries like "recommend a thriller like Gone Girl"
Deploy as a simple web app using Streamlit.

Please refer the pdf guide for more clarity
