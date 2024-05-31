# Notes

# Models to check:

1. [HistGradientBoostingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingClassifier.html#sklearn.ensemble.HistGradientBoostingClassifier)
   - learning_rate = [0.1, 0.01]
   - max_depth = [2,3,5]
   - random_state = [42]
   - max_features = [3, 5, 8, 1.0]
   - l2_regularization = [0, 0.5, 0.8]
2. LDA

   - solver = ['svd', 'lsqr']
   - shrinkage = [None, 'auto']
   - n_components = [3,5,8]

3. QDA
   - reg_param = [0.3,0.5,0.8]
4. KNN
   - n_neighbors = [3,5,8]
   - weights = ['uniform','distance']
   - p = [1,2]
   - leaf_size = [15,30,50]
5. SVM
   - C = [0.5,1,1.5]
   - kernel = ['linear','rbf','sigmoid','poly']
6. [GradientBoostingClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html#sklearn.ensemble.GradientBoostingClassifier)

   - loss = ['log_loss', 'exponential']
   - learning_rate = [0.1, 0.01]
   - n_estimators = [100, 200]
   - subsample = [1.0, 0.7]
   - max_depth = [2,3,5]
   - random_state = [42]
   - max_features = [3, 5, 8, None]
   - ccp_alpha = [0, 0.01, 0.05, 0.1]

7. [Voting?](https://scikit-learn.org/stable/modules/ensemble.html#voting-classifier)

# Feature Selectors to check:

1. KBest
   1. Parameters:
      - k: 5,10,20,40,80
      - socre_func: f_classif, mutual_info_classif
2. FPR
   1. Parameters:
      - score_func: f_classif, mutual_info_classif
      - alpha: 0.001, 0.01, 0.05, 0.1
3. FDR
   1. Parameters:
      - score_func: f_classif, mutual_info_classif
      - alpha: 0.001, 0.01, 0.05, 0.1
4. Fwe
   1. Parameters:
      - score_func: f_classif, mutual_info_classif
      - alpha: 0.001, 0.01, 0.05, 0.1
5. KBest with one of the above as score func? Just some best values
6. Some tree based
   1. Parameters:
      - The same as chosen classifier, can be the same as GradientBoostingClassifier for example
7. RFE
   1. Parameters:
      - estimator: KNeighborsClassifier (n_neighbors=sqrt(number of features to select)), svc(kernel="linear", "rbf"),DecisionTreeClassifier()
      - n_features_to_select: 5, 10, 20
      - step: 0.5, 0.2
8. RFECV
   1. Parameters:
      - estimator: KNeighborsClassifier (n_neighbors=sqrt(number of features to select)), , svc(kernel="linear", "rbf"),DecisionTreeClassifier()
      - step: 0.5, 0.2
      - min_features_to_select: 5,10,20
      - cv: 5, 10, 15
9. SequentialFeatureSelector:
   1. Parameters:
      - estimator: KNeighborsClassifier (n_neighbors=sqrt(number of features to select)), , svc(kernel="linear", "rbf"),DecisionTreeClassifier()
      - n_features_to_select: 5, 10, 20

# Batches based on the above:

1.  1. Models: LDA, QDA, KNN, svc, GradientBoosting, HistGradientBoosting. Basic params
    2. Selectors: KBest
1.  1. Models: LDA, QDA, KNN, svc, GradientBoosting, HistGradientBoosting. Basic params
    2. Selectors: KBest (with some best params), FPR, FDR, FWE
1.  Similar to the above but with better params
1.  1. Models: LDA, QDA, KNN, svc, GradientBoosting, HistGradientBoosting. Basic params
    2. Selectors: Best from the above, RFE, RFECV, SequentialFeatureSelector (this batch will take ages)

Next choose 3-5 best methods with some current best params and create batches for classifiers

## Main Description

Emm I read the pdf and it's a bit hard to split this project into tasks tbh. From what I understood the goal, in short, is to achieve the best possible accuracy with least amount of features used. Whereas there is some reward for higher accuracy and penalty for number of features used so we need to find a proper balance. 5 different approaches should be used. It is a binary classification task. So I think we could:

1. Find some best candidates methods for binary classification tasks with numeric features.
2. One approach would be to iterate over the number of features starting from 1 (xd) and find the number that achieves the best score for each of the chosen methods
3. We could also do some feature selection methods and try to find the best number of features that way.
4. We could do some ensembling, maybe combining models from the above

## The performance of the model could be measure in terms of:

1. Taking the average from the proba array (array returned by experiment function) - but then there is a problem with decisiion trees for example, cause I think they do not return probabilities of predictions. hmm so maybe some other metric, maybe just do train test splits and truncate the output to 1000. Maybe experiment with features this way, reduce their amount so that the number of predicted in y_test is closer to 1000, hmm but then when you reduce the number of features you are probabily lowering the quality of the predictions
2. The higher the average the better the model

## Process

1. Do the experiments in batches. Then look at some graphs and decide in which direction you should go, what parameter values you should test to obtain the best results.
