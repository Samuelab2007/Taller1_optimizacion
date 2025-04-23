## Import libraries


```python
import sympy as sp
import pandas as pd
import matplotlib.pyplot as plt
import math
```


```python
# Arrays para almacenar los resultados de ambos métodos
results_criticpoint = []
```

## Define functions to use the methods


```python
def funcion_ejemplo(x):
  return ((math.e)**x) - 2*x
```

## Newton method to find local critical point


```python
def minimizar(f, x_inicial, max_iter, tol, array_resultados):
  # Definir variable x
  x = sp.Symbol('x')
  # Obtener derivada y segunda derivada de la funcion ingresada
  derivative_x = sp.diff(f(x), x)
  second_derivative_x = sp.diff(derivative_x, x)
  x_i = x_inicial

  for i in range(max_iter):
    # Obtain next value
    x_i = x_i - derivative_x.subs(x, x_i)/second_derivative_x.subs(x, x_i)
    eval_derivative = derivative_x.subs(x, x_i)
    eval_second_derivative = second_derivative_x.subs(x, x_i)
    error = abs(eval_derivative)
    array_resultados.append([i+1, x_i.evalf(), eval_derivative.evalf(), eval_second_derivative.evalf(), error])
    if abs(eval_derivative) <= tol:
      return x_i.evalf()

  raise Exception("Max iterations reached")
```


```python
minimizar(funcion_ejemplo, 2, 100, 0.0001, results_criticpoint)
```




$\displaystyle 0.693189402250512$



## Plot de resultados


```python
df_criticpoint = pd.DataFrame(results_criticpoint, columns=['Iteracion', 'x_i', 'derivative_xi', 'second_derivative_xi', 'error'])
df_criticpoint
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Iteracion</th>
      <th>x_i</th>
      <th>derivative_xi</th>
      <th>second_derivative_xi</th>
      <th>error</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1.27067056647323</td>
      <td>1.56324115146432</td>
      <td>3.56324115146432</td>
      <td>1.56324115146432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.831957303739969</td>
      <td>0.297811857374462</td>
      <td>2.29781185737446</td>
      <td>0.297811857374462</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.702350584017167</td>
      <td>0.0184917699994616</td>
      <td>2.01849176999946</td>
      <td>0.0184917699994616</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.693189402250512</td>
      <td>8.44451638299937e-5</td>
      <td>2.00008444516383</td>
      <td>8.44451638299937e-5</td>
    </tr>
  </tbody>
</table>
</div>



El punto mínimo se halla en muy pocas iteraciones, en ciertos casos en la primera iteración ya se encuentra aquel valor


```python
# plot
fig, ax = plt.subplots()

ax.plot(df_criticpoint['Iteracion'], df_criticpoint['error']) # 'Iteracion' en x, 'Error' en y

plt.title("Error por iteracion")
plt.xlabel("Iteracion")
plt.ylabel("Error")
plt.show()
```


    
![png](output_11_0.png)
    



```python

```
