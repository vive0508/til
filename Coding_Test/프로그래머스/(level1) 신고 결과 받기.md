신고 결과 받기 (level 1)
===

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92334)

```python
def solution(id_list, report, k):
    # 신고자/ 피신고자 딕셔너리 생성
    reporter = {}
    reported = {}
    
    # 리포트에 있는 신고 데이터를 하나씩 꺼내서
    for i in report:
        # user, bad에 값을 할당
        user, bad = i.split()
        
        # 신고자 딕셔너리에 해당 user가 없으면, 빈집합을 만든 후 bad 추가
        if user not in repoter:
            reporter[user] = set()
            reporter[user].add(bad)
        # 신고자 딕셔너리에 해당 user가 있으면, 기존 집합에 bad를 추가
        else :
            reporter[user].add(bad)

        # 피신고자 딕셔너리에 해당 bad가 없으면, 빈집합을 만든 후 user추가
        if bad not in reported:
            reported[bad] = set()
            reported[bad].add(user)
        # 피신고자 딕셔너리에 해당 bad가 있으면, 기존 집합에 user를 추가
         else:
             reported[bad].add(user)
            
    # id 요소의 갯수만큼, 0을 가진 리스트 생성 (메일보낸 숫자를 카운팅 할)
    answer = [0 for _ in range(len(id_list))]
    
    # 반복문을 통해 id_list 리스트에 있는 id를 하나씩 가져옴
    for i in range(len(id_list)):
        id = id_list[i]

        # 해당 id가 신고한 이력이 없으면 넘어감
        if id not in reporter:
          continue

        # 해당 id가 신고한 이력이 있으면 반복문 실행
        # 신고한 이력을 확인해보고, 피신고 딕셔너리에서 기록을 조회
        for r in reporter[id]:
          # 피신고 횟수가 k번 이상이면, 메일 보낸 횟수를 하나 추가
          if len(reported[r]) >= k:
              answer[i] += 1
                   
    return answer
```

## 기억할 것
- split()과 함께 튜플 사용
```python
number = '일 이 삼'.split()
type(number)
```
list

```python
a, b, c = '일 이 삼'.split()
print(a)
print(b)
print(c)
```
일   
이   
삼   

- 집합 활용 ([링크](https://github.com/vive0508/TIL/blob/main/Python/grammar_set.md))
```python
집합명.add()
집합명.update()
집합명.remove()
```
