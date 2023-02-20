## Classifier
Build a classifier with the four languages' sentences and make predictions with the test set that equally contains these four language name as labels and analyze the frequency of one language being recognized as the other by the classifier.

### Tool: 
sklearn: SVC, GridSearchCV, TfidfVectorizer
- #### Model
  - SVC [(support vector classifier)](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html) is used with "C=10.0" (best C value searched by using       [GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html)).
- #### Data Preprocessing
  - x is the stacked sentences of all 4 languages and y is the stacked language names of the four.
  - Data is split into 25% test set and 75% of training set with stratify equals to y (Every language has the same amount in original data, so they will be equally spread in both train and test set after split.).
  - Punctuation is removed.
  - Characters are tokenized and encoded by using [TfidfVectorizer](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.TfidfVectorizer.html) with "ngram = (1, 3)".
- #### Predictions
  - The predictions of the model are compared against the true language labels to collect the names of the wrong predicted language pairs and their counts. Counts are normalized by dividing it by the total length of all labels in the test set (as shown in following, in which case 5 language pairs are wrongly predicted).
    ```
    {'cmn+wen': 0.2926829268292683,
    'cmn+wuu': 0.34146341463414637,
    'wuu+yue': 0.0975609756097561,
    'yue+cmn': 0.0975609756097561,
    'wuu+wen': 0.17073170731707318}
    ```
  
### 1000 Sampling without duplicates
- The above model training and prediction are run with different randomly splited train and test set each time for 1000 times. The mispredictions are collected, counted and normalized as well in each run, which is in the end plotted for visualization.
