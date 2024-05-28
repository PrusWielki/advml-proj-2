# Notes

TODO: It seems it's either Gradient Boosting or MLP Classifier with K Best or RFS, rather K Best. So test more Gradient Boosting vs MLP on K Best and RFS

Also try more with AdaBoost, it doesn't work with MLP Classifiers, so use something else

also test vanilla xgboost

Voting when voting=hard has no predict proba so dont use it

Try to rerun the best models (max 2, 1 feature selector) with scaled data, test different scalers, standard scaler, robust scaler

Also test adding polynomial features with different degrees

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
