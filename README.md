# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date:24-08-2026
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

data['date'] = pd.to_datetime(data['date'])
data = data.set_index('date')
resampled_data = data['money'].resample('YE').sum().to_frame()
resampled_data.head()

resampled_data.index = resampled_data.index.year
resampled_data.reset_index(inplace=True)
resampled_data.rename(columns={'Month': 'Year'}, inplace=True)
resampled_data.head()

years = resampled_data['date'].tolist()
money = resampled_data['money'].tolist()
X = [i - years[len(years) // 2] for i in years]
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, money)]

n = len(years)
b = (n * sum(xy) - sum(money) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(money) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2,money)]

coeff = [[len(X), sum(X), sum(x2)], [sum(X), sum(x2), sum(x3)], [sum(x2), sum(x3), sum(x4)]]
Y = [sum(money), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
A_linear = np.array([[n, sum(X)], [sum(X), sum(x2)]])
B_linear = np.array([sum(money), sum(xy)])

solution = np.linalg.solve(A_linear, B_linear)
a_poly, b_poly = solution
poly_trend = [a_poly + b_poly * X[i] for i in range(n)]
print(f"Linear Trend: y={a:.2f} + {b:.2f}x")
print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x")

resampled_data['Linear Trend'] = linear_trend
resampled_data['Polynomial Trend'] = poly_trend
resampled_data.set_index('date', inplace=True)

resampled_data['money'].plot(kind='line',color='blue',marker='o') #alpha=0.3 makes
resampled_data['Linear Trend'].plot(kind='line',color='black',linestyle='--')

resampled_data['money'].plot(kind='line',color='blue',marker='o')
resampled_data['Polynomial Trend'].plot(kind='line',color='black',marker='o')
```
A - LINEAR TREND ESTIMATION
Linear Trend: y=29600.78 + -56230.02x

B- POLYNOMIAL TREND ESTIMATION
Polynomial Trend: y=29600.78 + -56230.02x

### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="571" height="432" alt="image" src="https://github.com/user-attachments/assets/608193d2-b377-4ca5-b427-a1bf197e4484" />

B- POLYNOMIAL TREND ESTIMATION
<img width="571" height="432" alt="image" src="https://github.com/user-attachments/assets/a0cba73b-6134-4990-a240-6a70a79a886f" />

### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
