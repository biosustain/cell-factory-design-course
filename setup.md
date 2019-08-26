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

    conda create -y --name cell-factory-course python=3.6

If you're on Linux or OS X or are using the git-bash shell on Windows run

    source activate cell-factory-course

to activate the environment. If you're on Windows using the default terminal (cmd) run the following command instead.

    activate cell-factory-course

If you successfully activated you're environment, your command prompt will look similar to this.

    (cell-factory-course)$

Then use `pip` to install [cameo](http://cameo.bio) and a few other handy things.

    pip install cameo pandas escher plotly matplotlib --upgrade

Run the following command to check that the installation was successful (this can take a few seconds).

    python -c "from cameo import models;print(models.bigg.e_coli_core.optimize().objective_value)"

The output should be approximately `0.8739`.

You also have received an email with with a download link for CPLEX (only intended for academic use). Download the respective installer for your platform and install CPLEX. After you succeeded follow the respective instructions for your platform.

### OS X and Linux

On Linux or OS X, run the following in your terminal (make sure you activated the `cell-factory-course` environment first) to install CPLEX for Python.

    pip install <path-to-your-cplex-installation>/CPLEX_Studio128/cplex/python/3.6/<platform>/

 For OS X, this should look like

 	pip install /Applications/CPLEX_Studio128/cplex/python/3.6/x86-64_osx/

### Windows

If you installed CPLEX on Windows, `cd` into the following directory first
    
    cd "C:\Program Files\IBM\ILOG\CPLEX_Studio128\cplex\python\3.6\<platform>"
    
and then run (make sure you activated the `cell-factory-course` environment first)

    pip install .

## Fallback solution

Please create a GitHub account if you don't already own one at <https://github.com/join?source=header-home>. That way we'll be able to provide you with access to a Jupyterhub notebook server that already contains all necessary software pre-installed as a fallback solution in case you run into troubles during the course.

## Download course materials

 You can download all course notebooks at once [here](https://github.com/biosustain/cell-factory-design-course/archive/master.zip).
