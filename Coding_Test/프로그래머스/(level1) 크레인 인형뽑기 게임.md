크레인 인형뽑기 게임 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64061)


```
def solution(board, moves):
    
    # 인형을 담을 바구니 bucket 변수를 생성합니다
    # answer 변수로 사라진 인형의 갯수를 셉니다.
    bucket = []
    answer = 0
    
    # for 반복문으로 크레인 작동 순서를 하나씩 실행합니다.
    for move in moves:
        # move를 2차원 배열 board의 인덱스로 사용할 준비를 합니다. 
        index = move - 1
        # 2차원 배열 board의 행(row)을 위에서부터 하나씩 가져옵니다.
        for row_info in board:
            # 만약 주어진 인덱스에 해당하는 열(column)이 값을 갖고 있을 경우 바구니에 추가합니다.
            if row_info[index] != 0:
                bucket.append(row_info[index])
                # 바구니에 추가를 했으면, board에서는 0으로 보이도록 초기화를 시킵니다.
                row_info[index] = 0
                
                # 만약 바구니의 제일 위에 쌓여진 번호 두개가 같다면 삭제하고, answer에 숫자를 더합니다.
                if len(bucket) >= 2 and bucket[-1] == bucket[-2]:
                    bucket = bucket[0:-2]
                    answer += 2
                break
    return answer
```
