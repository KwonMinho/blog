---
title: "사이킷런"
date: 2019-12-22T20:41:28+09:00
categories: ["AI"]
tags: ["AI_Tool"]
cover: ""
---
# 1. Scikit-learn
## 1.1 개요
    1. 이 라이브러리는 파이썬에서 가장 유명한 머신러닝 라이브러리 중 하나
    2. Classfication, Regression Clustering 등 다양한 머신러닝 알고리즘을 적용할 수 있는 함수 제공

## 1.2 간단한 데이터 셋
    사이킷런 빌트인 데이터 셋
    캐글 데이터 셋
    UCI 머신러닝 저장소

사이킷런의 빌트인 데이터 셋 사용법
<code>
```
// 붓꽃 데이터 얻기
from sklearn.datasets import load_iris
iris = load_iris()
iris.data // 데이터 값
iris.target // 레이블 값(정답 값)
```
</code>

## 1.3 파워풀한 fit(), predict()
사이킷런은 핵심함수인 fit() 함수로 학습하고 predict()으로 예측하는 구조로 되어있다.

[**Exam**]
```
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
from sklearn.metrics import accuracy_score
from sklearn.model_selection import train_test_split

iris = load_iris()
dtc_tree = DecisionTreeClassifier()
X_train, X_test, y_train, y_test = train_test_split(iris.data, iris.target, test_size=0.3, random_state=121)

dt_tree.fit(X_train,y_train)
pred = dtc_tree.predict(X_test)
print("예측 정확도: ",accuracy_score(y_test, pred))
```




