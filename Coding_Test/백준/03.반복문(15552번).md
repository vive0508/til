## BAEKJOON ONLINE JUDGE
### 단계별로 풀어보기
#### 03. 반복문 ([15552번](https://www.acmicpc.net/problem/15552))

> 첫 줄에 테스트케이스의 개수 T가 주어진다.   
> 각 테스트케이스마다 A+B를 한 줄에 하나씩 순서대로 출력한다.
___
- 시간 초과
```python
t = int(input())

for _ in range(t):
    a,b = map(int, input().split())
    print(a+b)
```
값은 나오지만, 시간초과로 문제풀이 실패

- sys.stdin.readline() 활용
```python
import sys  # sys모듈 읽어들이기

t = int(sys.stdin.readline())

for _ in range(t):
    a,b = map(int, sys.stdin.readline().split())
    print(a+b)
```
Python을 사용하고 있다면, input 대신 sys.stdin.readline을 사용할 수 있다.
