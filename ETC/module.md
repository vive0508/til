Python 모듈 설치
===

### 1. pip 명령
- Python 공식 모듈 관리자
```python
- pip list : 현재 설치된 모듈 리스트 반환
- get_ipython().system("pip list") : 현재 설치된 모듈 리스트 반환
- pip install 모듈이름 : 모듈 설치
- pip unistall 모듈이름 : 설치된 모듈 제거
```

### 2. conda 명령
- pip를 사용하면 conda 환경에서 dependency 관리가 정확하지 않을 수 있다.
- 아나콘다에서는 가급적 conda 명령으로 모듈을 관리하는 것을 권장한다.
- 그러나 모든 모듈이 conda로 설치되는 것은 아니다.
```python
- conda list : 현재 설치된 모듈 리스트 반환
- conda install 모듈이름 : 모듈 설치 
- conda unistall 모듈이름 : 설치된 모듈 제거
- conda install -c 채널이름 모듈이름 : 지정된 배포 채널에서 모듈 설치
```
