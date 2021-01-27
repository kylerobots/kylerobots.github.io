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
k_armed_bandit:
    - image_path: assets/images/SlotMachine.jpg
      alt: "k-Armed Bandit"
      title: "K-Armed Bandit"
      excerpt: "A modular collection of K-Armed Bandits and associated reinforcement learning agents to solve them."
      url: https://kylerobots.github.io/k-armed-bandit/
algorithm:
    - image_path: assets/images/Algorithm.jpg
      overlay_color: "#000"
      overlay_filter: "0.5"
      alt: "A computer with code displayed on it."
      title: "Algorithms"
      excerpt: "Some practice code from my Algorithms course."
      url: https://kylerobots.github.io/algorithms/
mnist_viewer:
    - image_path: assets/images/MnistExamples.png
      alt: "A set of handwritten digits"
      title: "MNIST GUI Viewer"
      excerpt: "A *very* basic, underdeveloped project using Qt's GUI framework combined with PyTorch for C++."
      url: https://kylerobots.github.io/mnist-viewer/
---
{% include feature_row id="intro" type="center" %}
{% include feature_row id="k_armed_bandit" type="left" %}
{% include feature_row id="algorithm" type="right" %}
{% include feature_row id="mnist_viewer" type="left" %}