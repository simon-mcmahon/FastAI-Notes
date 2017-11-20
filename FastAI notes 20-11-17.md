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


We cannot be expected to memorise the best possible hyperparameter. Run a data science experiment with an experiment in a timely manner. Speed is a key parameter here (do as many as possible and do the m quickly with the available resources).


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


GANs
generative adversarial networks

loss functino = the function which determines how well your model think it is doing.
The model must base all of its learning off this score
we should design it to convey the information we want it to

A better approach is giving your learner richer knowledge such as:
position, size, species etc. of a fish 

Problem:
How to score (incrementally) such a vague task like (pictures, movie scripts etc.)

GANs are the strategy for to create a scoring system for these vague, non-concrete problems.

GANs:
generator vs discriminatior (2 NNs in competition)
generator generates the script/movie
discriminator says if it is real or fake.

Key insight: A neural network is being the loss function.

Important for the judge, he needs to not be very good in the beginning. The judge learns as it goes along.
Discriminator is about as skilled as the generator at each point. The loss function trains both the judge and the artist.

latent variable space (random seed for the image). 
we can make it N-dimensional (hand it a vector).
We can make some this effect properties
Latent variable space can be arbitrarily big. Design considerations:
- changing 1 number in the vector. (1 dimension is another knob to fine tune the image). 
There is not a hard lock between image size and variable size dimension size.

Generator back propogation step. it has access to the discriminator neurons so it knows how to fool the generator.
Discriminator learns in the same way CNN.

GANs. Original ones are very unstable. In last 2 years, a LOT of progress has been made.
Stability tricks to get system to converge:
soft labels and noisy labels. adding noise to inputs (dont label everything 0 or 1).
remember history dont let neurons change too much (checkpoint generations)
avoid sparse gradients (Relu)
- if the value is forced to zero we may not get as smooth a transition.
this is because we want smooth transitions.
Leaky relu was reccommended instead.

we can add and subtract "concepts" about the face such as "glases" or "smile vector" in the latent variable space.

discriminator is a convolutional NN
generator is a deconvolutional NN (not actually an unpooling operation)(it is the inverse of a convolution, we have one pixel bleed into 9 or so).

deconvolutional network. we unpool over and over to expand a a 7x7 vector 

overlap between neurons depends on your stride length.
bilinear interpolation is the name of the process for unpooling.
we use a spline process to smooth out the digital increases.

initially we start with a small discriminator nad generator and then when it reaches a certain level of competancy, we expand the number of layers and the area that the GAN can access.

## Going deeper on GANs

DCGAN is a deep convolutional GAN.
GCGAN are GAN 2.0.
We are now up to like GAN 13.0. Many im

arvix is a good source of printed literature on other peoples projects.

## Cool GAN projects

progressive GANs Nvidia (we can 
stacked GANs (initial photo generation step and then expansion ghan.)
CycleGAN is really cool. (zebras to horses).

Fake news GAN.

evolutionary algorithms are non-directed. Sam is not a fan.
neural networks are powerful because each step we know the directino in which we want to head.
