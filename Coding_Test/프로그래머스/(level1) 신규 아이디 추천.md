신규 아이디 추천 (level 1)
===
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72410)

### 문제 풀이
```python
def solution(new_id):
  answer = ''

  # 1단계 : 대문자를 소문자로 치환
  new_id = new_id.lower()
  
  # 2단계 : 소문자, 숫자, 빼기, 밑줄, 마침표만 가능
  for c in new_id:
    if c.isalpha() or c.isdigit() or c in "-_.":
      answer += c
      
  # 3단계 : 마침표 2번 불가능
  while '..' in answer:
    answer = answer.replace('..', '.')
    
  # 4단계 : 마침표가 처음이나 끝에 위치 불가능
  if answer[0:1] == '.':
    answer = answer[1:]
  if answer and answer[-1] == '.':
    answer = answer[:-1]
    
  # 5단계 : 빈문자열이면 a 대입
  if answer == '':
    answer = 'a'
  
  # 6단계 : 길이 16자 이상이면, 15자로 남김 (마침표 고려)
  answer = answer[:15]
  if answer[-1] == '.':
    answer = answer[:-1]
  
  # 7단계 : 길이가 2자 이하이면, 길이 3으로 맞춤
  while len(answer) < 3:
    answer += answer[-1]
    
  return answer
```
[레퍼런스](https://coding-grandpa.tistory.com/93)

---
## 기억할 것
- 알파벳 대소문자
```
문자.upper() : 모두 대문자로
문자.lower() : 모두 소문자로
```

- 소문자인지, 숫자인지 확인하기([레퍼런스](https://appia.tistory.com/178))
```
# 알파벳인지 확인
문자.isalpha()

# 숫자인지 확인
문자.isdigit()

# 알파벳 또는 숫자인지 확인
문자.isalnum()
```
- 문자 찾아 바꾸기
```
문자.replace('찾는내용','바꿀내용')
```

- string index out of range 오류
[링크](https://velog.io/@vive0508/pythonError1)로 설명을 대체합니다.
