# Optimización multidimensional por multiplicadores de Lagrange

[Articulo](https://es.khanacademy.org/math/multivariable-calculus/applications-of-multivariable-derivatives/constrained-optimization/a/lagrange-multipliers-single-constraint)

Esta técnica permite encontrar el máximo o el mínimo de una función multivariable $f(x,y,...)$, cuando hay alguna restricción en los valores de entrada que se pueden usar.

Esta técnica solo aplica a restricciones de la forma: $g(x,y,...)=c$ donde $g$ es otra función multivariable con el mismo espacio de entrada que $f$ y $c$ es una constante.

## Idea central

Buscar puntos en donde las curvas de nivel de $f$ y $g$ sean tangentes entre sí.

$∇f(x_0,y_0)=\lambda_0∇g(x_0,y_0)$

Donde:$\lambda_0$ es una constante


```python
import sympy as sp
import pandas as pd
import matplotlib.pyplot as plt
```


```python
def gradiente_fxy(expr, variables):

  # x = sp.Symbol('x')
  # y = sp.Symbol('y')

  # df_dx = sp.diff(f(x,y), x)
  # df_dy = sp.diff(f(x,y), y)

  return sp.Matrix([sp.diff(expr, var) for var in list(variables)])
```


```python
def mult_lagrange(f,g, variables):

  lmbda = sp.Symbol('lambda')

  if callable(f):
        f = f(*variables)
  if callable(g):
        g = g(*variables)


  # Obtiene la gradiente de la función f
  gradiente_f = gradiente_fxy(f, variables)

  # Obtiene la gradiente de la función g
  gradiente_g = gradiente_fxy(g, variables)

  # ∇f - λ∇g = 0
  ecuacion_lagrangiano = gradiente_f - lmbda * gradiente_g

  # sistema de ecuaciones
  ecuaciones = list(ecuacion_lagrangiano) + [g]

  # Agregamos la condicion
  ecuaciones = sp.Matrix(ecuaciones)

  # Soluciona el sistema para todas las variables y los lambdas
  solucion = sp.solve(ecuaciones, variables + [lmbda], dict=True)

  return solucion
```


```python
x, y = sp.symbols('x y')
# lmbda = sp.Symbol('lambda')
f = lambda x,y: 4*x+3*y
g = lambda x,y: 2*(x**2)+4*(y**2) - x + 4*y
resultados = mult_lagrange(f, g, [x,y])
resultados
```




    [{lambda: -sqrt(82)/6, x: 1/4 - 3*sqrt(82)/41, y: -1/2 - 9*sqrt(82)/328},
     {lambda: sqrt(82)/6, x: 1/4 + 3*sqrt(82)/41, y: -1/2 + 9*sqrt(82)/328}]


