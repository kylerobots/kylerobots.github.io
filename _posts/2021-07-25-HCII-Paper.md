---
title: HCII Paper and Presentation
classes: wide
toc: false
tag: Publication
tag: Neural Networks
---
Released today, I have a new published paper and presentation! Together with two of my work colleagues, I published a
paper at Human Computer Interaction International 2021 (HCII). The paper and associated talk presents a tool we created
for generating labeled synthetic data for neural network training. The novelty of the tool is that it is written
entirely within the ROS architecture. The paper, source code, and presentation can all be found below.

The purpose of the tool is to assist the user in creating perfectly labeled synthetic data using ROS and Gazebo. While
there are other such tools, none leverage the ROS ecosystem. My team and I wanted to create something that
would be extremely familiar to someone already using ROS, as opposed to something like
[Unity](https://unity.com/products/computer-vision) that would require additional learning. The tool can also write data
to multiple formats simultaneously. For example, it can write to
[COCO's JSON format](https://cocodataset.org/#format-data) and
[YOLO's text file format](https://pjreddie.com/darknet/yolo/). It can also easily be extended to include additional
formats as required. This is useful when you are exploring different networks that may require data in different
formats.

The tool should provide an easy user experience to anyone looking to generate labeled data automatically via ROS. The
code is freely available at GitHub and I encourage anyone to check it out if you think you will have a use for it. And
since it is open source, feel free to make any changes, note any bugs, or suggest improvements. I would love to hear
from you!

[The paper](/assets/papers/Automatic_Generation_of_Machine_Learning_Synthetic_Data_Using_ROS.pdf)

[The source code](https://github.com/Navy-RISE-Lab/nn_data_collection)

[The presentation](https://drive.google.com/file/d/1G-mnzDOK0mjHeCWuimCk-Ent7LIG4dSD/view?usp=sharing)

{% include video id="1G-mnzDOK0mjHeCWuimCk-Ent7LIG4dSD" provider="google-drive" %}
