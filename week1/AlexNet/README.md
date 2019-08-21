# ImageNet Classification with Deep Convolutional Neural Networks

### Questions:

##### 3.1) ReLU Nonlinearity

- Why use ReLU?

To avoid the saturation that happens with sigmoid and tanh - relu also trains faster.


##### 3.3) Local Response Normalization (LRN)

- It is done for a whole batch at once?

It seems to be done for each image - they do not talk about batch processing.

- What is the intuition of normalizing across different kernels mappings?

`The ideia seems to come from  [local contrast normalization](http://yann.lecun.com/exdb/publis/pdf/jarrett-iccv-09.pdf), which is itself based on computational neuroscience models.

As far as I can see, since we summing over the other kernels and squaring, we are kind of normalizing by the activation at that specific X, Y value in all my kernels mappings. That means if 1 kernel has a very low value and another kernel has a high value, the low value kernel will be penalized - This is a kind of **competition** among the various different kernels, that tries to give very big activities.`

We have Inter-Channel LRN (this paper) and Intra-Channel LRN; more info [here](https://towardsdatascience.com/difference-between-local-response-normalization-and-batch-normalization-272308c034ac).

- Difference of LRN to batch-normalization?

See [here](https://towardsdatascience.com/difference-between-local-response-normalization-and-batch-normalization-272308c034ac).

For one, LRN is a **non-trainable** layer, while BN we train.
BN also takes the mean/std for each pixel value, for a whole amount of data, instead of per x,y for each image as LRN.


##### 3.4) Overlapping Pooling

- Explain the intuition why overlapping pooling is better

Without it, we are loosing more spatial info, which might makie the feature useless. More [here](https://stats.stackexchange.com/questions/283261/why-does-overlapped-pooling-help-reduce-overfitting-in-conv-nets).

##### 3.4) Overlapping Architecture

- What is the size of the output first conv layer, given a 224x224x3 input and 96 kernels 11x11x3?

Trick question, the input image is actually 227x227, the original paper got the dimensions wrongs; We end up with 96 55x55

- What about after applying a max pool with stride 2 and 2x2?

We end up with 96 27x27

##### 4) Reducing overfitting

- How many "images" do we actually consider for training?

1.2 million times 2048 (data augmentation, 1024 random 224 patches and their horizonal reflection)


- What is the motivation behind dropout? ie, why would we want it?ow

By turning off some neurons, we force the neurons to not depend on a single other neuron (co-adaption), ie, learn features that are usefull with many random neurosn

- If we don't want to multiply output by P at testing time (because of time constraints), what can we do in training instead?

divide by P

- Why did they use SGD with Momentum and weight decay, that is, why isn't normal SGD enough?

Normal SGD has a problem when the ratio between the highest and lowest value of the Hessian matrix (derivates) is high! 

Because then it might move in a very zig-zag like and not really capture the gradient of the small value well/take a long time. 

Since we are in a very high dimension space (60 million params), the chance of the ratio being bad is quite high;

Also, in a very high dimension space, while the chance of local minima is very low (that is, at least 1 param should influence the loss), the change for saddle point is higher.

Because of all of this we add velocity with a friction parameter as a running mean of the gradients.


- Why did they not use Adam (SGD Momentum + RMSProp) instead of SGD Momentum?

Adam had yet to come out - the paper was published in 2014 ;)


- Why didn't they use Xavier initialization?

I am actually quite not that sure about this - a zero-mean Gaussian with low std isn't a bad idea, but probably isn't the best either - it could just be that the model wasn't that deep yet.

It could also be because the paper about Xavier initialization (Understanding the difficulty of training deep feedforward neural networks) does not mention ReLU as a activation function.

Also, Xavier initialization came out in 2010 - it could have not caught on yet.



