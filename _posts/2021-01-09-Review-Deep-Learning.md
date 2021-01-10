---
title: Review&#58; Udacity's Intro to Deep Learning with PyTorch
classes: wide
tag: Review
tag: Neural Networks
---
# Introduction #

Recently, I wanted to learn more about [PyTorch](https://pytorch.org/) for building neural networks. I had dabbled briefly,
but not enough to have any level of competency. My existing experience is with [TensorFlow](https://www.tensorflow.org/)
and [Darknet](https://pjreddie.com/darknet/). I have heard from a number of sources that PyTorch is really impressive. Additionally,
I found that they are one of the few popular networks that offers an easy to use C++ API (I use C++ for a number of personal
projects). Given that, it seemed worth exploring what working with PyTorch is like.

PyTorch offers a number of tutorials [on their site](https://pytorch.org/tutorials/). However, I vaguely remember these
tutorials not quite fitting what I was looking for last time I checked. To be fair, I was only dabbling and looked very briefly.
They are probably very helpful and worth checking out, so don't necessarily take my word on those.

In addition to PyTorch's tutorials, I recently also found Udacity offered a course called
[Intro to Deep Learning with PyTorch](https://www.udacity.com/course/deep-learning-pytorch--ud188). Based on the syllabus, this
seemed like a promising course to cover what I wanted. It starts with an introduction to neural networks and works up through
deep networks, convolutional neural networks (CNNs), recurrent neural networks (RNNs), and long short term memory (LSTM) networks.
Each features implementation examples using PyTorch, so offers a great way to get up to speed on using the framework. Additionally,
Udacity courses tend to have lots of exercises and quizzes throughout to make sure you understand the content. Lastly, this
particular course happened to be free (at least as of the time of writing). Therefore, it seemed like a worthwhile course
to explore.

After completing the course, I wrote up this post to share my experience. I quickly summarize the course content. I also
include my thoughts about the course, including what it did well and not so well. Lastly, I include a brief summary of the overall
usefulness of the course.

# Course Content #

The course contains nine sections, including a "Welcome to the course" section. Udacity estimated each section to take anywhere
between 30 minutes to 5 hours. However, the 5 hour estimates also include time to complete all the coding exercises. Most sections
consist of a bunch of videos interspersed with coding and quizzes.

## Introduction to Neural Networks ##

This section presents an overview of neural network concepts. This includes logistic regression, sigmoid and softmax functions,
loss functions, backpropagation, and more. It does not cover any specific network yet, but lays the concepts and mathematics that
make up the foundation of neural networks.

## Talking PyTorch with Soumith Chintala ##

This is an interview with the creator of PyTorch. It offers a history of the framework, some of its driving philosophy, and a bit
about the future of PyTorch. It isn't necessary to understand how to use it, but offers some nice context.

## Introduction PyTorch ##

This section starts to dive into using PyTorch. It has you create a deep multi-layer perceptron network for classifying images from
the [FashionMNIST dataset](https://github.com/zalandoresearch/fashion-mnist). As part of this, it teaches you how to prepare data,
define the model, train the model to learn the weights, and evaluate end accuracy. There is also a quick lesson on transfer learning.

## Convolutional Neural Networks ##

From there, the course then walks you through the theory and application of CNNs. It first defines how convolutional layers work. It
then guides you in building a CNN to classify the same FashionMNIST dataset from before. By doing this, you can compare the accuracy
of both networks.

## Style Transfer ##

This section is a quick aside into using CNNs for style transfer. Style transfer modifies one image to match the style of another.
In performing this task, you learn how to manipulate a PyTorch model at a more detailed level than before. You are required to access
intermediate output of several layers throughout the network, as well as freeze the weights so that backpropagation modifies the
input image instead of the network.

## Recurrent Neural Networks ##

Next, the course teaches you the theory behind RNNs and LSTMs. You demonstrate this knowledge by building a LSTM network to perform
text prediction. Given an arbitrary series of characters input into the network, it tries to predict what the best next character
should be.

## Sentiment Prediction RNNs ##

The penultimate section serves as a capstone project of sorts. It walks you through an end-to-end example on building an RNN for
sentiment classification of movie reviews. This includes a number of steps to pre-process the data, such as converting words to
numbers and padding to a specified input length. After processing, you then build a network and train on your processed data.
You then evaluate the results on a test set of data. While there is significant work involved, the instructor reviews solutions
after each portion of the code.

## Deploying PyTorch Models ##

The final section is very short. It covers how to build a network in Python and export it for use in a C++ environment. This is
useful for situations where production requirements just aren't met by Python. This section walks through the tutorial available on
PyTorch's website called [Loading a TorchScript Model in C++](https://pytorch.org/tutorials/advanced/cpp_export.html).

# Overall Thoughts #
After working through all the sections, there were some aspects of the course that I liked and some that I did not care for.
Overall, I definitely enjoyed the course, although I felt it is better suited for those newer to neural networks.

## Pros ##

1. As with any Udacity course, there is a plethora of quizzes and coding examples throughout the lessons. This gave me a great
opportunity to practice the material right after learning the concept.
2. Likewise, the exercises are really well put together. They follow the familiar format of template code that requires you to
finish some sections. However, unlike other courses I have seen, the surrounding code is well explained. In fact, I was able to
easily modify and reimplement it on my own to conduct some side exploration into automatic hyperparameter tuning.
3. The initial section on neural networks was really well done. They related the concepts very well and used a number of great
analogies to drive home the ideas. Additionally, there is just the right amount of math. If someone wasn't interested in the math,
they could safely gloss over it without being too lost (at least until implementing some functions). However, for someone like me who
needs to work through all the equations to feel like they have a solid grasp, there is enough to run with and understand.
4. The course has great production value. All the narrations are clear and the graphics were related and understandable. Many
sections offered links to related reading that covers the certain topics in more detail. Also, the code is fairly well documented!

## Cons ##

1. I think this course was pulled together from a number of Udacity's other course. At times, they make references to Keras in the
videos. Additionally, they repeat certain concepts in different sections, and not in the "remember from last time" sort of way. It
is a free course offered on a site that usually requires payment for their courses though, so still well worth the value.
2. Not all of the exercises can be done online in their classroom workspace. They mention the ability to use the workspace at the
beginning, but most of the later material requires cloning their Git repository. This isn't a huge issue, but I don't have a good
GPU on my computer, so I had to significantly limit training on the networks and thus didn't get nearly the accuracy as the
instructors.
3. The C++ section at the end essentially just reads the online tutorial it references, so there isn't really any value added. As
this wasn't the primary focus of the course, I can give them a pass on this.

## Takeaway ##

Overall, I liked this course. I would consider it a practical, introductory guide to neural networks in general and PyTorch
specifically. It provides a good introduction to the fundamentals of both. If you are just looking for a primer on using PyTorch and
are already well-versed in neural networks, this course will be overkill for you. However, if you are just getting started and 
want to dive in, this is an excellent resource to use.