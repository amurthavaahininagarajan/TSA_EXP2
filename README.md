# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
# DEVELOPED BY: AMURTHA VAAHINI.KN
# REGISTER.NO: 212222240008
# Date: 
### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```
# Load the dataset
```
file_path = 'cinemaTicket_Ref.csv'
data = pd.read_csv(file_path)
```
# Extract the day and tickets sold data
```
days = data['day']
tickets_sold = data['tickets_sold']
```
# Linear Trend Estimation
```
X = [i - days[len(days) // 2] for i in days]  # Center the x-values for numerical stability
x2 = [i ** 2 for i in X]
xy = [i * j for i, j in zip(X, tickets_sold)]

n = len(days)
b = (n * sum(xy) - sum(tickets_sold) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))
a = (sum(tickets_sold) - b * sum(X)) / n
linear_trend = [a + b * X[i] for i in range(n)]
```
# Polynomial Trend Estimation (2nd degree for simplicity)
```
x3 = [i ** 3 for i in X]
x4 = [i ** 4 for i in X]
x2y = [i * j for i, j in zip(x2, tickets_sold)]
```
# Coefficients matrix for the polynomial
```
coeff = [[len(X), sum(X), sum(x2)],
         [sum(X), sum(x2), sum(x3)],
         [sum(x2), sum(x3), sum(x4)]]
```
# Constant vector
```
Y = [sum(tickets_sold), sum(xy), sum(x2y)]
A = np.array(coeff)
B = np.array(Y)
```
# Solve for polynomial coefficients
```
solution = np.linalg.solve(A, B)
a_poly, b_poly, c_poly = solution
poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]
```
# Prepare the results
```
data['Linear_Trend'] = linear_trend
data['Polynomial_Trend'] = poly_trend
```
# Display the trend equations
```
print("Linear Trend Equation: y = {:.2f} + {:.2f}x".format(a, b))
print("Polynomial Trend Equation: y = {:.2f} + {:.2f}x + {:.2f}x^2".format(a_poly, b_poly, c_poly))
```
# Visualization for Linear Trend
```
plt.figure(figsize=(10, 6))
plt.plot(days, tickets_sold, label='Actual Data', marker='o')
plt.plot(days, linear_trend, label='Linear Trend', linestyle='--')
plt.xlabel('Day')
plt.ylabel('Tickets Sold')
plt.title('Linear Trend Estimation for Tickets Sold')
plt.legend()
plt.grid(True)
plt.show()
```
# Visualization for Polynomial Trend
```
plt.figure(figsize=(10, 6))
plt.plot(days, tickets_sold, label='Actual Data', marker='o')
plt.plot(days, poly_trend, label='Polynomial Trend', linestyle='-.')
plt.xlabel('Day')
plt.ylabel('Tickets Sold')
plt.title('Polynomial Trend Estimation for Tickets Sold')
plt.legend()
plt.grid(True)
plt.show()
```

### OUTPUT
# A - LINEAR TREND ESTIMATION
![image](https://github.com/user-attachments/assets/3b2b8812-5d01-4ebd-be65-51339a0bd0ad)

# B- POLYNOMIAL TREND ESTIMATION
![image](https://github.com/user-attachments/assets/0230253d-deee-49e9-bce4-8efc120aacc7)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
