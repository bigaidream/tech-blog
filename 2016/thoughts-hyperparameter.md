# Thoughts on Hyperparameter Optimization for Deep Learning

> Date: 2016-June-12

> Author: Jie Fu, http://bigaidream.github.io/

## Motivation: important things only

> When I read papers, I always wonder how the authors really come up with those ideas. Thus I'm trying to share my mental journeys here. 

As shown in [Bayesian Optimization of Text Representations](http://arxiv.org/abs/1503.00693), standard linear models tuned carefully can be competitive with more sophisticated, expensive state-of-the-art methods based on latent variable models or neural networks on various topic classification and sentiment analysis problems. A nice review is [Taking the Human Out of the Loop: A Review of Bayesian Optimization](http://ieeexplore.ieee.org/xpls/abs_all.jsp?arnumber=7352306).

Currently, it seems that only Google, Twitter or Facebook have the ability to automatically tune hyperparameters with their huge computer clusters. I personally know a PhD student who designed a new algorithm and compared it with a vanilla RNN. He said the RNN is with "defaut" settings and thus it's fair, which is definitely not! Because the number of  his specific dataset is much smaller than the one used in the RNN reference paper, the RNN used in his experiment is overfitting. Similar observations can be found in the paper [LSTM: A Search Space Odyssey](http://arxiv.org/abs/1503.04069). 

I decide to work on efficient and effective hyperparameter optimization problems so that machine learning researchers/practitioners can focus more on real and important research problems without worring about hyperparameter tuning. 

## BO seems not suitable for tuning deep learning
I played around with Bayesian optimization, BO,  (or called bandit) for tuning learning rates since 2014, but it failed utterly. In contrast to DQNs, most of the BO algorithms have very rigorous proof (this is even partially true for Thompson sampling). 

However, BO algorithms usually (except for contextual or dynamic bandits) only have one state, and they do not have influence over the environment but only sense and learn from it. 

Put this into the context of tuning learning rates, BO methods are not aware of the impacts to the learning tasks brought by the modification of learning rates. 

I kept trying to apply/extend BO to hyperparameter optimization till the end of 2015. I felt that BO based hyperparameter tuning methods are so all-consuming: need lots of machines for weeks to tune less than 20 hyperparaemters. 

## [DrMAD](https://github.com/nicholas-leonard/drmad)
Last December, I came across the paper [Gradient-based Hyperparameter Optimization through Reversible Learning](http://arxiv.org/abs/1502.03492). It's a very promising direction but not practical yet. 

At that time, I was also watching [One Punch Man](https://www.youtube.com/watch?v=_TUTJ0klnKk). The bald hero can always knock down the opponent in only one hit. Then I said to myself: can I do hyperparameter optimization also in one punch?

This is actually not that crazy. Sometimes, a very simple method can solve a big problem, such as the paper [Single Image Haze Removal using Dark Channel Prior](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=5567108&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D5567108). 

After having a rough idea, I did a brainstorm. Then I remembered that in the paper [Qualitatively characterizing neural network optimization problems](http://arxiv.org/abs/1412.6544), Ian Goodfellow showed that a very neat way to visualize the training trajectory of deep learning, which might be useful for my task. The following things become relatively easy.  

## Lesson learned

>Choose an 'important question' - that is, one that addresses a fundamental issue in the field; these questions might or might not be 'trendy'. Note that trendy areas are inevitably (and often inappropriately) competitive, and that future trends are not always predictable.  

[Choices in neuroscience careers](http://www.nature.com/nrn/journal/v9/n5/full/nrn2386.html), Nature Reviews Neuroscience, 2008, Tamas Bartfai, Tom Insel, Gord Fishell & Nancy Rothwell. 