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
Data imported from cleaned up csv (spotify_clean.csv) First, a scatter plot of the entire dataset with Popularity and Energy looking to see if a trend shows, it did not.  Then attempted to break the data down into clusters, K Curve showed 2-3 clusters would be best, 2 had the curve but 3's output seemed slightly better visually.  Models using different variables against popularity was created yet nothing stood out for the a-ha moment.  Finally, after trying several graphs, it was determined unsupervised model would not be of much value for this instance.

### Supervised Regression
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

### Supervised Classification
This model seeks to predict whether a song is a "banger" using a Random Forest Classifier. Model performance is evaluated with metrics like a confusion matrix and accuracy score, and recall score.

1. Reading and Preprocessing Data:
-Clean Spotify data is loaded.
-'track_album_release_date' is processed to extract the year.
-Index is set to 'track_name' and 'track_artist'.

2. Feature and Target Definition:
-Features (X) are defined by copying the DataFrame and dropping 'bangers'.
-Target vector (y) is defined as the 'bangers' column.

3. Data Splitting and Scaling:
-Data is split into training and testing sets.
-Standard scaling is applied to feature sets using StandardScaler.

4. Model Training and Evaluation:
-Random Forest Classifier (500 estimators) is created and trained.
-Predictions are made on the testing data.
-Model performance is evaluated using a confusion matrix and accuracy/recall scores.

Initial Result:
The model achieved a high accuracy score of 96%. However, the recall is relatively low at only 28%. This indicates that the model struggles to correctly identify positive instances. Specifically there were issues with high volume of false negative results. 

Importance Analysis:
The feature importance analysis from the model revealed that the top nine features (Loudness, Tempo, Energy, Speechiness, Acousticness, Duration, Valence, Danceability, Liveness) accounted for ~74% of the importance when determining whether a song can be classified as a "banger".

Model Improvement:
To address concerns about model performance, a new model was trained with a reduced set of features (df_spotify_MV). The new model was ran using exactly the same process except the features were trimmed down to only include the top nine features identified in the importance analysis. The new model achieved significantly improved results:
-Accuracy Score: 99.32%
-Recall (Class 1): 87%
-F1-Score (Class 1): 91%

The new model with a reduced set of features significantly improved performance, achieving an accuracy score of 99.32% and addressing the poor recall in the initial model. The feature selection process played a crucial role in enhancing the model's ability to identify "bangers". By trimming down the features and cutting out the extra noise in the model, high accuracy was acheived while eliminating the large volume of false negative results in the initial model. 

### Tableau
[Tableau Workbook](https://public.tableau.com/authoring/Project4_17014016191960/popvsgenre#1)

Data used the Spotify API csv file wsa used to find a trend between different variables. Through trial and error, we were able to find a trend between each variable. We decided to use the data provided by the csv file to answer asking ourselves three questions:
  1. Are key and mode of a song important ?
  2. Which artists have the most popular songs?
  3. What does it take to have a top song ?

We looked at different graphs and charts to determine the answer to these questions. 
  Answer 1. Key and Mode are not important when determining if a song is a 'banger' or a top song. Something we learned is that a song can       played in a key major, but that would have nothing to do with whether the song will be likeable enough to become a popular hit !
  Answer 2. We looked at the top 6 artists to determine what was the most popular songs.
    Based on the data:
  -Martin Garrix-No Sleep ft. Bonn
  -Queen-Somebody to love -2011 Mix
  -The Chainsmokers-Closer ft. Halsey
  -David Guetta-Titanium ft. Sia
  -Don Omar-Dile
  -Drake-One Dance
  Answer 3: Popular artists tend to have popular songs. We found that high energy, loudness, and danceability makes a song one of the chart     topper. 
