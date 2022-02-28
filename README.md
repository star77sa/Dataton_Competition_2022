# Dataton_Competition_2022

2022 데이터톤 경진대회 (2022.02.23 ~ 2022.02.25), 대상

---
![image](https://user-images.githubusercontent.com/73769046/156029098-0300bdc0-7508-46af-9b30-fe9548e83e6a.png)

## 1. Data Set

Train Data : 74,357건 / MBTI, 400개 단어 총 2컬럼 구성

Test Data : 9,337건 / 400개 단어 총 1컬럼 구성

데이터 셋 내 MBTI 분포는 균등하지 않음

## 2. Data preprocessing

처음 고려한 전처리 : 토큰화, 표제어 추출, 벡터화

- 토큰화 : Text를 여러개의 token으로 나누는 방법 (공백, 구두점, 특수문자 등으로 이름을 나눔)
- **표제어 추출** : 단수, 복수의 형태를 없애고 단어의 원형으로 돌려주는 과정
- **벡터화** : 컴퓨터가 문자를 이해할 수 있도록 수치화 해주는 과정

※ 주어진 데이터가 문장이 아닌 이미 단어로 나눠져 있기에 토큰화는 적용하지 않았다.

벡터화에서는 빈도수 기반 텍스트 벡터화인 TF-IDF를 적용

## 3. 예측 방식

1. MBTI의 4가지 특성을 각각 예측한 뒤 마지막에 합치는 방법

    Validation Set로 예측한 결과 정확도 70% (로지스틱 회귀를 기준으로 2번과 정확도 비교, 2번방식은 정확도가 80%라 2번방식을 채택)

      ***FeedBack : 이 방식은 4가지 특성을 예측할 때 각각의 특성이 서로 독립이 아니기에 낮게 나타났을 수 있음. 결과론적으로 2번 방식이 높게 나와서 썼다기 보다는 낮게 나온 이유를 생각해 볼 것***


2. **MBTI의 4가지 특성을 한번에 예측**

    사용모델 : 로지스틱 회귀(79.65%), 랜덤 포레스트(47.03%), 딥러닝(69.19%), LinearSVC(80.20%), LinearSVC + 배깅(77.21%)
    
    - LinearSVC의 정확도가 가장 높아 Linear SVC를 모델로 채택

    - LinearSVC 하이퍼파라미터 C값 조정 : C=0.475에서 정확도가 가장 높아 C=0.475로 하이퍼파라미터 채택
