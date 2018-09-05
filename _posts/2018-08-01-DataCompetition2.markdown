---
layout: post
title:  "2017 BigContest) 1. 데이터 정의 및 전처리"
date:   2018-08-01 12:00:00
author: Yeongrong Bak
categories: DataCompetition
tags: Competition Bigcon Bigdata
---

대회 과정에서 데이터를 통해 파악할 수 있었던 내용과 이를 바탕으로 진행한 전처리 과정에 대해서 기록해보고자 합니다.

## 1) 데이터 정의

- 신용평가사, 보험사, 통신사의 결합 데이터 (비식별화) 100,000건

- 지도 학습을 통해 TARGET 변수 (대출 연체여부 : 연체(1), 비연체(0))를 **정확히 맞추는 것이 주요 목표**

- 데이터 셋이 크고, 변수도 매우 다양해서 이를 팀원 끼리 나누어서 의미를 각자 파악하고, EDA를 진행한 뒤 각자의 결과를 바탕으로 팀원에게 설명해주는 방식으로 전체 데이터 셋을 이해했음

## 2) 데이터 전처리 및 EDA 과정

- 총 세개의 데이터 셋(신평사, 보험사, 통신사)으로 나누었을 때, 각 셋의 변수들 간의 높은 상관 관계가 존재
> 파생변수 생성 근거로 활용, 추후 상관 관계 고려

![cor_plot](https://user-images.githubusercontent.com/40160683/45091967-fa515600-b14e-11e8-8732-e82708829d51.PNG)


- 연속형 변수의 경우 0값이 높은 Sparse 데이터인 경우가 많았음 
> 로그 변환을 적용

![sparse_plot](https://user-images.githubusercontent.com/40160683/45092027-28cf3100-b14f-11e8-82ae-ac93a61e8b60.PNG)

- 소득을 직업 변수와 함께 그래프로 그려보았을 때, 직업 간 소득의 차이가 명확
> 표준화 작업 진행

![job_box](https://user-images.githubusercontent.com/40160683/45092035-2ff63f00-b14f-11e8-9ccc-361aed2d17bc.PNG)

- 그 밖에 각 독립변수의 분포 안에서 종속변수의 Proportion을 확인해 보면서 어떤 변수가 분류에 유의미하게 쓰일 지 판단

![prop_plot](https://user-images.githubusercontent.com/40160683/45092047-3684b680-b14f-11e8-9aaf-ee9586cda3c0.PNG)

- 파생 변수를 생성하는 과정에서 생성에 대한 명확한 로직이나 근거를 만드는 것에 집중했고 이 부분이 매우 중요하다는 것을 알 수 있었습니다.

---

이후 진행한 모델링과 결과에 대한 부분은 이후 포스팅 하도록 하겠습니다. :)
