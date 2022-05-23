환경설정
===

> 데이터사이언스 학습을 위한 환경설정에 관련된 내용입니다.   
> 윈도우 기준으로 작성하였으므로, 맥 유저분들은 다른 방법을 이용해주시기 바랍니다.

## 1. Conda 환경설정
- conda 설치 후, Anaconda Prompt를 실행하여 하기 설정을 진행한다.
```python
1. conda --version : 콘다의 현제 버전 확인
2. conda create -n 환경명 python=3.8 : conda 환경 생성
3. conda activate 환경명 : conda 환경 활성화
4. conda deactivate : conda 환경 비활성화
5. conda env list : conda 환경 목록 조회
6. conda en remove -n 환경명 : conda 환경 제거
```
추가로 필요한 내용은 [레퍼런스](https://sjquant.tistory.com/7)에서 확인

## 2. Jupyter Notebook
- conda 환경을 활성화한 상태로 하기 명령을 실행한다.
```python
1. conda install jupyer : conda 환경에 jupyter notebook 설치
2. 패키지 설치
- conda install ipython
- conda install matplotlib
- conda install seaborn
- conda install pandas
- conda install scikit-learn
- conda install xlrd
3. jupyer notebook : jupyter notebook 실행


#tip
- conda install -y 모듈 : y입력 없이 설치
```
[jupyter notebook 단축키](https://github.com/vive0508/TIL/blob/main/ETC/jupyter_shortcut.md)

## 3. matplotlib 한글 설정 (with Jupyter Notebook)
- matplotlib 패키지에서는 한글을 지원하지 않아서 한글이 깨지는 오류가 발생한다.
```python
import matplotlib.pyplot as plt
%matplotlib inline
plt.title("데이터사이언스")
```
- 이 문제를 해결하기 위해 하기의 방법을 사용합니다.
```python
from matplotlib import font_manager

f_path = "C:\Windows\Fonts\malgun.ttf"
font_manager.FontProperties(fname=f_path).get_name()
```
'Malgun Gothic'

- 위의 코드에서 나온 결과를 family에 할당하면 오류가 해결됩니다.
```python
from matplotlib import rc
rc("font", family="Malgun Gothic")
```
- 결과적으로 하기의 코드를 앞으로 이용하면 됩니다.
```python
import matplotlib.pyplot as plt
%matplotlib inline
from matplotlib import rc
rc("font", family="Malgun Gothic")
```

## 4. Visul Studio Code (with Conda)
- 콘다 가상환경을 활성화한 상태로 vscode를 실행시킨다.
```
1. ctrl + shift + p를 누른다.
2. select interprter을 선택한다.
3. 현재 사용하고 있는 conda 환경을 선택한다.
```

## 5. 구글 Colab
- 구글의 [colab](https://colab.research.google.com/)은 리눅스 기반의 환경이다.
```python
!cat /proc/cpuinfo : 현재 연결된 CPU 확인
!ls : 해당 파일의 하위 항목 조회
!pws : 해당 파일의 상위 항목 조회
```  
- colab에서는 matplotlib 한글 폰트를 지원하지 않는다.   
```python
# 리눅스 명령어로 필요한 한글 폰트를 설치한다.
!apt-get update -qq
!apt-get install fonts-nanum* -qq

# 다운받은 폰트로 기본 세팅을 한다.
import matplotlib.pyplot as plt
import matplotlib as mpl
%matplotlib inline

plt.rcParams['axes.unicode_minus'] = False

path = '/usr/share/fonts/truetype/nanum/NanumGothicEco.ttf'
font_name = mpl.font_manager.FontProperties(fname=path).get_name()
mpl.rc('font', family=font_name)
mpl.font_manager._rebuild()

# 런타임 다시 시작을 하고 나서 아래의 코드를 실행한다.
plt.title('데이터사이언스')
```
