# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION

REG NO: 212222240057

NAME : Mahalakshmi k

### Date: 

### AIM:

To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:

1. Import the required packages like pandas and numpy

2. Read the data using the pandas

3. Perform the decomposition process for the required data.

4. Plot the data according to need, either seasonal_decomposition or trend plot.

5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
from statsmodels.tsa.stattools import adfuller

# Load the COVID-19 dataset
url = 'https://covid.ourworldindata.org/data/owid-covid-data.csv'
data = pd.read_csv(url, parse_dates=['date'])

# Filter data for a specific country (e.g., United States)
country = 'USA'
country_data = data[data['iso_code'] == 'USA'][['date', 'new_cases']]
country_data.set_index('date', inplace=True)

# Drop missing values
country_data['new_cases'].fillna(0, inplace=True)

# Visualize the time series
plt.figure(figsize=(12, 6))
plt.plot(country_data['new_cases'], label='Daily New Cases', color='blue')
plt.title('Daily New COVID-19 Cases in the USA')
plt.xlabel('Date')
plt.ylabel('Number of Cases')
plt.legend()
plt.grid()
plt.show()

# Check for stationarity
result = adfuller(country_data['new_cases'])
print('ADF Statistic:', result[0])
print('p-value:', result[1])

# Decompose the time series
decomposition = seasonal_decompose(country_data['new_cases'], model='additive')

# Plot the decomposition
trend = decomposition.trend
seasonal = decomposition.seasonal
residual = decomposition.resid

plt.figure(figsize=(12, 12))
plt.subplot(411)
plt.plot(country_data['new_cases'], label='Original')
plt.legend(loc='upper left')
plt.subplot(412)
plt.plot(trend, label='Trend')
plt.legend(loc='upper left')
plt.subplot(413)
plt.plot(seasonal, label='Seasonal')
plt.legend(loc='upper left')
plt.subplot(414)
plt.plot(residual, label='Residual')
plt.legend(loc='upper left')
plt.tight_layout()
plt.show()
```

### OUTPUT:

FIRST FIVE ROWS:

![Screenshot (651)](https://github.com/user-attachments/assets/b608d8f8-1b56-46e6-9759-fa62756bb776)


SEASONAL PLOT REPRESENTATION :

![Screenshot (652)](https://github.com/user-attachments/assets/8b56e75b-7232-44e3-b9e0-a8fe163d4b58)


### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
