---
layout: post
title:  "What is Machine Learning?"
date:   2021-09-10
read: 8
description: What machine learning actually is, and the main types of machine learning algorithms.
categories: machine learning
---

---

# Machine Learning

Machine learning is a buzzword that you probably have heard a lot recently, but what exactly is it?

**Machine learning** is an application of **artificial intelligence (AI)** that provides systems the ability to automatically learn and improve from experience without being explicitly programmed. In other words, 
> Machine learning algorithms enable machines (or, more accurately, **models**) to **learn from experience** as humans do.

## Machine Learning (ML) vs Artificial Intelligence (AI)

Before we move on, are ML and AI the same thing? 
>**Machine learning (ML) is a subset of artificial intelligence (AI)**.

**Artificial intelligence (AI)** is the broad science of mimicking human abilities. It comprises a multitude of fields, including but not limited to robotics, speech processing, computer vision, and machine learning. These fields cover a wide array of applications that involve mimicking human abilities to solve or improve everyday problems.

**Machine learning** is a specific subset of AI which mimics the human ability to learn. 

## So how do models learn with Machine Learning?

As mentioned, the key element of machine learning is that models learn from experience, as humans do.

### Humans learn from experience. 

- After falling multiple times, babies learn what to do and what not to do, and eventually learn how to walk. 
- Ask someone who knows nothing about chess to watch two players playing chess. After a few rounds, they will be able to deduct that rooks move only in straight lines, bishops only in diagonals, and so on. 

From experience, humans learn to **group, classify and identify patterns**. With more experience and learning instances, the patterns identified become increasingly accurate.

### Machine Learning

Machine learning is essentially the same concept. Using the human analogy, **models** are the humans, and **data** is the learning instances.

Data collected from various sources (sensors, user-generated, etc) is fed into a model. The model then looks for patterns in the data. By identifying patterns, the model is able to make better decisions. 

## Types of Machine Learning

There are three main types of machine learning: 
1. Supervised learning
2. Unsupervised learning
3. Reinforcement learning 

### Supervised Learning

Data can be labelled or unlabelled. For example, given an image of a cat, the image can be given a label "cat" or not. \
>A supervised learning model uses labelled data for its learning. 

In supervised learning, the model takes in data samples and learns the correlation between the data samples and their corresponding labels. The model is "supervised" by the labels attached to the samples, hence the name supervised learning. When given a new piece of data, the model will use what it learns to predict the label for this new data. 

A common problem in supervised learning is **classification**. Classfication is the act of classifiying data, i.e. assigning labels to data. Classification is widely used. The most common applications include (but is not limited to):

1.  Face detection
    
    Detecting a face in an image. This could be detecting the presence of a face in the image or determining the exact location (in terms of pixels) of the face in the image.

    For detecting the presence of a face in an image, the data will be images with or without faces, and the label to each image will be `True` if the image contains a face and `False` if the image does not contains a face.
    
2.  Object detection and classification
    
    This is similar to face detection but for objects. Typically these problems involve detecting and classifying multiple types of objects in an image.

    For example, for a self-driving car to safely manoeuvre a busy road, it is important to know the different objects present on the road. From an image of the road taken with sensors or cameras on the car, the model needs to be able to detect stop signs, pedestrians, trees, pavement, etc. in the image and correctly classifies them.
    
3.  Speech recognition
    
    A common problem which forms the basis of auto captioning services and voice assistants. Speech recognition is the task of transcribing speech to text. The data is speech audio and the label to each speech audio is text corresponding to what's said in the audio.

### Unsupervised Learning

While supervised learning uses labelled data, 
>Unsupervised learning uses unlabelled data.

Due to the lack of labels, unsupervised learning problems are less about predicting labels for data, but more about grouping data.

A common problem in unsupervised learning is **clustering**. Clustering is the problem of grouping data into clusters. Given a set of data samples, a model will be tasked to group the data into several clusters. What the model will strive to learn is the criteria to group these clusters. When given a new piece of data, the model will use the criteria it learns to assign the new data to one of the clusters.

For example, given images of dogs, cats, birds and humans, the model will learn to group these images. Depending on the number of clusters specified for the model, the model might learn to group the images into:
1. dogs, cats, birds and humans (`cluster = 4`)
2. mammals and birds (`cluster = 2`)
3. walk on 4 limbs and walk on 2 limbs (`cluster = 2`)

etc.

Since there are no labels, we humans will have no idea what clusters the model will form beforehand. After the model learns, we then study the clusters and figure out the reasoning behind the clustering (For eg., is it animal groups or number of limbs?).

Therefore, while in classification the model will effectively "cluster" the data into groups based on labels attached to the data (by us humans), in clustering the model has to learn that on its own. This means that it is possible for the model to learn criteria for clustering that we humans had never thought of before!

### Reinforcement Learning

Finally, reinforcement learning. 
>**Reinforcement learning** is an area of machine learning concerned with learning to make a sequence of decisions. 

In reinforcement learning, the model learns not only from experience but also from rewards and punishments. This is analogous to how a baby learns to walk. 

A baby might move their limbs in one way but they fall. This is a punishment. The baby will then alter the way they move their limbs and try again. This time they are to stand straight. This is a reward. The baby will remember that and tend to replicate that action. Through trials and errors, the baby finally learns to walk.

A reinforcement learning model does the same thing. The model might be tasked to learn to play chess. The model does not know what moves are optimal initially. By trying different moves and playing many games, the model is able to learn an optimal strategy based on the rewards (when it wins) and punishments (when it loses) it receives. In other words, the optimality of a strategy the model tries is reinforced by the rewards and punishments it receives. The model then improves the strategy accordingly until it thinks it is the most optimal.

The problems reinforcement learning tackle involve sequences of complex decisions. Examples include but are not limited to robots learning to walk, models learning to play a game, etc.

## Conclusion

Machine learning is a rapidly growing area of interest due to its wide array of applications.

- Machine learning models learn from experience, i.e. data.
- Models learn to find patterns in the data.
- Data can be labelled or unlabelled. Machine learning with labelled data is *supervised learning*, while machine learning with unlabelled data is *unsupervised learning*.
- *Reinforcement learning* models learn to make sequence of decisions based on experience, rewards and punishments.


---

**Author**: Chia Jing Heng (andreusjh99)