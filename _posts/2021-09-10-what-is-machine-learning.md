---
layout: post
title:  "What is Machine Learning?"
date:   2021-09-10
read: 8
description: What machine learning actually is, and the main types of machine learning algorithms.
categories: machine learning
---

---

![](/assets/images/posts/2_machinelearning/post.jpg#colour-correct)

# Machine Learning

Machine learning is a buzzword that you probably have heard a lot recently, but what exactly is it?

**Machine learning** is an application of **artificial intelligence (AI)** that provides systems the ability to automatically learn and improve from experience without being explicitly programmed. 

In other words, 
> Machine learning algorithms enable machines (or, more accurately, systems and **models**) to **learn from experience** as humans do.

## So how do models learn with Machine Learning?

Machine learning models learn from **experience**, just like humans.

### Humans learn from experience. 

Humans are experts in learning from experience. We have been doing this since we were babies.

- After falling multiple times, babies learn what to do and what not to do, and eventually learn how to walk. 
- Ask someone who knows nothing about chess to watch two players playing chess. After a few rounds, they will be able to deduct from their observation that rooks move only in straight lines, bishops only in diagonals, and so on. 

From experience and observation, humans learn to **group, classify and identify patterns**. With more experience and learning instances, the patterns identified become increasingly accurate and closer to the ground truth.

### Machine Learning

Machine learning is essentially the same concept. Using the human analogy, **models** are the humans, and **data** is the learning instances.

Data collected from various sources (sensors, user-generated, etc) is fed into a model. The model then looks for patterns in the data. Using these patterns, the model is able to make better decisions. Generally the more data the model is fed, the better it will be at identifying patterns.

<hr style="border-style: dashed">
## Machine Learning (ML) vs Artificial Intelligence (AI)

Now before we move on...

You may have heard these two terms (machine learning and AI) often mentioned together or even used interchangeably. So let me demystify them for you. 

Are ML and AI the same thing? 
>**Machine learning (ML) is a subset of artificial intelligence (AI)**.

![Artificial Intelligence vs Machine Learning](/assets/images/posts/2_machinelearning/AI_vs_ML.png)

**Artificial intelligence (AI)** is the broad science of mimicking human abilities. It comprises a multitude of fields, including but not limited to:
- robotics, 
- speech processing, 
- computer vision,
- machine learning

These fields cover a wide array of applications that involve mimicking human abilities to solve or improve everyday problems.

**Machine learning** is a specific subset of AI which mimics the human ability to learn. 

<hr style="border-style: dashed">

# Types of Machine Learning

There are three main types of machine learning: 
1. Supervised learning
2. Unsupervised learning
3. Reinforcement learning 

The types can be easily differentiated based on their use cases and the existence of data labels. 

>An important concept of machine learning is **data labelling**. Let's assume the data we have is in the form of images of cats and dogs. Depending on the use case, we can choose whether to label each image. If we do, we might label each image as either a "cat" or a "dog". The data labels, or lack thereof, are essential in our machine learning applications, as we will see below.

## Supervised Learning

>A supervised learning model uses labelled data for its learning. 

In supervised learning, the model takes in labelled data samples and learns the correlation between the data samples and their corresponding labels. The model is "supervised" by the labels attached to the samples, hence the name supervised learning. When given a new piece of data, the model will use what it learned to predict the label for this new data. 

A common task that uses supervised learning is **classification**. Classfication is the act of classifiying data, i.e. assigning labels to data. Classification is widely used. The most common applications include:

1.  **Face detection**
    
    Detecting a face in an image. This can be detecting the presence of a face in the image or even determining the exact location (in terms of pixels) of a face, if present, in the image.

    For detecting the presence of a face in an image, the data will comprise images with and without faces, and the label to each image will be `True` if the image contains a face and `False` if the image does not contain a face. After learning, when given a new image, the model will then be able to predict whether the image has a face by predicting the label for the new image to be either `True` or `False`.
    
2.  **Object detection and classification**
    
    This is similar to face detection but for objects. Typically these problems involve detecting and classifying multiple types of objects in an image.

    For example, for a self-driving car to safely manoeuvre a busy road, it is important to know the different objects present on the road. From an image of the road taken with sensors or cameras on the car, the model needs to not only be able to detect the presence and location of stop signs, pedestrians, trees, pavement, etc. in the image but also to classify those objects correctly as stop signs, pedestrians, trees, pavement, etc.
    
3.  **Speech recognition**
    
    This is a common task which forms the basis of auto captioning services and voice assistants. Speech recognition is the task of transcribing speech, i.e. converting speech to text. The data for this task is in the form of speech audio and the label to each speech audio is the text corresponding to what's said in the audio. After learning, the model will be able to transcribe a new speech audio.

    You can learn more about speech recognition in this [blog post]({% post_url 2021-09-22-automatic-speech-recognition %}).

As can be seen in the examples above, the problem involves data with labels. The model learns the correlation between the data and the labels. When given new data, the model then applies what it learned to predict the label for the new data.

## Unsupervised Learning

While supervised learning uses labelled data, 
>Unsupervised learning uses unlabelled data.

Due to the lack of labels, unsupervised learning problems are not about predicting labels for data, but about grouping and clustering data.

A common task that uses unsupervised learning is **clustering**. Clustering is the problem of grouping data into clusters. Given a set of data samples, a model is tasked to group the data into several clusters. What the model will strive to learn is the criteria to group these clusters. When given a new piece of data, the model will use the criteria it learns to assign the new data to one of the clusters. The number of clusters is often specified by us humans.

For example, given data comprising images of dogs, cats, birds and humans, we can task the model to learn to group them into `n` clusters. Depending on `n`, the model might learn to group the images into:
1. dogs, cats, birds and humans (if `n = 4`)
2. mammals and birds (if `n = 2`)
3. walk on 4 limbs and walk on 2 limbs (if `n = 2`)

Note that in the second and third examples, the model groups the images differently desipte being given the same `n`. Bear in mind that both criterias for clustering are valid. Since there are no labels, we humans will have no idea how the model will end up clustering the data. It is our job to study the clusters after the model finishes its learning in order to figure out the reasoning behind the clustering (i.e. is it animal classes or number of limbs?).

<hr style="border-style: dashed">
### Classification vs Clustering
In classification, the model effectively "clusters" the data into groups based on labels attached to the data (by us humans). In clustering, the model has to learn that on its own. This means that it is possible for the model to learn criteria for clustering that we humans had never thought of before!
<hr style="border-style: dashed">

## Reinforcement Learning

Finally, reinforcement learning. 
>**Reinforcement learning** is an area of machine learning concerned with learning to make a sequence of decisions. 

In reinforcement learning, the model learns not only from experience but also from **rewards** and **punishments**. This is analogous to how a baby learns to walk. 

Initially, a baby might move their limbs in a certain way. Unfortunately, they fall. This is a **punishment**. The baby will then alter the way they move their limbs and try again. This time they are able to stand straight. This is a **reward**. The baby will remember that and tend to replicate that action. Through trials and errors, the baby learns to optimise their actions and limb behaviours to reduce the occurence of a punishment and to increase the occurence of a reward. By doing so repeatedly, the baby eventually learns to walk.

A reinforcement learning model does the same thing. Take an example of a model tasked to play chess. The model will be given the rules of chess and it should take it from there to learn how to win a game. Initially, the model does not know what moves are optimal. By trying different moves and playing many games, the model is able to learn an optimal strategy based on the rewards (when it wins) and punishments (when it loses) it receives. Over the trials, the rewards and punishments reinforce the optimality of strategy, allowing the model to improve constantly until the maximum achievable optimality. 

<figure>
<img src="/assets/images/posts/2_machinelearning/kasparov_vs_deepblue.jpg" alt="Kasparov vs Deep Blue">
<figcaption>1997: Garry Kasparov vs. Deep Blue</figcaption>
</figure>

Reinforcement learning is in fact the main algorithm behind the iconic defeat of chess world champion Garry Kasparov by [Deep Blue](https://en.wikipedia.org/wiki/Deep_Blue_(chess_computer)) in a historic [six-game match](https://en.wikipedia.org/wiki/Deep_Blue_versus_Garry_Kasparov) in 1997. Since then, more models have been created that are able to defeat world champion human players in various games of even higher complexity like [AlphaGo](https://en.wikipedia.org/wiki/AlphaGo) in the chess game Go and [OpenAI Five](https://en.wikipedia.org/wiki/OpenAI_Five) in the multiplayer online game Dota 2.

# Conclusion

Machine learning is a rapidly growing area of interest due to its wide array of applications and capabilities.

1. Machine learning models learn from experience, i.e. data.
   
2. Models learn to find patterns in the data.
   
3. Data can be labelled or unlabelled. Machine learning with labelled data is *supervised learning*, while machine learning with unlabelled data is *unsupervised learning*.
   
4. *Reinforcement learning* models learn to make sequence of decisions based on experience, rewards and punishments.


---

**Author**: <a href="https://github.com/andreusjh99" target="_blank">Chia Jing Heng (andreusjh99)</a>