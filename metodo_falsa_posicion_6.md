```python
import pandas as pd
import matplotlib.pyplot as plt
import math
```


```python
def funcion_prueba(x):
  return math.tanh((x**2) - 9)
```


```python
results = []
```


```python
def calcular_raiz(f, x_l, x_u, tol=0.01, max_iter=100):

  f_xl = f(x_l)
  f_xu = f(x_u)

  if f_xu * f_xl > 0:
    raise ValueError("No existe raíz en el intervalo dado")

  for i in range(max_iter):

    f_xl = f(x_l)
    f_xu = f(x_u)

    x_r = x_u - (f_xu*(x_l - x_u))/(f_xl - f_xu)
    f_xr = f(x_r)
    error = abs(f_xr)
    results.append([i+1, x_l, x_u, f_xl, f_xu, x_r, f_xr, error])
    if error <= tol:
      return x_r, i+1
    elif f_xl * f_xr < 0:
      x_u = x_r
    elif f_xr * f_xu < 0:
      x_l = x_r

  raise ValueError("No se pudo encontrar la raíz")
```


```python
calcular_raiz(funcion_prueba, 0, 4, 0.0001, 1000000)
```




    (2.99999999842532, 4)




```python
df = pd.DataFrame(results, columns=['Iteracion','x_l', 'x_u', 'f_xl', 'f_xu', 'x_r', 'f_xr', 'error'])
df
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
      <th>x_l</th>
      <th>x_u</th>
      <th>f_xl</th>
      <th>f_xu</th>
      <th>x_r</th>
      <th>f_xr</th>
      <th>error</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>-1.000000</td>
      <td>0.999998</td>
      <td>2.000002</td>
      <td>-9.999092e-01</td>
      <td>9.999092e-01</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2.000002</td>
      <td>4.000000</td>
      <td>-0.999909</td>
      <td>0.999998</td>
      <td>2.999956</td>
      <td>-2.625140e-04</td>
      <td>2.625140e-04</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2.999956</td>
      <td>4.000000</td>
      <td>-0.000263</td>
      <td>0.999998</td>
      <td>3.000219</td>
      <td>1.312273e-03</td>
      <td>1.312273e-03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2.999956</td>
      <td>3.000219</td>
      <td>-0.000263</td>
      <td>0.001312</td>
      <td>3.000000</td>
      <td>-9.448080e-09</td>
      <td>9.448080e-09</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot
fig, ax = plt.subplots()

ax.plot(df['Iteracion'], df['error']) # 'Iteracion' en x, 'Error' en y

plt.title("Error por iteracion")
plt.xlabel("Iteracion")
plt.ylabel("Error")
plt.show()
```


    
![png](output_6_0_5.png)
    



```python

```
