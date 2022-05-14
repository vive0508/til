확률 분포 (probability distribution)
===

## 1. 확률 분포

- 확률 분포
```
확률 변수 X가 취할 수 있는 모든 값과 그 값을 나타날 확률을 표현한 함수
```

## 2. 이산형 확률 분포
- 이산형 균등 분포 ([discrete uniform disctribution](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%82%B0%EA%B7%A0%EB%93%B1%EB%B6%84%ED%8F%AC))
```
함수 가정의 된모든곳에서그 값이 일정한 분포
```
- 베르누이 분포 ([Bernoulli trial](https://ko.wikipedia.org/wiki/%EB%B2%A0%EB%A5%B4%EB%88%84%EC%9D%B4_%EB%B6%84%ED%8F%AC))
```
매 시행마다 오직 성공과 실패 두 가지의 가능한 결과만 일어나는 경우
```
- 이항분포([binomial distribution](https://ko.wikipedia.org/wiki/%EC%9D%B4%ED%95%AD_%EB%B6%84%ED%8F%AC))
```
연속적인 베르누이 시행을 거쳐 나타나는 확률분포
서로 독립인 베르누이 시행을 n번 반복하여 실행했을 때, 성공한 횟수 X의 확률 분포
```
- 포아송분포([poisson distribuiton](https://ko.wikipedia.org/wiki/%ED%91%B8%EC%95%84%EC%86%A1_%EB%B6%84%ED%8F%AC))
```
단위 시간 안에 어떤 사건이 몇 번 발생할 것인지 표현하는 이산 확률 분포
```

- 기하분포([geometric distribution](https://ko.wikipedia.org/wiki/%EA%B8%B0%ED%95%98_%EB%B6%84%ED%8F%AC))
```
베르누이 시행에서 처음 성공까지 시도한 횟수 X의 분포. 
베르누이 시행에서 처음 성공할 때까지 실패한 횟수 Y=X-1의 분포
```

- 음이항분포([negative binomial distribution](http://aispiration.com/r-algorithm/r-selling-candy-problem.html))
```
음이항 분포는 기하분포를 확장한 분포로 성공이 최초 목격되는 것은 확장하여 r 번째 성공할 확률을 모형화한 것이다.
```


## 3. 연속형 확률 분포
- 확률밀도함수 ([probability density function]())
```
 확률 변수의 분포를 나타내는 함수
 확률밀도 함수를 적분하면 누적분포함수가 됨
```
- 균일분포 ([continuous uniform distribution](https://ko.wikipedia.org/wiki/%EC%97%B0%EC%86%8D%EA%B7%A0%EB%93%B1%EB%B6%84%ED%8F%AC))
```
분포가 특정 범위 내에서 균등하게 나타나 있을 경우
```
- 정규분포 ([normal distribution](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%EB%B6%84%ED%8F%AC))
```
가우스 분포라고 불리며, 수집된 자료의 분포를 근사하는 데에 자주 사용된다.
특히, 평균이 0이고 표준편차가 1인 정규분포를 표준 정규 분포라고 한다
```

- 감마분포 ([gamma distribution](https://ko.wikipedia.org/wiki/%EA%B0%90%EB%A7%88_%EB%B6%84%ED%8F%AC))
```
감마 분포는 지수 분포나 푸아송 분포 등의 매개변수에 대한
켤레 사전 확률 분포이며, 베이즈 확률론에서 사전 확률 분포로 사용된다.
```
- 지수분포 ([exponential distribution](https://ko.wikipedia.org/wiki/%EC%A7%80%EC%88%98_%EB%B6%84%ED%8F%AC))
```
사건이 서로 독립적일 때, 일정 시간동안 발생하는 사건의 횟수가 푸아송 분포를 따른다면,
다음 사건이 일어날 때까지 대기 시간은 지수분포를 따른다. 이는 기하분포와 유사한 측면이 있다.
```
- 카이제곱분포 ([카이제곱분포](https://ko.wikipedia.org/wiki/%EC%B9%B4%EC%9D%B4%EC%A0%9C%EA%B3%B1_%EB%B6%84%ED%8F%AC))
```
서로 독립적인 표준정규 확률변수를 각각 제곱한 다음 합해서 얻어지는 분포
```
- 베타분포 ([beta distribution](https://ko.wikipedia.org/wiki/%EB%B2%A0%ED%83%80_%EB%B6%84%ED%8F%AC))
```
두 매개변수 alpha 와 beta에 따라 [0,1] 구간에서 정의되는 연속 확률 분포
```
