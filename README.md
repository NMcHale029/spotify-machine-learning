# What Makes a Banger?

### Project Overview
Data on 30,000 songs from a Spotify API was used to create models to predict a song's popularity. Data was cleaned, and then used in three different machine learning models- Unsupervised, Supervised Regression, and Supervised Classification. Data was also visualized in Tableau before modeling, and after modeling.

### Collaborators
- Sha’miah Lindsey (ShamiahL)
- Kent Andrews (kxandrews1970)
- Tristan Vazquez (vazq0003)
- Noah McHale (NMcHale029)

### Project Documentation
- [Project Proposal](https://docs.google.com/document/d/1fJfuKnB7wwmtjz0gdJATHtjz5hcWmLb2p8mySA15cbc/edit?usp=sharing)
- [Presentation](https://docs.google.com/presentation/d/1bgPAeIX8A5Rs4ynsJEjMJ7fokzhuDyn44jWHyjtXL90/edit?usp=sharing)

### Dependencies used in project
- numpy
- pandas
- Path from pathlib
- StandardScaler from sklearn.preprocessing
- train_test_split from sklearn.model_selection
- LinearRegression from sklearn.linear_model
- mean_squared_error from sklearn.metrics
- r2_score from sklearn.metrics
- KMeans from sklearn.cluster
- PCA from sklearn.decomposition
- hvplot.pandas
- RandomForestClassifier from sklearn.ensemble
- confusion_matrix from sklearn.metrics
- accuracy_score from sklearn.metrics
- classification_report from sklearn.metrics

### Cleaning
Data was read in using Path from a csv file that contains data about 30,000 songs on Spotify. The data included:
- track_id (removed)
- track_name
- track_artist
- track_popularity
- track_album_id (removed)
- track_album_name (removed)
- track_album_release_date
- playlist_name (removed)
- playlist_id (removed)
- playlist_genre
- playlist_subgenre
- danceability
- energy
- key
- loudness
- mode
- speechiness
- acousticness
- instrumentalness
- liveness
- valence
- tempo
- duration_ms

The variables that were removed are denoted above. These variables were removed because they were at times arbitrary (such as track_id, or playlist_name), or they were unneeded as a way to uniquley identify a song.
A column named 'bangers' was added. This column included a 1 or 0, depending on if the song had a popularity about 80 or not.
track_name and track_artist were set as the index, and release date was chagned to a datetime variable.
Numerical columns were scaled using StandardScaler and categorical variables had dummies created.
This final dataframe was saved to a csv, 'spotify_clean.csv' in our Resource folder.

### Unsupervised Model
Data was imported from spotify_clean.csv into a pandas dataframe, and then plit into training and test data. The target variable used is track_popularity. The notebook tests several models for mean squared error.

Models tested in the notebook include:
- All music variables, all genres, and sub-genres (MSE: 530)
- Just music variables (MSE: 574)
- All genres/sub-genres (MSE: 551)
- Just genres (MSE: 600)
- Just sub-genres (MSE: 550)
- Each music variable (MSE: ranged 610-624)

The best model was the model including all variables. However, the model does not do a good job of predicting the popularity of a song. The model, on average, comes within 23 points of the actual popularity score of a song. The scale is 0-100 which means that on average, the score is off by a quarter the posible range.

A Linear Regression model is not a good fit for predicting a song's popularity.

### Supervised Regression


### Supervised Classification


### Tableau
[Spotify Banger Tableau](ENTER LINK HERE)