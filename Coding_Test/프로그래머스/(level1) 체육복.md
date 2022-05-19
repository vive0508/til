체육복 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42862)

```python
def solution(n, lost, reserve):
    # 학생들이 모두 체육복을 하나 가지고 있던 상황에서
    student = [1]*(n+2)
    
    # 체육복을 잃어버린 학생과, 여분이 있는 학생을 반영
    for r in reserve:
        student[r] += 1
    for l in lost:
        student[l] -= 1
    
    # 여벌이 있던 학생들이 앞뒤 번호에 체육복이 없는 학생들이 있으면 빌려줌
    for i in range(1, n+1):
        if student[i] == 2:
            if student[i-1] == 0:
                student[i] -= 1
                student[i-1] += 1
            elif student[i+1] == 0:
                student[i] -= 1
                student[i+1] += 1
    
    # 체육복이 있는 학생의 수를 구하면 문제풀이 완료
    answer = 0
    
    for i in range(1, n+1):
        if student[i] >= 1:
            answer += 1
    
    return answer
```
