# ImageNet Classification with Deep Convolutional Neural Networks

### Questions:
##### 3.1) ReLU Nonlinearity

- Why use ReLU?

##### 3.3) Local Response Normalization (LRN)

- It is done for a whole batch at once?

- What is the intuition of normalizing across different kernels mappings?

- Difference of LRN to batch-normalization?


##### 3.4) Overlapping Pooling

- Explain the intuition why overlapping pooling is better


##### 3.4) Overlapping Architecture

- What is the size of the output first conv layer, given a 224x224x3 input and 96 kernels 11x11x3?


- What about after applying a max pool with stride 2 and 2x2?


##### 4) Reducing overfitting

- How many "images" do we actually consider for training?


- What is the motivation behind dropout? ie, why would we want it?ow


- If we don't want to multiply output by P at testing time (because of time constraints), what can we do in training instead?


- Why did they use SGD with Momentum and weight decay, that is, why isn't normal SGD enough?


- Why did they not use Adam (SGD Momentum + RMSProp) instead of SGD Momentum?


- Why didn't they use Xavier initialization?


