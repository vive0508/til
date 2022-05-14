모집단과 표본
===

## 1. 모집단과 표본

[레퍼런스](https://losskatsu.github.io/statistics/population-sample/#1-%EB%AA%A8%EC%A7%91%EB%8B%A8population%EA%B3%BC-%EB%AA%A8%EC%88%98population-parameter)

- 모집단 : 정보를 얻고자 하는 관심 대상의 전체집합을 말한다.   
- 모수 : 모집단 분포 특성을 규정 짓는 척도, 관심의 대상이 되는 모집단의 대표값.   
- 표본 : 모집단의 부분집합      
- 표본통계량 : 표본의 몇몇 특징을 수치화 한 값
- 표본분포 : 통계량들이 이루는 분포

### 1.1 표본 추출
- 표본추출: 모집단으로부터 표본을 추출하는 것
```
복원추출 : 추출한 데이터를 다시 넣고 추출하는 방법, 동일 표본 추출 가능
비복원 추출 : 추출한 데이터를 다시 넣지 않고 추출하는 방법
랜덤추출 : 각 개체가 모두 동일한 확률로 추출하는 방법
```
- 불균형 데이터(Imbalanced Data)의 문제
```
데이터가 불균형 데이터일 경우 문제가 생김

# 솔루션
1. 샘플링 기법을 통하여 해결하거나
2. 모델을 통한 성능 개선
```

### 1.2 sampling 기법
![image](https://user-images.githubusercontent.com/101171109/168420186-2cd99e90-5cb1-4c98-93e6-541e6f533a56.png)
- Over sampling : 타겟이 적은 class의 수를, 많은 class의 비율만큼 증가
- Under sampling : 타겟이 많은 class의 수를. 적은 class의 비율만큼 감소

### 1.3 중심극한 정리
- 중심극한정리([위키백과](https://ko.wikipedia.org/wiki/%EC%A4%91%EC%8B%AC_%EA%B7%B9%ED%95%9C_%EC%A0%95%EB%A6%AC))
```
동일한 확률분포를 가진 독립 확률 변수 n개의 평균의 분포는
n이 적당히 크다면 정규분포에 가까워진다는 정리이다.
```

## 2. 표본 분포
- 카이제곱 분포
- T분포
- F분포
