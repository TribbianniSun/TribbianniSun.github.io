---
layout: post
title: t-test basics
date: 2024-07-20 12:14:32
description: This is an article that outlines basics about t-test.
tags: stats
categories: machine-learning
tabs: true
---

# What is a t-test?

T-test analyzes whether there is a significant difference between two groups of people.

- assumptions: metrics variable must be normally distributed.
- variances must be approximately equal.

# Three types of t-test

| Column 1               | one-sample                                      | Independent-sample                                                                 | Paired-sample                 |
| ---------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------- | ----------------------------- |
| Description            | **a single** sample over                        | **two** independent groups                                                         | **two dependent** groups      |
| Example                | chocolate bar                                   | pain relief among two groups of patients                                           | diet (mean with reference 0)  |
| Hypothesis             | null: sample mean = reference value             | null: null hypothesis of both groups are the same                                  | sample mean between pairs = 0 |
| Formula                | $$t =\frac{\bar{x} - \mu}{\frac{s}{\sqrt{n}}}$$ | $$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$$ | same with one-sample          |
| df (degree of freedom) | n - 1                                           | n1 + n2 - 2                                                                        | n = 1                         |

# Some heuristics

- t is greater if there is a greater difference between the mean
- t is greater if we have a less scatter data
- t is greater if we have more data

# How to check the hypothesis

## Read critical t-value

- Read the table of critical t-values
- Find the **df (degree of freedom)**
- Find the **level of significance**
- t > t_critical reject the hypothesis, the means are so different that we have to reject the hypothesis

## Calculate p-value

- what is a p-value?
  Assume there is no difference in the population
- significance level 5%
- one-tail / two-tail
