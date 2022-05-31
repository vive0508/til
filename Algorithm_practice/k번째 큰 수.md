### K번째 큰 수

> n장의 카드 중 3장을 뽑아 각 카드에 적힌 수를 합한 값을 기록한다.   
> 같은 숫자가 카드에 여러장 있을 수 있다. 기록한 값 중 K번째로 큰 수를 출력하시오.   

```python
n, k = map(int, input().split())
a=list(map(int, input().split()))


select_sum=set()

# 인덱스가 중복되지 않게 삼중 반복문 사용
for i in range(n):
    for j in range(i+1, n):
        for m in range(j+1, n):
            select_sum.add(a[i]+a[j]+a[m])
            
select_sum=list(select_sum)
select_sum.sort(reverse=True)
print(select_sum[k-1])
```

___
[[인프런] 파이썬 알고리즘 문제풀이 (코딩테스트 대비)](https://www.inflearn.com/course/%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4-%EC%BD%94%EB%94%A9%ED%85%8C%EC%8A%A4%ED%8A%B8#)
