### K번째 약수

> 두 자연수 n과 k가 주어졌을 때,   
> n의 약수들 중 k번째로 작은 수

```python
n,k = map(int, input().split())

cnt=0

for i in range(1, n+1):
    if n%i==0:
        cnt += 1
    if cnt==k:
        print(i)
        break
else:
    print(-1)
```

___
[[인프런] 파이썬 알고리즘 문제풀이 (코딩테스트 대비)](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8#)
