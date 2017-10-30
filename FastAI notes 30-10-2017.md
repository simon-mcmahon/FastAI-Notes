# Notes from Amazon FastAI course (30/11/2017)

### Tips and tricks from lesson 1 and 2 (discussed)

Things aren't working? Try to:
1. Run the command `nvidia-smi` in the bash shell to check that the GPU is actually running.

2. In some lessons after the model is trained, save it and restart the kernel in the jupyter notebook. Load only the model and not the training data. This will avoid memory overflow on the p2 instance.


### Convolutional Neural Networks (Presentation by Sam).

**Note:** 
I do not pretend to be an expert here and the powerpoint is very good. I took these notes to try and capture some of Sam's off hand remarks to try and pick up some of the "rules of thumb" that can come from experience (which I don't have yet).

Please feel free to let me know of anything that is wrong here (or just for a chat) by contacting me via email `simon.nathan.mcmahon (at) gmail (dot) com` .

#### Definitions:

* epoch = number of times the training process is applied

* The activation function is a response to input which determines to determine if neurons "fire" in the conventional biological sense.

* Convolution = (piecewise multiplication and sum of pixels from image and the convolution kernel maps to the output of the convolution layer).

* Convolution Kernel = (matrix with values representing a specific process such as emboss)

The output of a convolution operation is in some sense a similiarity value of the kernel to the image over the target region.

* Commonly, convolution layers are stacked to represent more and more abstract features.
    * layer 1 = simple (diagonal lines etc)
    * layer 2 = hexagonal shapes
    * layer 3 = even more abstract etc.

Pooling = the process of applying an operation on the output of a series of convolutions to reduce the dimensionality and keep the important information

Max pooling = keeping the largest value in an *N x N* region from the output of the convolution layer.

Regularisation is a process to prevent overfitting.

#### Tips and Tricks:

* Data should be normalised (0 to 1) wherever possible

* input parameters are not independent

* zero padding is commonly used - so convolution does not shrink the tensor.

* commonly odd numbers are used to avoid changes in the size of the tensor

#### Structure of the CNN

data augmentation through looking at different rotations of the same 

CNN goes through 

we can adjust the size of our tensor 



#### Max pooling layer 

**Purpose:** 
* managing the dimensionality or scaling of the NN
transition so neuron represents higher level concepts in your image
* to reduce the number of neurons needed by the algorithm

2x2 max pool, takes the biggest value in the 2x2 grid and replaces that with a 1x1 maximum value.

alternatives to max pooling:
choose a different algorithm rather than the maximum operation to 

Max pooling seems like it is throwing away information but that is one job of a NN, to throw away the useless information in understandning an abstract concept.

Sam thinks that max pooling will probably get scaled back as computer performance increases as it is in some sense done for performance reasons.

#### Activation Function

Function to determine if neuron is to fire. Weights and biases combined to establish firing yes or no.

##### ReLU (most commonly used) (fast training, cheap maximum function)
* max(0,z) (doesnt suffer from exploding gradient issue from exponentials)
* dozen-100's of layer in neurl net
* back propogation needs to be able to go all the way back through many iterations and not run into exploding values.

##### Softmax (usually used in final layer)
* (to select one more prevalent neuron than the others, reinforce these signals to make a decision).
* sum of ratio of exp values.
* produces an output which does sum up to 1. (still not a probability)

PER LAYER we expect the activation function to be identical but different layers may have different function types.

ReLU and softmax are state of the art as they are in use today. However, this may change as the field is still in its infancy.

##### Other Potential options for Activation function
* Swish 
    * Google brain released this potential.
    * Continuous and differentiable. can approximate softmax or ReLU. 

* Leaky ReLU 
    * Does not completely zero a negative but gives a small value. 

#### Structure
(data objects in the CNN are tensors, which have depth)
1. Input Layer. 
2. convolution Layer 1. 
3. pooling 1. 
4. convolution 2. 
5. pooling 2. 
6. And so on ...
7. locally connected layer. 
8. fully connected layers (dealing with the abstract concepts such as identifying a bird).
9. output layer.

(Fine tuning is generally done by replacing the final layer with a number of neurons equal to the categories you want to train on.)

The number of convolution layers before pooling is customizable

vgg16 has 16 layers, but 100's can be used.
more layers = more training time.
zero padding is used to maintain dimensionality in vgg16.

**Drop out is a regularisation technique.**
Regularisation is a process to prevent overfitting.
We have neurons randomly drop out in the training process the network must become more resiliant.

#### Outputs of the CNN:

Note that these are not real probabilities, but they are sometimes probability like as they can sum up to 1 but they do not literally represent a chance of success.

It is just an indicative score of confidence.

### Code samples:
**Keras**
* Tensorflow goes down to a pure math level and is too low level for devlopment. This is where Keras comes in.

process of defining VGG16 is quite straightforward.
we define a sequential model, and then add attributes to the model with model.add.

The input shape of (3,224,224) (3 =  RGB, 224x224 = image size)

Zeropadding to avoid dimensionality change.

* convolution (64,3,3) 
    * 64 = size of the filters used in the convolution kernel
    * 3x3 = size of the convolution kernel.
    * activation function is also defined here "relu" all the way except for dense output layer. (where softmax is used).

* max pooling (2,2) 2x2 is being used in vgg16 
    * stride = how far the pooling implements across the image. 
    * strides too long  = information lost
    * 3x3 is preffered these days as it gives reasonable definition in any one direction.

As we go down layers, they increase the numbers of filters able to train on 64 to 512 (in convolution layers).

model.add(Flatten()) #We are now training on abstract concepts
This is done after the convolution and maz pooling layers.

In the dense model, the first argument is the number of neurons. 
In this case the final layer this argument has 1000 due to that being the number of categories in the competition.

dropout(0.5) (0.5 = proportion of neurons which are left out of a particular layer each epoch to avoid overfitting the model).

### Things to learn more about

* Fast R-CNN (residual convolutional neural networks)
* YOLO: Real-Time Object Detection (mentioned)
* What is fully connected layers?
* Definition of strides and the pro's and con's of a large and small stride


### Additional Resources

http://www.playground.tensorflow.org = excellent resource to play around with a simple neural net in browser to understand different parts of them intuitively.

* jitter in the picture means that the model is volitile, reduce your learning rate.
* modern frameworks will automatically drop the learning rate as the number of epochs increases.
* No flow of information to one or more neurons may mean your network has "dead" neurons and they can be pruned away.

### Add credit code:
1. Go to the AWS console and click on My Account.
2. *click credits tab*
3. Type in the code. Do the CAPCHA text and bingo bango bongo.
