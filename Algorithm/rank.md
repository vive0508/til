# 순위 알고리즘
- 수의 크고 작음을 이용하여 수의 순서를 정하는 알고리즘

### 예제 1
```python
import random

# 순위를 매길 리스트 요소를 랜덤으로 생성한다.
nums = random.sample(range(50, 101), 20)

# 순위를 체크하기 위해 요소의 갯수를 맞추어 순위 리스트를 만든다.
ranks = [0 for i in range (20)]

# 두 숫자를 비교하여 수가 작은 요소에 1을 더한다
for idx, num1 in enumerate(nums):
    for num2 in nums:
        if num1 < num2:
            ranks[idx] += 1

print(f'nums : {nums}')
print(f'ranks : {ranks}')

for idx, num in enumerate(nums):
    print(f'nums: {num} \t rank: {ranks[idx]+1}')
```

<!--
- 모듈
```python
class RankDeviation:

    def __init__(self, score21, score22):
        self.score21 = score21
        self.score22 = score22
        self.rank21 = [0 for i in range(len(score21))]
        self.rank22 = [0 for i in range(len(score21))]
        self.rankDeviation = [0 for i in range(len(score21))]
   
    def setRank(self, score, rank):
        for idx, score1 in enumerate(score):
            for score2 in score:
                if score1 < score2:
                    rank[idx] += 1

    def setRank21(self):
        self.setRank(self.score21, self.rank21)
        
    def getRank21(self):
        return self.rank21
        
    def setRank22(self):
        self.setRank(self.score22, self.rank22)
    
    def getRank22(self):
        return self.rank22
    
    def printRankDeviation(self):
        for idx, vRank in enumerate(self.rank21):
            deviation = vRank - self.rank22[idx]
            
            if deviation > 0 :
                print = '↑' +  str(abs(deviation))
                
            elif deviation < 0 :
                print = '↓' +  str(abs(deviation))
  
            elif deviation == 0 :
                print = '=' +  str(abs(deviation))
            
            # 오류 발생 지점 (TypeError: 'str' object is not callable)
            print(f'21시즌 : {vRank} \t 22시즌 : {self.rank22[idx]} \t 순위변동 : {deviation}')
```

- 실행 파일
```python
from site import addusersitepackages
import module as rk
import random

score21 = random.sample(range(1,21), 20)
score22 = random.sample(range(1,21), 20)

epl = rk.RankDeviation(score21, score22)

epl.setRank21()
print(f'score21: {score21}')
print(f'rank21: {epl.getRank21()}')

epl.setRank22()
print(f'score22: {score22}')
print(f'rank22: {epl.getRank22()}')

epl.printRankDeviation()
```

-->

