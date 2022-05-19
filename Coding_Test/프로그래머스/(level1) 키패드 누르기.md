키패드 누르기 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/67256)

```python
def solution(numbers, hand):
    
    # 키에 따라 사용할 손
    only_left = [1, 4, 7]
    only_right = [3, 6, 9] 
    hand_position = ['*', '#']
    
    # 키의 좌표 (1을 (0,0)으로 기준)
    key_loc ={
        1: (0,0), 2: (1,0), 3:(2,0),
        4: (0,1), 5: (1,1), 6:(2,1),
        7: (0,2), 8: (1,2), 9:(2,2),
        '*': (0,3), 0: (1,3), '#':(2,3)     
    }
    
    # 눌러야할 키패드를 하나씩 반복문으로 꺼냄
    
    answer = ''
    
    for num in numbers:
        # 해당 키가 왼손으로 눌러야 한다면
        if num in only_left:
            hand_position[0] = num
            answer += 'L'
        # 해당 키가 오른손으로 눌러야 한다면
        elif num in only_right:
            hand_position[1] = num
            answer += 'R'
        # 더 가까운 손으로 눌러야 한다면
        else :
            near_hand = get_near_hand(key_loc, hand_position[0],hand_position[1], num, hand)
            if near_hand == 'L':
                hand_position[0] = num
                answer += 'L'
            elif near_hand == 'R':
                hand_position[1] = num
                answer += 'R'
                
    return answer

    
# 좌표, 현재 현재 손의 위치 l,r, 이동할 키, 주로 사용하는 손                 
def get_near_hand(key_loc,l,r,num, hand):
    # 현재 위치와 이동할 위치의 x좌표, y좌표의 거리를 구한다 
    left_distance = abs(key_loc[l][0]-key_loc[num][0])+abs(key_loc[l][1]-key_loc[num][1])
    right_distance = abs(key_loc[r][0]-key_loc[num][0])+abs(key_loc[r][1]-key_loc[num][1])

    # 이동거리가 왼손, 오른손 모두 같으면 
    if left_distance == right_distance:
        near_hand = 'L' if hand == 'left' else 'R'
    # 이동거리 같지 않다면 가까운 손으로 값을 리턴
    else :    
        near_hand = 'L' if left_distance < right_distance else 'R'
    return near_hand
```
