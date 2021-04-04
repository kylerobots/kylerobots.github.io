---
title: Learning ROS2
classes: wide
toc: false
tag: Personal
tag: PhD
---
It has been a bit since I last posted anything. Turns out, this semester is busier than I first expected. While I am
only taking a single class, I will also be taking the qualifiers in May. This involves a research component and a
knowledge component, so I have been brushing up on my lessons from prior classes to prepare. To stay up to date with it
all, my non-working time is pretty stricly regimented. *Monday:* review practice problems, *Tuesday:* lecture,
*Wednesday:* ... you get the picture. The studying is going well, but it takes a lot of time. What little downtime I
have left is spent with the family or just recharging. Consequently, I have had little time left to dive in to any new
projects or interesting programming tools. Hence, the lack of new content.

That being said, I still have managed to start a new project! I am getting up to speed on
[ROS2](https://docs.ros.org/en/foxy/index.html). I use ROS1 extensively at work and have been aware of ROS2 for some
time. I just haven't had any opportunities to learn and use it. I have a few personal project concepts in mind that
would benefit tremendously from ROS2 as well, so I have a personal motivation to learn it (as opposed to just free
labor for my employer).

This project involves creating a package to control the
[turtlesim example](https://docs.ros.org/en/foxy/Tutorials/Turtlesim/Introducing-Turtlesim.html) via keyboard. This is
definitely not an original idea. In fact, there is a package in the turtlesim examples that offers this exact
functionality. However, turtlesim control offers an opportunity to learn all the fundamentals. In particular, I am
planning to allow the following functionality:

* Drive the turtle via keyboard control (topics).
* Change the pen colors via key presets (services).
* Instruct the turtle to rotate to absolute orientations (actions).
* Change key mappings prior to running (parameters).
* Include Docker files to allow development anywhere.
* Include rigorous documentation.
* Use a CI pipeline.
* Explore some basic static code analysis tools.

I have only just started the project and only completed the first goal so far. The documentation is at
[https://kylerobots.github.io/turtlesim_teleop/](https://kylerobots.github.io/turtlesim_teleop/) and the source code is
at [https://github.com/kylerobots/turtlesim_teleop](https://github.com/kylerobots/turtlesim_teleop). I will chip away at
it when I have time. Once the qualifiers are done, progress should speed up.

Additionally, this project actually started because of a bigger project idea I had. The two knowledge areas under test
for the qualifiers are dynamics and controls. I thought it would be interesting to recreate the
[cart-pole/inverted pendulum](https://en.wikipedia.org/wiki/Inverted_pendulum) control problem in
[Gazebo/Ignition](https://ignitionrobotics.org/about) to help pull all this information together. This could also be an
opportunity to explore some of my reinforcement learning knowledge as an alternate controller. However, that would be a
lot to tackle in a single project. I figured it would be easier to learn the ROS2 fundamentals first with this keyboard
control project, then progress to the cart-pole controller. There is no way I will finish before the qualifiers, but it
is still an interesting project to tackle that encorporates a number of areas of interest.

Until then, though, I think I have another practice problem that I need to get to...