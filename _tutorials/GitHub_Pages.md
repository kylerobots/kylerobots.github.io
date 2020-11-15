---
title: Setting up a GitHub Pages Space with Minimal Mistakes
---
# Introducton #
This guide covers how i set up these pages using minimal mistakes (XXX - put link). It will start from scratch
and slowly build up everything. It also cvers how to do this with a docker environment and VS Code, although
the VS code part isn't necessary. techincally the docker part isn't necessary eiterh, but it helps if you
dont want to configure ruby and jekyll on your computer.

I will skip the backgorund on what all these tools are, but for more information on jekyll see (XXX - put link)
This also assumes taht you have VS code and docker installed already and are confortable using them. For VS Code, you
will need the (XXX - remote plugins??)

Minimal Mistakes is a layout created already that is easy to use, powerful, and looks really sharp. I selected it
because i liked the collections layout and the ability to put tables of content and side panels on pages. There are
plenty of other themes available here (XXX - put link).

# Docker Setup #
First, it is helpful to create a Docker container that can be used to run the Jekyll stuff (XXX). This will help with
viewing your layout locally before you push it. If you are using VS Code, you need a Dockerfile and a devcontainer.json.
Frotunately, VS Code can autogenerate these for you. If Docker is started already, just go to (XXX - put all the commands here).

It will created the needed files and start everything within a container. You will know becuase you will see the infomration
at the bottom left of the screen like so:

(XXX - screenshot)

You will also notice that the two files have been created. They should look something like this:

(XXX - put the files here)

I am not super familiar with Docker settings, so won't elaborate on them.

# Empty Site #
Next, we will create the bare minimum needed to start up a webpage. First, create a new file called Gemfile. In it, put the
following:

(XXX - contents)

Afer, run (XXX - command). This will install everything within the container (XXX - is this needed the first time?) You will
see a "Gemfile.lock" file appear.

Once that is done, you will need to create a _config.yml file. This is used to specify site wide configuration settings and
details that Jekyll needs to build the site. It is one of the only documents that can't be changed on the fly while serving
the page. You have to restart for updates to take effect (see later XXX).

At a minimum, put the following:

(XXX - _config, with line numbers?)

