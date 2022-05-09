# 선형 검색 알고리즘(linear search algorithm)

- 리스트에서 특정한 값을 찾는 알고리즘의 하나다.   
- 리스트에서 찾고자 하는 값을 맨 앞에서부터 끝까지 차례대로 찾아 나간다.   
- 검색할 리스트의 길이가 길면 비효율적이다.   
- 하지만, 검색 방법 중 가장 단순하여 구현이 쉽고 정렬되지 않은 리스트에서도 사용할 수 있다는 장점이 있다.   
- 순차 검색 알고리즘(sequential search algorithm)이라고도 불린다.   

[개념 설명(위키백과)](https://ko.wikipedia.org/wiki/%EC%88%9C%EC%B0%A8_%EA%B2%80%EC%83%89_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
___
## 예제 1

```python
players = ['손흥민', '황희찬', '황의조', '황인범', '이재성', '정우영', '김민재', '김영권', '김태환', '김진수', '김승규']

searchPlayer = input('찾으려는 선수 입력:')

# 존재하지 않는 인덱스를 -1로 설정
searchResultIdx = -1

n = 0
while True :
  # 검색한 결과가 리스트에 없다면,
  if n == len(players):
    searchResultIdx=-1
    break
  
  # 검색한 결과가 리스트에 있다면,
  elif players[n] == searchPlayer:
    searchResultIdx=n
    break
    
  n += 1

print(f'{searchPlayer} 선수는 {searchResultIdx}번째 인덱스에 있습니다')
```
손흥민 선수는 0번째 인덱스에 있습니다

## 예제 2
### 보초법
반복의 종료를 알리는 특정한 값인 보초(Sentinel) 값을 사용하여   
종료 조건중 검색 실패 조건을 제거하여 판단 횟수를 줄이는 방법

```python
players = ['손흥민', '황희찬', '황의조', '황인범', '이재성', '정우영', '김민재', '김영권', '김태환', '김진수', '김승규']

searchPlayer = input('찾으려는 선수 입력:')
searchResultIdx = -1

# 리스트 끝에 검색값을 추가
players.append(searchPlayer)

n = 0
while True :
  if players[n] == searchPlayer:
        if n != len(players) - 1:
            searchResultIdx=n
        break
    
  n += 1

print(f'{searchPlayer} 선수는 {searchResultIdx}번째 인덱스에 있습니다')
```
조현우 선수는 -1번째 인덱스에 있습니다

## 예제 3
```python
# 리스트 내에서 검색하는 숫자가 어디에 있는지(위치), 몇 개 있는지 구하시오

nums = [6, 9, 12, 4, 6, 9, 2, 4, 9, 5, 10]

searchNum = int(input('찾는 숫자를 입력하세요 : '))
searchResultIdxs = []

nums.append(searchNum)

n = 0
while True:
    if nums[n] == searchNum:
        if n != len(nums)-1:
            searchResultIdxs.append(n)
        else:
            break
    n += 1

print(f'리스트 내 {searchNum}의 위치 : {searchResultIdxs}')
print(f'리스트 내 {searchNum}의 갯수 : {len(searchResultIdxs)}')
```
