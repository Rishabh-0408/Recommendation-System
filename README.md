# Recommendation-System
Content-based filtering system using cosine similarity and NLP techniques

# Movie Recommendation System

## Project Overview

This project is a content-based movie recommendation system. The goal is to recommend movies to users based on the content and attributes of a movie they have watched or liked. The system leverages natural language processing (NLP) techniques to analyze movie overviews, genres, keywords, cast, and crew to find similarities between movies.

## Dataset

The project utilizes the [TMDB 5000 Movie Dataset](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata), which consists of two CSV files:

* `tmdb_5000_movies.csv`: Contains detailed information about the movies.
* `tmdb_5000_credits.csv`: Contains information about the cast and crew for each movie.

## Methodology

The recommendation system is built using a content-based filtering approach. The core idea is to create a "tag" for each movie, which is a collection of its most important attributes. The similarity between these tags is then used to recommend movies.

The key steps in the process are:

1.  **Data Loading and Merging:** The two datasets (`movies` and `credits`) are loaded and merged into a single DataFrame based on the movie title.

2.  **Data Cleaning and Preprocessing:**
    * Irrelevant columns are dropped, and only the most important features for recommendation are kept (`movie_id`, `title`, `overview`, `genres`, `keywords`, `cast`, `crew`).
    * Missing data points are handled by dropping the corresponding rows.
    * Helper functions are used to extract relevant information from the JSON-like columns (`genres`, `keywords`, `cast`, `crew`). For example, the names of the genres, the first three cast members, and the director's name are extracted.

3.  **Feature Engineering:**
    * A new column called `tags` is created by concatenating the preprocessed `overview`, `genres`, `keywords`, `cast`, and `crew` columns. This `tags` column serves as the primary text corpus for each movie.
    * All text in the `tags` column is converted to lowercase for consistency.

4.  **Text Vectorization:**
    * The `tags` are vectorized using the `CountVectorizer` from scikit-learn. This converts the text data into a matrix of token counts.
    * To reduce the dimensionality of the data and focus on the most important words, `max_features` is set to 5000, and common English `stop_words` are removed.

5.  **Similarity Calculation:**
    * The `cosine_similarity` metric is used to calculate the similarity between the vector representations of the movies. This results in a similarity matrix where each entry represents the similarity score between two movies.

6.  **Recommendation Function:**
    * A function `recommend(movie)` is defined that takes a movie title as input.
    * It finds the index of the input movie in the dataset.
    * It then retrieves the similarity scores for that movie from the similarity matrix.
    * The movies are sorted based on their similarity scores in descending order.
    * The top 5 most similar movies (excluding the input movie itself) are returned as recommendations.

## Technologies and Libraries Used

* **Python:** The primary programming language used.
* **Pandas:** For data manipulation and analysis.
* **NumPy:** For numerical operations.
* **scikit-learn:** For implementing the `CountVectorizer` and `cosine_similarity`.
* **NLTK (Natural Language Toolkit):** For stemming and other NLP tasks.
* **Ast:** For safely evaluating strings containing Python literals.
* **Jupyter Notebook:** For interactive development and visualization.

## How to Run the Project

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    ```
2.  **Install the required libraries:**
    ```bash
    pip install numpy pandas scikit-learn nltk
    ```
3.  **Download the dataset:**
    * Download the TMDB 5000 Movie Dataset from [Kaggle](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata).
    * Place the `tmdb_5000_movies.csv` and `tmdb_5000_credits.csv` files in a `Dataset` folder within the project directory.

4.  **Run the Jupyter Notebook:**
    * Open and run the `Recommendation system.ipynb` notebook to see the step-by-step implementation and generate the recommendations.
