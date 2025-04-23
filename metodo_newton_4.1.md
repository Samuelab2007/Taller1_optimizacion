## Import libraries


```python
import sympy as sp
import pandas as pd
import matplotlib.pyplot as plt
```


```python
# Arrays para almacenar los resultados de ambos métodos
results_criticpoint = []
```

## Define functions to use the methods


```python
def funcion_ejemplo(x):
  return (-1.5*(x**6))-(2*(x**4))+(12*x)
```


```python
def raiz(f, x_inicial, max_iter, tol):
  # Definir variable x
  x = sp.Symbol('x')
  # Obtener derivada de la funcion ingresada
  derivative_x = sp.diff(f(x), x)

  x_i = x_inicial
  for i in range(max_iter):
    # Obtain next value
    x_i = x_i - f(x_i)/derivative_x.subs(x, x_i)
    f_xi = f(x_i)
    error = abs(f_xi.evalf())
    results_raiz.append([i+1, x_i.evalf(), f_xi.evalf(), error])
    if abs(f_xi) <= tol:
      return x_i.evalf()

  raise Exception("Max iterations reached")
```


```python
raiz(funcion_ejemplo, 0.8, 100, 0.0001)
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
minimizar(funcion_ejemplo, -0.5, 100, 0.0001, results_criticpoint)
```




$\displaystyle 0.916915282744097$



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
      <td>1.00709219858156</td>
      <td>-5.49513089392581</td>
      <td>-70.6318735908260</td>
      <td>5.49513089392581</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0.929292607340934</td>
      <td>-0.657602421307294</td>
      <td>-54.2860719254173</td>
      <td>0.657602421307294</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0.917178958333308</td>
      <td>-0.0137199120748752</td>
      <td>-52.0333039397645</td>
      <td>0.0137199120748752</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0.916915282744097</td>
      <td>-6.35661457515369e-6</td>
      <td>-51.9850943386392</td>
      <td>6.35661457515369e-6</td>
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


    
![png](output_13_0.png)
    



```python

```
