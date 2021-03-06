---
title: (머신러닝) (ex) linear regression2
date: 2018-08-09T14:00:58+09:00
author: nobbaggu
layout: post
categories: 머신러닝
image: /images/2018/08/machine-learning.jpg
tags:
  - AI
  - cost function
  - gradient descent
  - hypothesis function
  - linear regression
  - machine learning
  - 가설함수
  - 경사하강법
  - 기계학습
  - 머신러닝
  - 비용함수
  - 선형회귀
  - 인공지능
---
feature 1 : 인구

feature 2 : 수입이 $5000 밑인 비율

feature 3 : 실업 비율

output : 100만명 당 연간 살인자 수

![image](https://nobbaggu.github.io/images/2018/08/1-2.png){: width="50%" height="50%"}

일단 feature별로 절대적 수치의 scale의 차이가 커서 feature normalization을 해야한다. 그렇지 않으면 gradient descent의 속도가 너무 느릴 것이다.

![image](https://nobbaggu.github.io/images/2018/08/1-3.png){: width="50%" height="50%"}

평균을 구하는 mean함수와 표준편차를 구하는 std함수는 각 column별로 연산해준다. 이렇게 normalize를 하고 나니 각 feature matrix의 각 column의 평균이 거의 0에 가깝고 표준편차는 1이 되었다. 이제 마지막으로 모든 element가 1인 column을 추가해주어 x\_0라는 theta\_0에 해당하는 feature를 만들어야한다. 이는 우리가 고등학교때 보았던 정규분포이다. 이제 마지막으로 모든 element가 1인 column을 추가해주어 x\_0라는 theta\_0에 해당하는 feature를 만들어야한다.

![image](https://nobbaggu.github.io/images/2018/08/1-4.png){: width="50%" height="50%"}

이제 gradient descent를 해도 된다. 이전 글에서 implementation 할 때 썼던 cost 하수와 graD 함수를 그대로 쓰겠다. 두 함수의 내용은 다음과 같다.

![image](https://nobbaggu.github.io/images/2018/08/1-5.png){: width="50%" height="50%"}

graD 함수는 theta와 J를 반환시켜주는 함수이다. gradient descent는 200번의 iteration을 거치고 마지막에는 iteration의 횟수에 따른 cost function J의 변화를 그래프로 보여주도록 했다.

![image](https://nobbaggu.github.io/images/2018/08/1-6.png){: width="50%" height="50%"}

cost는 3370으로 수렴하였다. 이제 위에 계산된 theta를 최종 parameter로 정하겠다. 이제 model이 만들어졌다. 위의 model로 인구가 100만명, 수입이 $5000밑인 비율이 30%, 실업 비율이 10%인 도시의 100만명 당 연간 살인사건의 수를 예측해보겠다.

![image](https://nobbaggu.github.io/images/2018/08/1-4.jpg){: width="50%" height="50%"}

연간 46명의 살인사건이 일어날 것으로 예상된다.

애석한 것은 위의 데이터들을 그림으로 나타낼 수 없다는 것이다. 우리가 그림으로 그릴 수 있는 것은 3차원 공간까지인데, feature2개와 output 1개 까지이다. feature가 3개 이상인 경우에는 feature와 output의 상간관계를 그림으로 파악하는것이 되지 않는다.

아무튼 개인적으로 linear regression으로 풀 수 있는 머신러닝 문제를 implementation 해보면서 이론으로 배웠던 내용들에대한 이해가 한층 더 높아진 것 같은 기분이 든다.

정리를 한 번 해보겠다.

<span style="color: #ff0000;"><strong>(0. training dataset을 통해 feature matrix X, output y 만들기. 필요하다면 feature normalization 실행)</strong></span>

<span style="color: #ff0000;"><strong>1. feature 갯수에 따른 hypothesis function 생성 = theta의 갯수 정하기</strong></span>

<span style="color: #ff0000;"><strong>2. gradient descent를 통해서 cost function J가 수렴할 때 까지 theta를 update해서 최종 theta 정하기( = model 정하기)</strong></span>

<span style="color: #ff0000;"><strong>3. model로 특정한 case의 결과 예측 해보기</strong></span>