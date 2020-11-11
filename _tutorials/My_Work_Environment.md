---
title: My Work Environment
toc: true
---
# Introduction #
I have a rather unusual development setup, including multiple devices. Additionally, I hate spending time configuring
the same things across each device as I inevitably miss something. Especially for things like keyboard shortcuts, it is
important to me to have consistency so that I don't have to remember which keys based on context. To that end, I have
made extensive use of Chocolatey (XXX - put link) and VS Code's new syncing functionality to keep my environment consistent.

I have four computers that I develop on. Two are Windows computers for personal use. I also have two at work. One is Windows and
one is Ubuntu. This guide targets the personal computers, as I have control over what I put on them. I do however sync some keyboard
shortcuts and other things to my other computers, but any in depth instructions are excluded here.

Most of my development is in C++, although I occasionally dabble in Python if one of my classes requires it. Most of my development
is for command line applications, but I occasionally feel the urge to make a nice GUI. Consequently, I use VS Code for most of
my development (XXX - put link) with Qt used for GUIs. While VS Code is certainly incredibly feature rich, it is not a full-fledged
IDE. So I also need some build tools to compile everything. And of course, there are the usual tools for version control,
containers, and documentation. The full list is as follows:

- Chocolatey (XXX - put link) (To manage all these applications)
- clang-format (For linting, part of VS Code)
- CMake
- Doxygen (For documentation generation) (XXX - put link)
- Git
- MinGW (64 bit specifically)
- MSVC build tools (A recent addition to )
- Python (XXX - whatever version)
- Qt Creator (XXX - put link)
- VS Code (XXX - put link)

# The Short Version #
To skip all the context for why these steps are done, just follow this list.
1. blah
2. 

# Setup Steps #
First, all of the tools need to be installed. Fortunately, this is easy using Chocolatey (XXX - put link). To install it, just follow the instructions
located here (XXX - put link). It can then be used to manage the installation of the rest of tools. To that end, I use a specific configuration file
in the right format for Chocolatey to read. It also includes some installation flags for specific configurations. It is set up as follows:
(XXX - put in code)
I keep this and several other configuration files saved in an online drive for easy access from any new computer. All I need to do is run:
(XXX - put command here)
This sometimes takes a little bit to run, but after it is done, I have almost everything installed. The only exception is Qt Creator. Installation
instructions are found in Qt Creator (XXX - link to other section).

From there, there are only a few additional configurations that are needed. Primarily, this involves putting several locations on the PATH environment
variable. Without this, VS Code, Qt Creator, and some of the other applications can't find some of the tools. Specifically, the following items should
be added. I list where they are installed by default when I run the command, but there may be some differences on each computer

(XXX - Make a chart with install locations)

Next, 

Then, pip install pipenv for python packages.

Lastly, one one of my computers, I had to add myself to the docker group. I work on my standard acocunt and only use the amdin for install. So i ran these commands: XXXX That allows the standard user to use Docker (full disclosure, depending on XXX, that might mean I have a vulnerability, but I'm not smart enough about how docker works to know.)

# Git Setup #
Ths is an easy one. Git stores all its configuration in a .gitconfig file. I keep one in the same spot as the chocolatey config. I also keep a .gitignore that contains the entries for all the items that I commonely use - C++, Python, Qt, ROS, etc. I just copy these in to the top elvel directoroy of each system.

# VS Code #
This is a bit more to set up, but once it is done, it is painless to migrate to a new system. One one of my sytems, I downloaded all the extensions i use. I then went through and established keyboard shortcuts and settings.

Then, I turened on the new syncing feature. This came out in version XXX. It uses your GitHub account, although I believe there are other sync options taht can be used. It automatically sunces all your extensions, settins, and shortucts.

There are also a few system specific things i ahd to confugre. For the CMake extensions, i had to point it to my copy of MinGW and CMake, as they weren't in the sual spot. CMake ??? in particular as in a weired spot because of chocolatey. I also had to confiugre the default kit, as it wouldn't use MinGW. Once they were on the PATH, run "scan for new kits" to detect them. MSVC is usually always found no problem.

On a new system, i just had to sign in to my account and start syncing. It would pull them all down and install everything. Specific to the Ubuntu system, I had to change a few settings. Before chaning each one, I made sure to disable syncing that setting, otherwise, it would overwrite on every system.

# CLang-format #
This was also pretty easy. VScode has a local copy of clang-format, so I don't need to install all of LLVM. I just need to define a clang format folder. To help with that, I use XXXXX. In particular, (maybe show my format file???)

# Qt Creator #
If everything else is done right, this part is actually pretty easy. When installing, make sure you download Qt versions that support the compilers you use. In my case, this is MSVC and MinGW 64bit. You can also uncheck the install of CMake, since it is already on your system. AFter install, it should recognize all the right build systems since they are on your PATH. it will already make the right kits.

From there, i went through and set up all the keyboard shortucts. I basically just viewed all the common ones from VSCode and made it the same for consistency. You can actuallly export the keyobard shortcuts, so i did that for future systems.

Lastly, i set up the code formatting. Qt needs to use an external clang-format, so i went to the setting in XXXx (add picture_) and pointed it to the clang-format that comes with VSCode at XXXX. It should be able to find the format file if it is at the top level.

Also, i set up my defaults to build within a subdirectory of the project and specified my default project directory.

# Conclusion #
That shoudl be everything! with luck, you will have the same enviornment across all your computers. It is still a little bit of setup, but it is better than doing each one by hand. And the less time you spend setting up, the more you spend developing!


I have a somewhat unusual development environment. Almost all of my development
is on C++, with a little bit on Python for class. Additionally, I only occasionally
develop GUIs. Most of the time, I am developing applications for the command line.
As such, I tend not to use an IDE for most development. When most of my work consists
of some C++ files and a CMakeLists to pull it all together, an IDE seems like
overkill.

However, I make extensive use of [Visual Studio Code](https://code.visualstudio.com/).
It is a phenominal editor that is practically an IDE at this point. There is also an
extensive marketplace for Microsoft and 3rd party developed plugins offering a wide
arrange of functionality. However, it doesn't come with any build tools. So I need
to configure all them manually.

Additionally, I also use VS Code at work on different devices there.
I have a Windows computer and an Ubuntu computer. I also have personal
computers at home I use for personal projects. I also sometimes use
Qt and QtCreator for GUI development.

The end result is
a lot of configuring needed to achieve uniformity across each
computer. To expediate this, I've started leveraging package
managers and syncronized settings