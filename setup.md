---
layout: page
title: Setup
permalink: /setup/
---

## Prerequisites

Before installing any of the course-specific packages below, please head over to <https://biosustain.github.io/2016-09-05-software-carpentry/> and
follow the installation instructions for Python.

## Installing cameo

Please open a shell (terminal) and create a conda environment for the course using the following command.

    conda create -y --name cell-factory-course python=3.4 scipy pandas numexpr bokeh jupyter sympy lxml matplotlib

If you're on Linux or OS X or are using the git-bash shell on Windows run

    source activate cell-factory-course

to activate the environment. If you're on Windows using the default terminal (cmd) run the following command instead.

    activate cell-factory-course

If you successfully activated you're environment, your command prompt will look similar to this.

    (cell-factory-course)$

Then use `pip` to install [cameo](http://cameo.bio).

    pip install cameo

Run the following command to check that the installation was successful.

    python -c "from cameo import models;print(models.bigg.e_coli_core.optimize().objective_value)"

The output should be `0.8739215069684304`.

You also have received an email with installation instructions for one commercial software package. Install it by copy and pasting the command into your shell.

    pip install <the-dropbox-link>

If this fails, please click on the dropbox link, download the wheel file, and then run the following in your shell (you need to be in the directory where you downloaded the file from dropbox).

OS X:

    pip install cplex-12.6.3.0-py3-none-any.whl


Windows:

    pip install cplex-12.6.1.0-py3-none-any.whl  #

## Download course materials

 You can download all course notebooks at once [here](https://github.com/biosustain/cell-factory-design-course/archive/master.zip).
