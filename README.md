### Developed by: DODDA JAYASRI
### Register No: 212222240028
### Date: 
# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on Salesforce stock history data
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

train = pd.read_csv("Salesforce_stock_history.csv")
train.timestamp = pd.to_datetime(train.Date, format='%Y-%m-%d') 
train.drop('Date', axis=1, inplace=True)
print(train.head())
train['Open'].plot()

def adf_test(timeseries):
    print('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic', 'p-value', '#Lags Used', 'Number of Observations Used'])
    for key, value in dftest[4].items():
        dfoutput['Critical Value (%s)' % key] = value
    print(dfoutput)
adf_test(train['Open'])
# Regular Differencing
train['Open_diff'] = train['Open'] - train['Open'].shift(1)
train['Open_diff'].dropna().plot()

# Seasonal Differencing
n=7
train['Open_diff'] = train['Open'] - train['Open'].shift(n)
train['Open_diff'].dropna().plot()

# Transformation
train['Open_log'] = np.log(train['Open'])
train['Open_log_diff'] = train['Open_log'] - train['Open_log'].shift(1)
train['Open_log_diff'].dropna().plot()

```

### OUTPUT:

![image](https://github.com/user-attachments/assets/1c717994-84cb-4ba7-a375-60aa9e16b795)


REGULAR DIFFERENCING:

![image](https://github.com/user-attachments/assets/e106abcd-2218-44c9-8207-f24911192381)

SEASONAL ADJUSTMENT:

![image](https://github.com/user-attachments/assets/3cf65b2d-238a-423e-bab3-77aa85d06f66)

LOG TRANSFORMATION:

![image](https://github.com/user-attachments/assets/c8bb9916-f034-440f-a7c8-3b443e386659)

ALL 3:

![image](https://github.com/user-attachments/assets/96e116cd-2e8d-4a47-9ee0-63260720947f)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on Salesforce stock history data.
