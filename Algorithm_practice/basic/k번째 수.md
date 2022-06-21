### K번째 수

> T번의 테스트를 진행한다. n개의 숫자로 이루어진 숫자열 리스트에서   
> s번째부터 e번째까지의 수를 오름차순 정렬했을 때, k번째 나타나는 숫자를 출력하시오

```python
T = int(input())

for t in range(T):
    n, s, e, k = map(int, input().split())
    a=list(map(int, input().split()))
    a=a[s-1:e]
    a.sort()
    print(f'#{t+1} {a[k-1]}')
```

___
[[인프런] 파이썬 알고리즘 문제풀이 (코딩테스트 대비)](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8#)
