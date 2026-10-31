# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 31.10.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data

### SOFTWARE USED:
Google Colab

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```py

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv('Netflix-Subscriptions.csv')
data.head()

data['Time Period'] = pd.to_datetime(data['Time Period'])
data.set_index('Time Period', inplace=True)
data = data.sort_index()

data['Subscribers_diff'] = data['Subscribers'].diff()

result = seasonal_decompose(data['Subscribers'], model='additive', period=4)
data['Subscribers_seasonal_diff'] = result.resid

data['Subscribers_log'] = np.log(data['Subscribers'])
data['Subscribers_log_diff'] = data['Subscribers_log'].diff()

result = seasonal_decompose(data['Subscribers_log_diff'].dropna(), model='additive', period=4)
data['Subscribers_log_seasonal_diff'] = result.resid

plt.figure(figsize=(16, 16))

plt.subplot(6, 1, 1)
plt.plot(data['Subscribers'], label='Original')
plt.legend(loc='best')
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Subscribers')

plt.subplot(6, 1, 2)
plt.plot(data['Subscribers_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Subscribers')

plt.subplot(6, 1, 3)
plt.plot(data['Subscribers_seasonal_diff'], label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Adjusted Subscribers')

plt.subplot(6, 1, 4)
plt.plot(data['Subscribers_log'], label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log Subscribers')

plt.subplot(6, 1, 5)
plt.plot(data['Subscribers_log_diff'], label='Log Difference')
plt.legend(loc='best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Log Subscribers')

plt.subplot(6, 1, 6)
plt.plot(data['Subscribers_log_seasonal_diff'], label='Log Seasonal Difference')
plt.legend(loc='best')
plt.title('Log Transformation, Regular and Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Log Subscribers')

plt.tight_layout()
plt.show()

data.plot(kind='line')
plt.show()
```

### OUTPUT:

<img width="1590" height="1590" alt="image" src="https://github.com/user-attachments/assets/ffbaf209-e20a-4e36-bac0-b1f3d85d963a" />
<img width="547" height="420" alt="image" src="https://github.com/user-attachments/assets/e7c13b31-f080-4b58-b97d-84a7cd432d79" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
