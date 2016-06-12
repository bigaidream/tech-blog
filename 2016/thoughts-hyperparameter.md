# Thoughts on Hyperparameters Optimization for Deep Learning

> Date: 2016-June-12
> Author: Jie Fu, http://bigaidream.github.io/

## Real Motivations: Alleviating the Avalanche of Low-Quality Research

> When I read papers, I always wonder how the authors really come up with those ideas. Thus I'm trying to share my mental journeys here. 

As shown in [Bayesian Optimization of Text Representations](http://arxiv.org/abs/1503.00693), standard linear models tuned carefully can be competitive with more sophisticated, expensive state-of-the-art methods based on latent variable models or neural networks on various topic classification and sentiment analysis problems. 

In my opinion, some so-called `novel` ML application papers do not contribute to real knowledge. They propose a new method (tuned carefully) and compare it with other baseline method without tuning them carefully/at all. I personally know a researcher who designed a new algorithm and compared it with a vanilla RNN. He said the RNN is with `defaut` settings and thus it's fair, which is definitely not! Because the number of  his specific dataset is much smaller than the one used in the RNN reference paper, the RNN used in his experiment is overfitting. In other words, much of the improvements of so-called new methods come from the carefully tuned hyperparameters, instead of the new algorithms themselves. Similar conclusion can be found in the paper [LSTM: A Search Space Odyssey](http://arxiv.org/abs/1503.04069). 

To be honest, I might be able to graduate by publishing this kind of papers, but doing so will never help me with my big AI dream. I thus decide to work on efficient and effective hyperparameter optimization problems such that machine learning researchers can focus more on real and important research problems, rather than publishing papers with only negligibly incremental improvement. 

## BO seems not appropriate for tuning DNN
I played around with Bayesian optimization, BO,  (or called bandit) for tuning learning rates since 2014, but it failed utterly. In contrast to DQNs, most of the BO algorithms have very rigorous proof (this is even partially true for Thompson sampling). 

However, BO algorithms usually (except for contextual or dynamic bandits) only have one state, and they do not have influence over the environment but only sense and learn from it. 

Put this into the context of tuning learning rates, BO methods are not aware of the impacts to the learning tasks brought by the modification of learning rates. 

I kept trying to apply/extend BO to hyperparameter optimization till the end of 2015. I felt that BO based hyperparameter tuning methods are so all-consuming: need lots of machines for weeks to tune less than 20 hyperparaemters. 

## DrMAD
Last December, I came across the paper [Gradient-based Hyperparameter Optimization through Reversible Learning](http://arxiv.org/abs/1502.03492). It's a very promising direction but not practical yet. 

At that time, I was also watching [One Punch Man](https://www.youtube.com/watch?v=_TUTJ0klnKk). The bald hero can always knock down the opponent in only one hit. Then I said to myself: can I do hyperparameter optimization also in one punch?

This is actually not that crazy. Sometimes, a very simple method can solve a big problem, such as the paper [Single Image Haze Removal using Dark Channel Prior](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=5567108&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D5567108). 

After having a rough idea, I did a brainstorm. Then I remembered that in the paper [Qualitatively characterizing neural network optimization problems](http://arxiv.org/abs/1412.6544), Ian Goodfellow showed that a very neat way to visualize the training trajectory of deep learning, which might be useful for my task. The following things become relatively easy.  

## QAN
After finishing DrMAD project, I came across the paper [Train faster, generalize better: Stability of stochastic gradient descent](https://arxiv.org/abs/1509.01240). Then I thought it might be interesting to design a practical method to improve deep networks. 

As I got familiar with BO, I first did a brainstorm based on BO. Then I realized that, to some extent,  a DQN can be seen as a BO by adding more states and the ability to change the environment. 

In fact, I first became interested in reinforcement learning when I was doing Masters in New Zealand. Lots of difficult computer vision tasks seem very ill-posed and unnatural to me. For example, when a baby sees a part of an object in distance, she will probably move towards that direction trying to observe it from more perspectives and touch or even bite it; she would rarely try to guess what the object is by sitting there and staring. 

Next, I decide to cast this problem into a Atari game problem, which has already been solved using DQN. 

Let's look at the following animation on the training of some convolutional filters:

http://cs.nyu.edu/~yann/research/sparse/psd-anim.gif

Imaging that we are playing a weird Atari game with the above screen. The screen seems simpler than real Atari games'. This reminds me the difference between biomedical image processing and natural image processing. In biomedical images, the objects (e.g. red blood cells) are much simpler, thus needing simpler models. 

Compared to real Atari games, however, the positions of filters change at every episode due to the global update mechanism of back-propagation. To solve this, we need a way to fix them. 

Since I just finished DrMAD project, I know that the training trajectories of deep learning training between episodes tend to be similar. This reminds me of regression tasks. Interestingly, this can be seen as a catapult used in Angry Birds: at every episode, we use a regressor to "project" the DNN into the somewhat similar trajectory. 

The following things should be relatively easy. 

## Lessons Learned

>Choose an 'important question' - that is, one that addresses a fundamental issue in the field; these questions might or might not be 'trendy'. Note that trendy areas are inevitably (and often inappropriately) competitive, and that future trends are not always predictable.  

Nancy Rothwell, Choices in neuroscience careers, Nature Reviews, 2008.