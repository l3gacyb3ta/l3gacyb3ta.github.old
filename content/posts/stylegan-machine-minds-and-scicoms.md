
---
title: Stylegan2, Machine Minds, & Science Communication
date: 2021-04-16 18:42:52
tags: ["Stylegan2", "AI", "SciCom"]
---


AI is becoming a more and more important topic in our daily lives, and understanding has stayed about the same. I'm here to fix that! One of the very interesting new types of AI are GANs. For this article I'll be talking about one [Stylegan2](https://arxiv.org/abs/1912.04958). Stylegan2 is a huge leap in image generation GANs. I know I am a *bit* behind on this whole shebang, but I just found out that I could run Stylegan2 myself, so I wanted to write about it!



First, what even is a GAN? GAN stands for **G**enerative **A**dversarial **N**etwork. A GAN is a set of two AIs that work together to create original content. GANs are made up of two neural nets, a generator  and a discriminator. They are trained by feeding the training images to both the generator and the discriminator, the way you would usually train a NN. But then the fancy GAN-tech kicks in. The second phase of training is where the generator tries to generate images that the discriminator will classify as real, so that we can get the most realistic images possible. The discriminator also learns from its mistakes, making the whole model more effective as training time goes on. The good thing about this type of model is that it can be trained on some very complex data, such as audio, images, and even video!



"Now, what about this Stylegan2 thingy-ma-bob?", you may be asking. Well Stylegan2 is a GAN that has been optimized for images and even has some pre-trained models out there! One of the most impressive examples is the version trained on the FFHQ face dataset. It can generate images that are basically indistinguishable from normal photos of faces. 



For example, can you determine which of these photos is real?



![An AI generated image and an actual photo](Untitled.png)



If you guessed the kid on the left is real, good job! You're better at this than me! If you want to play this game, check out [whichfaceisreal.com](https://www.whichfaceisreal.com/)! The AI does have some telling features that can show an image is fake. Things that don't really pertain to images of faces, or whatever dataset you have, such as logos and people in the background, tend to get messed up. Here are some examples I found of weird stuff that the site [thispersondoesnotexist.com](http://thispersondoesnotexist.com) generated:



![Bad baseball cap generation](Untitled%201.png)



Ah yes, the Ḇ̸̨̢̨̼̟̰͈̞͍͈͓̼̫̞̒͂̒͛͌̌̓́͠͝ͅa̸̡̪̘̗̣͚̫̬͔͉̙͎̫̺̘̣͚̲͉͉̱͔̭͆̀́̃͘͜͠l̶̢̬͔͈̻̣̬̮͇̠̯̩̲̂͑̆̇̓̇̉̏̒͛̉̕͜͜͜t̵̨̡̧̛̙̬̬̫͎̱͔̺͕̩̳̪̳͔̟̖͓̪̲͇͉͍̀̓̐̈́̉̈̆̋͋̑̉͆̃̇͐͒͘i̸̔͗̍̐̓̅̔͌͛̊̅̆̏̾͌̚̚̕͝m̶̦̤̜͕̃̓̾̽̄̆̑̒͋͠a̵̛̰̰̽͆́̑̎̽̊͆̾́̇̅͊̇̇̑̚͘͘ṇ̴̜͉̽̏̋̅̐̃̋̈̓͆͗̽̾̀͌̋̆̓̇̎̑͗̚͘͝ ̷͌̈́̔͂̑̔̇̀̿̄̾̆̾̿͐̈́̚͠͝ are my favorite team.



Another fun thing that you can do with these really interesting AIs is watching them show how they think features evolve across multiple datapoints (those being images of faces). Here is a little video I generated with [this](https://colab.research.google.com/drive/1ShgW6wohEFQtqs_znMna3dzrcVoABKIH?authuser=2) Google Colab notebook (If you want to train your AI locally, instead of using a pretrained model, try [this](https://github.com/lucidrains/lightweight-gan)).



[A trippy interpollation](mov-10.mp4)



As you can see, at some points, it gets a bit confused, and it has some issues with people in the background. This is really interesting to watch, as we get a rare peek into the mind of a machine. Another *really* cool look into the minds of computers is the [Aphantasia](https://github.com/eps696/aphantasia) project. It uses a model called CLIP, that helps guide AIs using natural language and a GAN to generate those images. These images are gradually refined from random noise that was generated for the AI in the beginning. Here is a video of the AI generating an image based on the prompt "A woman walking her dog with her child" or something to that effect.



[Anoter interpolation](download.mp4)



Trippy, right? This is really a really interesting view into the way NNs, GANs, and other kinds of mechanical minds think! Fun experiments, and other interesting projects like this will be the best way to explain the ways that the computers that more an more control our lives work. Fun videos and websites like this can also be a very effective science communication method. Methods of explaining complex AI systems to laypeople will be *very* important in the coming years.



Please note: I am *not* an expert in this field, and am just presenting some thoughts I typed out during science class.



Sources:



- [https://arxiv.org/abs/1912.04958](https://arxiv.org/abs/1912.04958) ← Original Stylegan2 study!

- [https://medium.com/analytics-vidhya/gans-a-brief-introduction-to-generative-adversarial-networks-f06216c7200](https://medium.com/analytics-vidhya/gans-a-brief-introduction-to-generative-adversarial-networks-f06216c7200e#:~:text=GANs%20consists%20of%20two%20networks,those%20in%20the%20training%20set.&text=They%20both%20work%20simultaneously%20to,audio%2C%20video%20or%20image%20files)

- [https://towardsdatascience.com/stylegan2-ace6d3da405d](https://towardsdatascience.com/stylegan2-ace6d3da405d#:~:text=The%20authors%20of%20StyleGAN2%20explain,in%20these%20water%2Ddroplet%20artifacts)

- [https://habr.com/en/post/537334/](https://habr.com/en/post/537334/)