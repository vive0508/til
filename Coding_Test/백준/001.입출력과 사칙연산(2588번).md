## BAEKJOON ONLINE JUDGE
### 단계별로 풀어보기
#### 01. 입출력과 사칙연산 ([2588번](https://www.acmicpc.net/problem/2588))

(세 자리 수) × (세 자리 수)는 다음과 같은 과정을 통하여 이루어진다.

![image](https://user-images.githubusercontent.com/101171109/166952739-7873bde9-aa4f-43cf-a4a7-a5cbd5624720.png)

1)과 (2)위치에 들어갈 세 자리 자연수가 주어질 때 (3), (4), (5), (6)위치에 들어갈 값을 구하는 프로그램을 작성하시오.

##### 예제 입력
```python
472
385
```

##### 예제 출력
```python
2360
3776
1416
181720
```

___
#### 나의 풀이
```python
# 세 자리 숫자 두 개를 입력받는다
num1 = input()
num2 = input()

# 문자열의 인덱스 기능을 활용하여 num2의 n의 자릿수에 접근하여 정수로 변환한다
num2_1 = int(num2[-1])
num2_10 = int(num2[-2])
num2_100 = int(num2[-3])

# num1, num2를 모두 정수로 변환한다
num1 = int(num1)
num2 = int(num2)

# 원하는 결과 값을 출력한다
print(num2_1 * num1)
print(num2_10 * num1)
print(num2_100 * num1)
print(num1*num2)
```

문자열의 인덱스 기능을 활용하여, 불필요하게 코드의 길이가 길어졌다고 판단 됨
___
#### 참고 풀이 ([링크](https://choseongho93.tistory.com/281))
```python
A = int(input())
B = int(input())

out1 = A*((B%100)%10)
out2 = A*((B%100)//10)
out3 = A*(B//100)
result = A*B

print(out1, out2, out3, result, sep='\n')
```
세 자리 숫자의 각 자릿수에 다음과 같이 접근하면, 코드의 길이를 줄일 수 있음
- 일의 자리 숫자 : `(B%100)%10`
- 십의 자리 숫자 : `(B%100)//10`
- 백의 자리 숫자 : `B//100`

