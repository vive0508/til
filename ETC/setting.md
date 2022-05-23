환경설정
===

> 데이터사이언스 학습을 위한 환경설정에 관련된 내용입니다.   
> 윈도우 기준으로 작성하였으므로, 맥 유저분들은 다른 방법을 이용해주시기 바랍니다.

## 1. conda 환경설정
- conda 설치 후, Anaconda Prompt를 실행하여 하기 설정을 진행한다.
```
1. conda --version : 콘다의 현제 버전 확인
2. conda create -n 환경명 python=3.8 : conda 환경 생성
3. conda activate 환경명 : conda 환경 활성화
4. conda deactivate : conda 환경 비활성화
5. conda env list : conda 환경 목록 조회
6. conda en remove -n 환경명 : conda 환경 제거
```
추가로 필요한 내용은 [레퍼런스](https://sjquant.tistory.com/7)에서 확인

## 2. jupyer notebook
- conda 환경을 활성화한 상태로 하기 명령을 실행한다.
```
1. conda install jupyer : conda 환경에 jupyter notebook 설치
2. 모듈 설치
- conda install ipython
- conda install matplotlib
- conda install seaborn
- conda install pandas
- conda install scikit-learn
- conda install xlrd
3. jupyer notebook : jupyter notebook 실행


tip
- conda install -y 모듈 : 
```
