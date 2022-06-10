시계열 데이터 분석
===

### 1. fbprophet 설치
- [C++ Build Tool 설치](https://visualstudio.microsoft.com/ko/visual-cpp-build-tools/)
- prompt 창에서 필요한 모듈 설치
```
conda install pandas-datareader 
conda install -c conda-forge fbprophet
```

### 2. 예측하기
- 예측할 그래프를 생성한다.
```python
# 필요한 모듈 불러오기
import pandas as pd 
import numpy as np 
import matplotlib.pyplot as plt 
%matplotlib inline 

# 0과 1사이의 730개의(2년간) 데이터 생성 후
# 임의의 sin값 생성
time = np.linspace(0, 1, 365*2)
result = np.sin(2*np.pi*12*time)

# 임의의 날짜 생성
dates = pd.date_range("2022-01-01", periods=365*2, freq="D")

# 날짜와 sin값으로 데이터 프레임 생성
df = pd.DataFrame({"ds": dates, "y": result})

# 데이터프레임에서 그래프를 생성
df['y'].plot(figsize=(10, 6));
```
- fbprophet을 활용하여 그래프를 예측한다
```python
from fbprophet import Prophet

# 설정을 한 후 학습을 시킨다
m = Prophet(yearly_seasonality=True, daily_seasonality=True)
m.fit(df)

# 학습 시킨 데이터를 바탕으로 예측 데이터를 생성할 수 있다.
future = m.make_future_dataframe(periods=30)
forecast = m.predict(future)

# 예측의 결과를 그래프로 그려 확인할 수 있다.
m.plot(forecast)
```
