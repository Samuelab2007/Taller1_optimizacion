La interpolación cuadrática es un método que se utiliza para obtener máximos y mínimos y optimizarlos.


```python
import math
import pandas as pd
import matplotlib.pyplot as plt
```


```python
def funcion(x):
  return (x**2) + 2*x - 9
```


```python
results = []
```


```python
def interpolacion_cuadratica(f, x0, x1, x2, tol, max_iter):
  # El valor x3 que calculamos describe un valor crítico de la parábola con la que aproximamos la región.

  for i in range(max_iter):
    f_x0 = f(x0)
    f_x1 = f(x1)
    f_x2 = f(x2)

    x3 = (f_x0*(x1**2 - x2**2) + f_x1*(x2**2 - x0**2) + f_x2*(x0**2 - x1**2)) / (2*f_x0*(x1 - x2) + 2*f_x1*(x2 - x0) + 2*f_x2*(x0 - x1))
    f_x3 = f(x3)
    # Después de calcular x3 hay que reemplazar alguno de los puntos x0, x1 o x2 por este valor.
    # En mi opinión lo más acertado es descartar el punto más lejano a x3
    error = abs(x3 - x1)

    results.append([i+1, x0, x1, x2, x3, f_x0, f_x1, f_x2, f_x3, error])
    if error < tol:
      return x3

    if ((f_x3 > f_x1) and (x3 > x1)):
      x0 = x1
      x1 = x3
    elif ((f_x3 > f_x1) and (x3 < x1)):
      x2 = x1
      x1 = x3
    elif ((f_x3 < f_x1) and (x3 < x1)):
      x0 = x1
      x1 = x3
    elif ((f_x3 < f_x1) and (x3 > x1)):
      x2 = x1
      x1 = x3
  raise Exception("No se encontró una solución")
```


```python
interpolacion_cuadratica(funcion, -4, 0, 2, 0.0001, 1000)
```




    -1.0



## Plot the results


```python
df = pd.DataFrame(results, columns=['Iteracion', 'x0', 'x1', 'x2', 'x3', 'f(x0)', 'f(x1)', 'f(x2)', 'f(x3)', 'Error'])
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
      <th>x0</th>
      <th>x1</th>
      <th>x2</th>
      <th>x3</th>
      <th>f(x0)</th>
      <th>f(x1)</th>
      <th>f(x2)</th>
      <th>f(x3)</th>
      <th>Error</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>-4</td>
      <td>0.0</td>
      <td>2</td>
      <td>-1.0</td>
      <td>-1</td>
      <td>-9.0</td>
      <td>-1</td>
      <td>-10.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>-1.0</td>
      <td>2</td>
      <td>-1.0</td>
      <td>-9</td>
      <td>-10.0</td>
      <td>-1</td>
      <td>-10.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# plot
fig, ax = plt.subplots()

ax.plot(df['Iteracion'], df['Error']) # 'Iteracion' en x, 'Error' en y

plt.title("Error por iteracion")
plt.xlabel("Iteracion")
plt.ylabel("Error")
plt.show()
```


    
![png](output_8_0.png)
    



```python

```
