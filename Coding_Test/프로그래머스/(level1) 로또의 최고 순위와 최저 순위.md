로또의 최고 순위와 최저 순위 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77484)

```python
def solution(lottos, win_nums):
        # 알아볼 수 없는 숫자를 제외하고 몇 개를 맞췄는지 알아본다
        cntCorrect = 0
        for num in lottos:
            if num in win_nums:
                cntCorrect +=1
        
        # 맞춘 갯수를 활용해, 최저 순위를 구한다
        minRank = 0        
        if cntCorrect > 0:
            minRank = 7 - cntCorrect
        else:    
            minRank = 6
        
        # 알아볼 수 없는 숫자가 몇 개 있는지 알아본다
        cntZero = 0
        for num in lottos:
            if num == 0:
                cntZero += 1
        
        # 알아볼 수 없는 숫자의 갯수를 활용해, 최대 순위를 구한다
        maxRank = 7 - cntCorrect - cntZero
        if maxRank ==7:
            maxRank = 6

        return[maxRank, minRank]
```
