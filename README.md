### Developed by: DODDA JAYASRI
### Register No: 212222240028
### Date: 
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
%matplotlib inline

train = pd.read_csv("AirPassengers.csv")
train.timestamp = pd.to_datetime(train.Month, format = '%Y-%m')
train.drop('Month', axis=1, inplace = True)
train.head()
train['#Passengers'].plot()

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
adf_test(train['#Passengers'])

train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(1)
train['#Passengers_diff'].dropna().plot()
# Seasonal Differencing
n=7
train['#Passengers_diff'] = train['#Passengers'] - train['#Passengers'].shift(n)
train['#Passengers_diff'].dropna().plot()
# Transformation
train['#Passengers_log'] = np.log(train['#Passengers'])
train['#Passengers_log_diff'] = train['#Passengers_log'] - train['#Passengers_log'].shift(1)
train['#Passengers_log_diff'].dropna().plot()

```

### OUTPUT:
![image](https://github.com/user-attachments/assets/94f68a80-e167-4508-afff-b42dac7f8939)

![image](https://github.com/user-attachments/assets/bfa8e4ab-445d-43a2-8ec3-f74662de9af9)

REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/17857046-7bd7-44dc-9428-c1394de2f9c8)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/f762d90c-d979-429b-aff5-80b528bb17be)

LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/0602e303-2a10-4d7d-9ac9-bda95bfdd368)

ALL 3:

![image](https://github.com/user-attachments/assets/d56961b3-175a-49c5-843a-cc4b4ce71ca3)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
