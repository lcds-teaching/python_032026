<p align="center">
  <img src="./assets/python_logo.png" width="200"/>&nbsp; &nbsp; &nbsp;<img src="./assets/python_logo.png" width="200"/>&nbsp; &nbsp; &nbsp;<img src="./assets/python_logo.png" width="200"/>
</p>

![coverage](https://img.shields.io/badge/Teaching-yellow)
[![Generic badge](https://img.shields.io/badge/Python-blue.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/GNU3.0-purple.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/Maintained-brightgreen.svg)](https://shields.io/)
[![Generic badge](https://img.shields.io/badge/BuildPassing-orange.svg)](https://shields.io/)
---
# Python for Health, Social, and Economic Data Science

### Introduction

Welcome to the 'Python for Health, Social, and Economic Data Science' class! This GitHub repository contains everything that we'll need for about ~15 hours of lectures. This course begins by assuming absolutely no knowledge of what Python is or can do, and hopefully ends with us being able to read `data' (in multiple different formats, from the web or otherwise), load it into dataframes, visualise, and model it. The background of the class will determine how quickly we go. Please star this repository on GitHub if you are taking the class!

### Prearrival

Be sure to consult the [course website](https://lcds-teaching.github.io/python_032026). Importantly, it contains a [setup.md](https://lcds-teaching.github.io/python_032026/setup.html) file.

There are two things in particular which we need:

* **Python**: A powerful, versatile language used for data analysis, visualization, and machine learning, with extensive libraries like pandas, NumPy, and scikit-learn

* **Git**: Git is a distributed version control system that tracks changes in code, enabling collaborative development and efficient project management.

If you are using a Chromebook, you might want to investigate [Google Colab](https://colab.research.google.com).

### Files

The main subdirectories which we will need are:

1. [Lectures](./Lectures), which holds the five main notebooks that we'll work through together each morning.
2. [Labs](./Labs), which contains information on the labs which we'll do each afternoon.
3. [Solutions](./Solutions), which will be updated and populated day by day after the labs.
4. [Homeworks](./Homeworks), which will be updated and populated day by day after the labs.
5. [Data](./Data), which is the place where we store data which we create and download.
6. [Figures](./Figures), which is where we still store our figures when we get to the matplotlib component of the class.

Homeworks are not optional, but should be *quite* easy if you've attended the lecture and completed the lab. My preferred system is to randomly select (via Python!) three people at the start of each following class to present their solutions to the group, with feedback. There are three questions each evening.

This is useful because *communicating* data science is every bit as important as doing it! You should consider writing your solutions in a Jupyter Notebook, the same tool that we are using to `live code' the lecture series. We will use ```homework_randomiser.py``` to achieve this: One of the goals of this course is actually to get us to a point where everybody understands what this is doing. I am never sharing the ```./assets/student_list.csv``` or ```./assets/selected_names.csv``` for confidentiality. **Note to self**: Do not forget to remove any randomly drawn students from the ```./assets/selected_names.csv``` file!

### Structure

* **Lecture One**: Basic object types and an introduction to collections (tentatively Day One)
* **Lecture Two**: Iterating over collections, Boolean logic, advanced loops, user input, and error handling (tentatively Day Two)
* **Lecture Three**: Pseudocode, functions, file I/O, programming outside Python, NumPy, and random numbers (tentatively Day Three)
* **Lecture Four**: Data from the internet, requests, pandas, and matplotlib (tentatively Day Four)
* **Lecture Five**: StatsModels, scikit-learn, and text modelling for health/social/economic analysis (tentatively Day Five, 13:00)

The lectures should take between two and a half and three hours. The first part of each of the second through fifth days will be a review of the homeworks (~15 minutes). One 'lecture' doesn't necessarily correspond *exactly* to one day: if we finish one lecture earlier on a specific day, we can move on to the next lecture. If we finish all five days of content early, we can spend the remaining time working on and discussing your own specific projects which you want to use Python for. At the end of each section of the notebooks, we will take a ~3-5 minute break from the lecture and you can play around in the notebooks following the set example question (which will then be live coded afterwards when the lectures resume). 
