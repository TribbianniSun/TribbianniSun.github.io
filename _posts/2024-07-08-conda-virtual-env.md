---
layout: post
title: conda virtual environment
date: 2024-07-02 12:14:32
description: This is an article which shows how to create, manage, and freeze virtual environment using conda.
tags: python-developing
categories: developing, research
tabs: true
---

```bash
conda create -n venv new python=3.9 # craete the first virtual env
conda activate venv # actiave the env
pip list # check that we have a clear pip list
pip install requests # install request package
pip list # check that we installed the requests in the previous step
pip freeze > requirements.txt # freeze the current requirements into this txt for other environments
conda deactivate venv # deactivate the current virtual environment
conda create -n venv-child new python=3.9 # craete another new virtual env
conda activate venv-child # actiave the new env
pip list # check that we have a clear pip list
pip install -r requirements.txt # install the packages listed in requirements.txt
pip list # check that we successfull installed the required packages
```
