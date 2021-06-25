---
title: Images made by writing bots?
date: 2021-02-18 00:04:50
tags: ["title: images made by writing bots?"]
---

~Soo~ today we have something a tad bit more complicated, so first I\'ll introduce a few concepts and tools:



1\\. Markov chains: From [simple.wikipedia.org](https://simple.wikipedia.org/wiki/Markov_chain): "A **Markov chain** is a model of some random process that happens over time. Markov chains are called that because they follow a rule called the Markov property. The Markov property says that whatever happens next in a process only depends on how it is right now (the state). It doesn\'t have a "memory" of how it was before. It is helpful to think of a Markov chain as evolving through discrete steps in time, although the "step" doesn\'t need to have anything to do with time."  

  



2\\. Jupyter notebooks: Jupyter notebooks are a way of sharing code, usually, academic and running it in a presentable and browser-friendly format. I\'m gonna share my code in Google\'s free notebook hosting service, collaboratory.



Now, usually, Markov chains are used to generate text, as seen [here](https://towardsdatascience.com/simulating-text-with-markov-chains-in-python-1a27e6d13fc6), and [here](https://www.kdnuggets.com/2019/11/markov-chains-train-text-generation.html). But, I\'ve done something weird. I\'ve generated images.



"Well l3gacy, how does this work?" - You, now, probably. It\'s pretty easy actually!



First I take in 3 training images (I know that\'s not a lot, any more and it took hours to run), here I chose 3 pieces of Bauhaus art. These are then converted into a list of the RGB values in the images. This is then fed into the Markov chain algorithm. Usually, it expects the list input to be a list of words, but here I fed the RGB values. It then does its Markov-magic and spits out an output image.



Right now, the output is in the form of a list of RGB pixels as a string, so we convert it back, turn it into an image, and show it!



Bam! Machine-generated images!



![out](https://i.ibb.co/1QDxDXZ/out.png)



Now, this is interesting. We can tell from the way there are horizontal lines, the way that this algorithm is supposed to work, as it usually would write words from left to right.



If y\'all wanna play around with the code, here\'s a [google collab link](https://colab.research.google.com/drive/1XB0W5QB5iStSwtMCCCPBHz5AxMkNXUYP)



That\'s it! Thanks and goodbye.



\\-l3gacy
