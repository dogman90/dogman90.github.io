---
title: (머신러닝) Ensemble - Boosting
date: 2018-10-28T20:06:00+09:00
author: nobbaggu
layout: post
categories: 머신러닝
image: /images/2018/08/machine-learning.jpg
tags:
  - adaboost
  - boosting
  - Ensemble
  - 머신러닝
  - 부스팅
  - 아다부스트
  - 앙상블
---
앙상블 방법 중 Bagging에 대해 학습하였다. 또다른 방법으로 Boosting이 있다. 유명한 Ada Boost가 바로 Boosting Ensemble 중 하나이다.

&nbsp;

# 1. Boosting

* * *

** Bagging은 여러개의 모델을 <span style="text-decoration: underline;">같은 알고리즘</span>으로 <span style="text-decoration: underline;">서로 다른 dataset</span>을 이용해서 학습시켜 합치는 것**이라 했는데, boosting은 여기에 하나의 개념이 추가된다. n&#8217;개의 데이터를 추출해 모델을 학습시켰을 때, 상대적으로 큰 error를 내는 데이터일 수록 다음 모델에서 추출될 가능성이 높아진다는 것이다. 상대적으로 poor한 학습효과를 내는 데이터에 가중치를 부여해서 다음 모델에서 추출될 가능성을 높이는 것이다.

&nbsp;

![image](https://nobbaggu.github.io/images/2018/10/no-name-7.jpg){: width="50%" height="50%"}

물론 Bagging과 마찬가지로 각각의 model은 **중복되는 데이터를 가질 수 있다.**

최종적으로 만들어진 여러개의 model이 예측한 결과를 평균을 내어 최종 예측 결과가 나온다.