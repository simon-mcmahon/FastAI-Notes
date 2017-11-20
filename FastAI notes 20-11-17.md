# AnsicsH20 file

# Bucketizing

We take something like age, and make it into a categorical variable such as teenagers or 60+.
Basically changing a numerical variable into a categorical. This can help the learner.

Jscore:

factor columns

Using ML tool called H20. Metrics and charts out of the box.
import the data file.

# Data splitting
This has a huge impact on the output.
If you choose blindly (80-10-10) (the 10% validation might have a trend which might rule out any results
Choose a non-random split which can keep a balance of the different trends of results.

Gradient boosted estimator trains very quickly

Gradient boosted machine

builds small decision trees
imports it into a larger trees and then optimizes somehow??

GBM - not a neural network. can be built much quicker. proof of concept 

CAN BE BUILT IN A LAYER ON TOP OF SEMANTIC SEGMENTATION.

GBM picks decision bounds and the trees have a voting 

hyperparameter are used by the gradient boosting estimator

Deep neural nets work very well with 'analogue data'.
mortality data is not a compositional problem, it is very binary.

We can make an ensemble voter which combines together the results of many models together.

AUC is the area under a curve of an ROC curve (plot of True positive rate vs false positive rate (y vs x)).


We cannot be expected to memorise the best possible hyperparameter. Run a data science experiment with an experiment in a timely manner.


Build a function to pick a subset of hyperparameter, do a grid search to optimize.

train many models, score the results and build up a picture of the relevant parameters and which ones are consistently scoring higher.

This GBM was not a deep learner but was a 2 dense layer neural network. Adapt the hyperparameters over time.

For each hyperparameter there is a weight which determines its likelyhood of being selected in further grid searches.
A poorly performing variable will have its weight decreased 

If your initial learning rate score the model will do badly 
we didn't but we could build a neural network in order to choose the hyperparameters.

The larger number of data experiments , the better. Understanding of metrics is key however.

Confusion Matrix
table of true positive/ true negative/ false positive/ false negative values.

# Data breakdown

Training - validation - testing.

After we have a good model, we can resplit the data and retrain based on the good hyperparameters on the entire set for deployment for better reliability.

We build 5-10 models off of the data set for different splits. We then predict the dataset on the 
This can test the reliability of the dataset in a robust way.

momentum term can effect stability of the model.
learning rate annealing = learning rate decays over the training process.

defaults are a great idea.

The winners of imagenet each year are typically voting ensembles of different models.


Stacked ensemble. We output value of multple model and vote on their outputs.

# Grid search

Inside the hyperparameters, we set a maximum and a minimum, it will work across the hyper-cube for the min-max value and see which ic the best.
This is not an intelligent values.

Typically we are given a grid-search. Reccommend a random, discrete grid search. (finite number of points).

## How do we compare these models against each other?

We should not pay too much attention to the training data.
AUC = 0.95
