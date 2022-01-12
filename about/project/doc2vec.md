---
layout: page
title: Doc2Vec and neural nets
bodyclass: project
---

What is a neural net? What does it mean to train one on a document corpus?

## What is a neural net?
> Machine learning is the science[^1] of getting computers to act without being explicitly programmed.
>
> Andrew Ng, [Machine Learning](https://www.coursera.org/learn/machine-learning)

In traditional programming, the programmer defines a set of rules for the computer to follow, and the computer applies those rules to input data in order to generate outputs. For example, if I wanted a robot to be able to make a cake, I might put all the ingredients on a table, and provide a step-by-step recipe: first, mix the dry ingredients...

In machine learning, the programmer gives the computer a lot of data, a general plan of how to process it, a goal, and a way to determine if it's done a good job achieving that goal. However, the programmer does _not_ write specific rules. In this instance, I would put a lot of ingredients on a table, give instructions for a few cooking techniques, tell a robot what a cake is, and leave the kitchen. The robot would then learn through trial and error: try something random with the ingredients and techniques it knew about; see if the result was a cake; and use what it learned to make something slightly more cakelike next time. While the early attempts are likely debacles, given enough time to experiment, the robot eventually (we hope) makes a credible cake. It may (and probably will) follow procedures completely alien to human chefs, but it's the result that counts.[^2]

There are many possible computational techniques for machine learning, but neural nets have largely taken over in recent years due to their sometimes-spooky effectiveness across a wide range of problems. Inspired by brain science, neural nets are large collections of tiny programs, each of which does a little bit of computation and then communicates its results to other programs — kind of like neurons in the brain communicate with each other to collaborate on large-scale problem-solving. The programmer defines what kind of equations each neuron uses, and which ones connect to which others. Thus, for instance, I might tell neurons in the second layer to look at all the outputs of the first layer; apply an equation of the form `y = mx + b` to those inputs (`x`); and send that output `y` to the third layer.[^3] However, the computer figures out the specific values (here, `m` and `b`) that all the equations use. Updating these through its trial-and-error process is the "learning" part of "machine learning".

Computation of this nature underlies a huge number of the apps you use every day. Its uses include automatic translation; photo tagging; book recommendations; and more.

## What is Doc2Vec?
I noted that "the programmer defines what kind of equations each neuron uses, and which ones connect to which others". In other words, there are many algorithms and architectures that we can choose from in defining a neural net and giving it a framework for learning. Doc2Vec is one of those algorithms. It was designed for processing texts of variable lengths in order to compare and classify them.[^4]

How does it work? The computer reads in documents one word at a time, examining a sliding window of words along the way. It infers that words that frequently occur near one another probably have some kind of relationship. For instance, here are three ten-word windows, taken from (respectively) the Thirteenth, Fourteenth, and Fifteenth Amendments:

> ...Congress shall have power to enforce this article by appropriate...
>
> ...The Congress shall have power to enforce, by appropriate legislation, ...
>
> ...The Congress shall have power to enforce this article by...

The neural net would notice that "Congress", "power", "enforce", and (to a lesser extent) "article" and "appropriate" tend to go together. As it continued sliding its ten-word window, it would rapidly discover that "legislation" is close to "enforce", "article", and "appropriate" in all of these documents too — and it would infer thereby that "legislation" likely has something to do with "Congress" as well.

This process underlies the algorithm Word2Vec.[^5] Doc2Vec builds on this by adding a secret extra word to every window, which is a label identifying the whole document. In this way, it learns what a document is "about" by learning what words are in it. By reading through the entire document, it's able to take into account which words are most common. And by iterating through this process multiple times, it can take into account what it's learned from previous passes about word similarity. For instance, if a document never contains the word "Congress", but does contain words like "legislation" and "enforce", it is probably at least somewhat related to documents that talk about "Congress" a lot.

For a more in-depth explanation (or if you prefer video), please see [my 2021 Code4Lib talk](https://www.youtube.com/watch?v=Iun5ZYuuBQA&t=2245).

You may have noticed that text might make this process harder for spurious reasons. For instance, "power" and "powers" are not really different in meaning, but the computer would not know they are the same word. Alternately, "power" and "powers" are different in meaning, in the phrases "Congress shall have power..." and "The Hoover Dam powers the Southwest"! Similarly, "legislation" and "Legislation" are not different in meaning, but the computer would see them as different words. Worse yet, the typo "legis1ation" (note the number) is likely meant to be "legislation", but the computer would see them as distinct. In addition, some words (such as "a", "the") occur constantly and add little or no information about _meaning_.

Doc2Vec is surprisingly good at sorting through minor discrepancies, given enough examples. However, a certain amount of data cleaning may be helpful or even necessary to get good results. I have a separate page on [how I handled data cleaning in this project]({% link about/content/data-cleaning.md %}).

## From Doc2Vec to the browser
When the neural net is done training, it represents every document (and word) as a _vector_: a set of numbers identifying a point in space. For example, you may recall graphing points like `(0.5, 1.3)` in math class. `(0.5, 1.3)` is a _two-dimensional vector_. You can represent it either as that list of numbers or as a dot on paper, and they mean the same thing.

Doc2Vec represents words as vectors, but with many more dimensions (the default is 100). These are straightforward to represent as lists of numbers: your list just has (say) 100 numbers instead of 2. They're harder to visualize or draw, since you would need hundred-dimensional paper.

In order to represent the vectors in the browser and make them meaningful, we need to _project_ them down to two dimensions. Think about the way a light shining on you projects a shadow behind you. You have a three-dimensional shape, but your shadow has only two dimensions. Its shape resembles yours in meaningful ways, but it also loses some details. Furthermore, depending on how you cast the light, where you stand, et cetera, your shadow may be distorted: shrinking to nothing at noon on the equator; stretching much farther than your height when the sun is low.

You might also think about photographs, which capture three-dimensional scenes in a two-dimensional medium. Imagine taking a selfie on the National Mall with the Washington Monument in the background. The pixels depicting your face may be right next to the pixels depicting the monument, because of the way the photograph flattens space. However, in all likelihood, you are standing quite far away from the monument! As humans, we're good at using visual cues in the scene, like relative sizes, to infer that objects which are adjacent in a two-dimensional photograph aren't actually touching in real life.

There are numerous techniques for projecting high-dimensional vectors down to fewer dimensions. Based on Dr. T.J. Jankun-Kelly's literature review and ease of use of the available tools, I used [UMAP](https://umap-learn.readthedocs.io/). I also used two dimensions rather than three, following his advice. While it's possible to depict three dimensions, and in theory this would lose less information than using only two, in practice people find it hard to understand three-dimensional data visualizations.

## What does this mean for this project?
Every dot you see is a document. They're positioned in the browser based on their similarity, as inferred by the neural net.

Ideally, Doc2Vec has captured _overall similarities_ between documents, and UMAP has projected document vectors down to two dimensions in a way that retains _broad structures_.

However, it's still up to us, the viewers, to look for things that _might_ be structures and evaluate whether they are. Similarly, we must be mindful that documents that truly are related don't always end up together, and documents that are adjacent in two dimensions may be far away in the original 100. The visualization provides broad entry points, but not reliable specifics.

I've tried to experiment with UMAP parameters and dot-coloring options in ways that let you see possible structures. I invite you to investigate what's really there, and talk about it with the hashtag `#SituatingUs`.

## Notes
[^1]: While Ng characterizes machine learniing as a science, I think it would be more acccurate to say "science, or possibly art". In practice machine learning is often highly empirical (if you feel charitable) or deeply atheoretical (if you don't); that is, there's a lot of experimenting with system parameters to find an output that gets the job done. This experimentation may be driven more by intuition, experience, or aesthetics than theory.

[^2]: For a much more thorough — but approachable and hilarious — explanation, see Janelle Shane's [_You Look Like A Thing And I Love You_](https://bookshop.org/books/you-look-like-a-thing-and-i-love-you-how-artificial-intelligence-works-and-why-it-s-making-the-world-a-weirder-place/9780316525244).

[^3]: The equations are somewhat more complicated in practice, but not as much as you might think. `y = mx + b` is a surprisingly good analogy in many cases.

[^4]: Quoc V. Le and Tomas Mikolov. ["Distributed Representations of Sentences and Documents"](https://arxiv.org/abs/1405.4053).

[^5]: Tomas Mikolov, Kai Chen, Greg Corrado, and Jeffrey Dean. ["Efficient Estimation of Word Representations in Vector Space"](https://arxiv.org/abs/1301.3781).
