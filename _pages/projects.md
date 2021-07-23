---
title: "Projects"
layout: splash
permalink: projects
header:
    overlay_color: "#000"
    overlay_filter: "0.5"
    overlay_image: /assets/images/PortfolioCropped.jpg
excerpt: My personal programming projects
intro:
    - excerpt: All photos courtesy of [**Unsplash**](https://unsplash.com)
algorithm:
    - image_path: assets/images/Algorithm.jpg
      overlay_color: "#000"
      overlay_filter: "0.5"
      alt: "A computer with code displayed on it."
      title: "Algorithms"
      excerpt: "Some practice code from my Algorithms course."
      url: https://kylerobots.github.io/algorithms/
ground_texture:
    - image_path: assets/images/WoodFloor.jpg
      alt: "A picture of wood floors."
      title: "Ground Texture Sim"
      excerpt: "A tool to simulate realistic ground textures for use in downward facing monocular SLAM applications. 
      This is to help generate data for my PhD research."
      url: https://kylerobots.github.io/ground-texture-sim/
k_armed_bandit:
    - image_path: assets/images/SlotMachine.jpg
      alt: "k-Armed Bandit"
      title: "K-Armed Bandit"
      excerpt: "A modular collection of K-Armed Bandits and associated reinforcement learning agents to solve them."
      url: https://kylerobots.github.io/k-armed-bandit/
mnist_viewer:
    - image_path: assets/images/MnistExamples.png
      alt: "A set of handwritten digits"
      title: "MNIST GUI Viewer"
      excerpt: "A *very* basic, underdeveloped project using Qt's GUI framework combined with PyTorch for C++."
      url: https://kylerobots.github.io/mnist-viewer/
turtlesim_teleop:
    - image_path: assets/images/Turtle.jpg
      alt: "A turtle swimming in the water."
      title: turtlesim_teleop
      excerpt: "A ROS2 package to control the turtlesim demonstration via keyboard. This is mainly to practice working
      with ROS2 and has only basic capability at the moment due to other priorities."
      url: https://kylerobots.github.io/turtlesim_teleop/
---
{% include feature_row id="intro" type="center" %}
{% include feature_row id="ground_texture" type="right" %}
{% include feature_row id="k_armed_bandit" type="left" %}
{% include feature_row id="algorithm" type="right" %}
{% include feature_row id="turtlesim_teleop" type="left" %}
{% include feature_row id="mnist_viewer" type="right" %}