모의고사 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42840)

```python
def solution(answers):

    # 반복문을 사용하기 위해 리스트 요소를 문자로 변경
    answers = list(map(str, answers))
    
    # 수포자의 찍는방법도 리스트 요소를 문자로 변경 
    lucks_1 = list(map(str, [1, 2, 3, 4, 5]))
    lucks_2 = list(map(str, [2, 1, 2, 3, 2, 4, 2, 5]))
    lucks_3 = list(map(str, [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]))
    
    # 찍은 문제가 얼마나 맞았는지 숫자를 셀 변수 생성
    result_1 = 0
    result_2 = 0
    result_3 = 0

    # 답안의 n번째 값이, 찍은 문제의 n번째 값과 같다면 정답처리
    for i in range(len(answers)):
        if answers[i] == lucks_1[i%5]:
            result_1 += 1
        if answers[i] == lucks_2[i%8]:
            result_2 += 1
        if answers[i] == lucks_3[i%10]:
            result_3 += 1

    # 정답 최다갯수를 맞춘 수포자를 answer에 할당
    results = [result_1, result_2, result_3]
    k = max(results)
    answer = []

    if k == result_1:
        answer.append(1)
    if k == result_2:
        answer.append(2)
    if k == result_3:
        answer.append(3)

    return answer
```
