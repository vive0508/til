# 하노이의 탑 (The Tower Of Hanoi)
## 예제 1

```python
# 원판 갯수, 출발 기둥, 도착 기둥, 경유 기둥
def moveDisc(discCnt, fromBar, toBar, viaBar):
    if discCnt ==1:
        print(f'{discCnt}disc를 {fromBar}에서 {viaBar}로 이동!')

    else :
        # (discNo-1)개들을 경유 기둥으로 이동
        moveDisc(discCnt-1, fromBar, viaBar, toBar)
        
        # discNo를 목적 기둥으로 이동
        print(f'{discCnt}disc를 {fromBar}에서 {toBar}로 이동!')
        
        # (discNo-1)개들을 도착 기둥으로 이동
        moveDisc(discCnt-1, viaBar, toBar, fromBar)

moveDisc(3, 1, 3, 2)
```
