숫자 문자열과 영단어 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81301)

```python
def solution(s):   
    answer = s
    change = {'zero':'0', 'one':'1', 'two':'2', 'three':'3', 'four':'4', 'five':'5', 'six':'6', 'seven':'7', 'eight':'8', 'nine':'9'}
    flag = True
    
    while flag:
        if answer not in change:
            flag = False
        for i in change:
            answer = answer.replace(i,change[i])
    
    answer = int(answer)
    return answer
```
