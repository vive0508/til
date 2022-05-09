# 이진 검색 알고리즘 (binary search algorithm)
- 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘이다.   
- 찾고자 하는 값과 중앙값의 크고 작음을 비교하여 데이터를 검색한다.   
- 검색 원리상 정렬된 리스트에만 사용할 수 있다는 단점이 있다.   
- 하지만, 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되므로 속도가 빠르다.

[개념설명(위키백과)](https://ko.wikipedia.org/wiki/%EC%9D%B4%EC%A7%84_%EA%B2%80%EC%83%89_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)

___
## 예제 1
```python
# 리스트를 오름차순으로 정렬한다
nums = [5, 9, 3, 7, 6, 1, 5, 10, 2, 8]
nums.sort()

searchNum = int(input('찾는 숫자를 입력하세요 : '))
searchResultIdx = -1

# 첫 인덱스, 끝 인덱스, 가운데 인덱스
staIdx = 0
endIdx = len(nums)-1
midIdx = (staIdx + endIdx) // 2
midVal = nums[midIdx]

while searchNum >= nums[0] and searchNum <= nums[len(nums)-1]:

    # 검색값이 리스트의 마지막 요소와 같을 때
    if searchNum == nums[len(nums)-1] :
        searchResultIdx = len(nums)-1
        break
    
    # 검색값이 중앙값보다 클 때
    elif searchNum > midVal :
        staIdx = midIdx
        midIdx = (staIdx + endIdx) // 2
        midVal = nums[midIdx]
        print(f'midIdx : {midIdx}')
        print(f'midVal : {midVal}')

    # 검색값이 중앙값보다 작을 때
    elif searchNum < midVal :
        endIdx = midIdx
        midIdx = (staIdx + endIdx) // 2
        midVal = nums[midIdx]
        print(f'midIdx : {midIdx}')
        print(f'midVal : {midVal}')

    # 검색값이 중앙값과 같을 때
    elif searchNum == midVal :
        searchNum == midVal
        searchResultIdx = midIdx
        break

print(f'searchResultIdx : {searchResultIdx}')
```
