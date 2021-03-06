---
layout: post
title:  "머신러닝 프로젝트 진행에서 중요 사항"
date:   2018-07-31 12:00:00
author: Yeongrong Bak
categories: MachineLearning
tags: ML MachineLearning Project Process
---

머신러닝 프로젝트를 진행함에 있어서 가장 기본이자 중요한 파트가 전체적인 프로세스를 이해하는 것 이라고 생각합니다.

실제로 분석을 진행하다보면 지엽적인 문제 해결에 갇힐 때가 발생하는 등,

분석의 최종적인 목표가 무엇인지 흐려질 때가 발생합니다.

따라서 전체적인 흐름을 이해하고 단계를 확실히 나누어서 단계 별로 목표를 명확히 하고

이를 통해 최종적인 목표를 달성하는 것이 프로젝트에서 가장 중요한 사항입니다.

따라서 이번 포스팅에서는 머신러닝 프로젝트 진행의 각 단계에서 어떠한 것에 중점을 두어야 하는지에 대해 좀 더 명확히 정리하고자 합니다.

---

## 머신러닝 프로젝트의 주요 단계

1) 큰 그림을 본다.

2) 데이터를 구한다.

3) 데이터를 탐색하고 시각화한다.

4) 머신러닝 알고리즘을 위해 데이터를 준비한다.

5) 모델을 선택하고 훈련시킨다.

6) 모델을 상세하게 조정한다.

7) 솔루션을 제시한다

8) 시스템을 론칭하고 유지보수한다.

---

## **1. 큰 그림 보기**

- 비즈니스 목적이 정확히 무엇인지 파악한다

- 현재의 솔루션에 대해 파악한다

- 어떤 작업을 수행할 것인지 결정한다

- 결정된 작업에 맞는 성능 지표를 선택한다

- 생성한 가정에 대해 나열하고 검사한다

---

## **2. 데이터 구하기**

- 실제 현업에서의 프로젝트 진행이라면 적재 되어있는 데이터셋을 불러오는 과정

- 머신러닝 공부를 위해서 주로 활용되는 데이터 셋은 아래의 사이트에서 구할 수 있다.

1) 유명한 공개 데이터 저장소

>UC 얼바인 머신러닝 저장소(http://archive.ics.uci.edu/ml/)

>캐글(Kaggle) 데이터셋(http://www.kaggle.com/datasets)

>아마존 AWS 데이터셋(http://aws.amazon.com/ko/datasets)

2) 메타 포털

>http://dataportals.org/

>http://opendatamonitor.eu/

>http://quandl.com

3) 그 외 데이터 저장소

>위키백과 머신러닝 데이터셋 목록(http://goo.gl/SJHN2k)

>Quora.com 질문(http://goo.gl/zDR78y)

>데이터셋 서브레딧 (http://www.reddit.com/r/datasets)

---

## **3. 데이터를 탐색 및 시각화**

- 데이터 탐색에서 기본적으로 사용되는 Pandas 함수

`df.head()` : 데이터 테이블의 처음 다섯개 행 출력

`df.info()` : 데이터에 대한 간략한 설명 출력

`df["variable"].value_count()` 특정 범주형 변수에 대한 관측 값 빈도 출력

`df.describe()` : 숫자형 변수의 요약 통계량 출력

- Matplotlib 을 활용한 데이터 시각화

`df.hist(bins=50, figsize=(20, 15))` :히스토 그램 출력

`df.plot(kind="지정", x, y)` : 특정 형태(Scatter, bar, box 등)를 지정해서 그래프 출력

- 상관 관계 파악

`corr.matrix = df.corr()` : 전체 변수에 대한 상관 계수를 매트릭스 형태로 계산

`corr.matrix["variable"].sort_values(ascending=False)` : 특정 변수 기준 상관 계수 출력

- 변수에 대한 조합을 바탕으로 파생변수를 생성하는 것이 중요함

- NA 처리 등 데이터 정제 작업 필요

- 범주형 변수에 대한 원-핫 인코딩 : 범주 값이 가까운 카테고리를 비슷하게 인식하는 경우가 존재하기 때문에 수행

- 특성 스케일링 (min-max 스케일링, 표준화) 작업

---

## **4. 모델 선택과 훈련**

- 훈련 세트를 특정 알고리즘을 바탕으로 훈련 시키고 모형의 성능을 파악한다(회귀 모형의 경우 RMSE)

- 훈련 세트에 사용되지 않은 데이터를 바탕으로 모형의 성능을 검증한다.

- 훈련 모형의 성능과 검증 모형의 성능을 비교해 모형이 과대적합 되지 않았는지 확인한다.

- **K-겹 교차 검증** : 훈련 세트를 폴드(fold)라 불리는 K개의 서브셋으로 무작위 분할 → 모델을 K번 훈련하고 평가 (매번 다른 폴드를 사용)

---

## **5. 모델 세부 튜닝**

- **그리드 탐색** : 가능한 모든 하이퍼 파라미터 조합에 대해 교차 검증을 사용해 평가

- **랜덤 탐색** :각 반복마다 하이퍼파라미터에 임의의 수를 대입하여 지정한 횟수만큼 평가한다(하이퍼 파라미터 탐색 공간이 커지면 랜덤 탐색이 더 효율적)

- **앙상블 방법** : 단일 모델 여러개를 결합해 모형의 성능을 더욱 향상 시키는 방법

---

이상으로 머신러닝 프로젝트를 진행함에 있어서 전체적인 진행 과정에 대한 설명과 각 과정에서 어떠한 작업을 수행해야 하는지를 살펴 봤습니다.

다음 포스팅에서부터는 이번 포스팅에서 자세한 설명이 생략된 개념들에 대해서 더 깊게 포스팅 하도록 하겠습니다. :)

---

- 참고 자료 : Hands-On Machine Learning with Scikit-Learn & TensorFlow (한빛미디어)

