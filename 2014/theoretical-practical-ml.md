@(Cabinet)[thinking|research_ideas|published]

# On Theoretical and Practical Machine Learning

## Supervisor Said...
It all started with a casual conversion with my supervisor. I told him that I would work on proving a high-probability bound of a randomized algorithm as it seemed to be more practical than asymptotic bounds. But he said in fact there is no practitioners caring about any kinds of bounds at all, which shocked me at first. However, it is right in the sense that most NIPS and ICML papers only give asymptotic convergence analyses. Due to the bias-variance trade-off, if an algorithms A has better asymptotic properties than B when given infinite data, then B will probably perform better in practice when given limited data. 

## Only Applications?
To be clear, I have two supervisors: one working on theories of machine learning and another one more focusing on applications of machine learning to social media.

It seems to me that the students and interns in the social media lab almost have no idea about various bounds. Currently, due to the popularity of deep learning, they tend to apply it to any topics they can think of, without knowing anything about the theories behind it. On the other hand, the students in the theoretical lab do not give a shit to applications. Well, I'm not saying applications are not important or interesting. But there apparently is a (huge) gap between theoretical and practical machine learning algorithms and research.

Yoshua Bengio once argued that if an algorithm works very well in practice but with little theoretical guarantees, it just means that theories are inadequate; if theories do not agree with empirical successes, theories are wrong. I guess this is also partly why [Elon Musk said](http://www.quora.com/Is-Elon-Musk-right-in-saying-most-academic-papers-are-useless) *most* academic papers were useless.

## Role of Theoretical Guarantees
In the paper *A Few Useful Things to Know about Machine Learning* written by Pedro Domingos, he says:

> The main role of theoretical guarantees in machine learning is not as a criterion for practical decisions, but as a source of understanding and driving force for algorithm design.

Anyway, I still feel that high-probability bounds for randomized algorithms are slightly more useful...