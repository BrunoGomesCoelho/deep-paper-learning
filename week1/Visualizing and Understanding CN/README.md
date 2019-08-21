# Visualizing and Understanding Convolutional Networks

### Questions:

##### 1) Introduction

- Why do we even care about feature visualization?

It helps show that our model is learning something reasonable;
It might work as a kind of AI interpretability;
Allows us to better our training process by seeing erros during training and the features generated


##### 2.1)  Visualization with a Deconvnet

- How do we deal with "unpooling" a pooling layer, making a small image bigger?

We use "switches" (term created by the paper) for maintaining the coordinates of the pixel that was selected as a max value. When unpooling, we then make that coordinate the value that we have and the rest of the pooling region 0.


- Why do we not use transpose convolution for upsampling the image instead of the max unpooling above?

We don't want to actually train for the upsampling operation that gives a "minimal" loss - instead we want to undo the operations we have done, so it doesn't make sense to learn a upsampling.


##### 4) Covnet Visualization

- What do we visualize in the simplest, basic unit? Is it a layer, a feature map, a value of a feature map, ...?

It is one single value (neuron) of a feature map.

- How come we generate both a activation and a image patch? Does the model generate these pictures? Are they training images?

This seems a bit tricky/badly explained in the paper.

Once we have a fully trained model, we pick a layer/feature map and get one of the maximum activations, the use a Deconv net backwards to project it onto pixel space. These are the greyish images with features in them.

Given these feature maps, we get a whole bunch of images in our validation set (that is, that were not used in training) and check which of them give a high activation for our specific feature map - for those images we did pick, we them "sum" them.


- What changes do they propose to the original AlexNet and why?

Sometimes, a quote is best:

"The first layer filters are a mix of extremely high and low frequency information, with little coverage of the mid frequencies. Additionally,the 2nd layer visualization shows aliasing artifacts caused by the large stride 4 used in the 1st layer convolutions. To remedy these problems, we (i) reduced the 1st layer filter size from 11x11 to 7x7 and (ii) made the stride of the convolution 2, rather than 4."


- Discuss feature generalization in the context of this paper.

In the end, the features found by the improved AlexNet architecure gernalized very well to other training tasks, even for few-shot or one-shot approaches. 

This shows how the features the net finds are very relevant and useful - further, it learns for example to identify human faces, even though humans is not one of the original 1000 categories, but it is probably very usefull for other categories.


