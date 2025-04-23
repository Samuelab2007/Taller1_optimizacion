>NOTA: Cabe resaltar que los resultados de los notebooks adjuntos solo están actualizados para la parte relevante al punto que resuelven. Ejemplo: Si es un problema de minimización, solo lo relacionado a minimización está actualizado en los resultados.
## Punto 1

Para la función $f(x)=4x+3y$ con la restricción $g(x)=2x^{2}+4y^{2}-x+4y$

Ya se realizó previamente una implementación del método de multiplicadores de lagrange. Por lo tanto se procede a adjuntar los resultados obtenidos para este punto concreto.

Puntos críticos: $(\frac{1}{4} - \frac{3\sqrt(82)}{41}, -\frac{1}{2} - \frac{9\sqrt(82)}{328})$, $(\frac{1}{4} + \frac{3\sqrt(82)}{41}, -\frac{1}{2} + \frac{9\sqrt(82)}{328})$

O en valores decimales: $(-0.41258, -0.74847)$, $(0.91258, -0.25152)$

[Resultados notebook](Multiplicadores_Lagrange)

Gráfico de la intersección de la restricción con la superficie:

![[Pasted image 20250422215939.png]]

## Punto 2

Teniendo en cuenta la función $f(x)=x^{10}-3$

- Localizar la raíz con los métodos de falsa posición y bisección, comparar desempeño.
	Considerando la forma de la función vamos a escoger el intervalo inicial $[0,4]$, con una presición de $0.0001$ y máximo 100 iteraciones.

	Con el método de la bisección obtenemos los siguientes resultados:
	$x=1.1161231994628906$, $\text{iteraciones}=20$, $\text{precision}=0.0001$
	Link a la ejecución del notebook:[resultados_notebook](metodo_biseccion_2.md)
	
	Con el método de la falsa posición obtenemos los siguientes resultados:
	$x=1.1161194537476447$, $\text{iteraciones}=251045$, $\text{precision}=0.0001$
	Link a la ejecución del notebook:[resultados_notebook](metodo_falsa_posicion_2.md)

 - Raíz con el método de Newton Raphson con valor inicial $x=0.8$
	Se escogió ejecutar el método con la misma precisión y cantidad de iteraciones máximas que los anteriores.
	Obteniendo los siguientes resultados:
	$x=1.11612317423391$, $\text{iteraciones}=14$, $\text{precision}=0.0001$
	[Link a la ejecución del notebook](metodo_newton-raphson_2)

### Conclusiones
Los tres métodos utilizados llegan al mismo resultado con la misma precisión, la única diferencia entre ellos es la velocidad con la que lo alcanzan. Para este caso concreto el método más rápido es el método de Newton-Raphson. El cual llega a la respuesta en 14 iteraciones, 6 menos que los otros dos métodos.

El pero método es el método de la falsa posición, el cual tiene un alto costo computacional, requiriendo 251045 iteraciones para igualar a los demás métodos. Pero en este caso podemos observar que el error se comporta similar a una sigmoide, en la cual el error disminuye de manera rápida pasada una cantidad grande de iteraciones.

La manera en la que se calcula el error en los métodos es ligeramente diferente, pero los tres presentan una curva de error descendente y con tendencias logarítmicas en su decrecimiento, caracterizado por mejoras iniciales bruscas que luego se van haciendo más sutiles.

## Punto 3

Función continua y derivable: $f(x)=x^{2}+2x-9$

Aplicar todos los métodos necesarios para hallar: Máximo o mínimo de la función.

En este caso la función sólo tiene un mínimo, el cual es global.
Los métodos que aplican a este caso son el método de la interpolación cuadrática y el método de Newton.

### Interpolacion cuadrática

Utilizando interpolación cuadrática, con puntos iniciales: $x_0=-4$, $x_1=0$ y $x_2=2$, con una precisión de 0.0001 y un máximo de 1000 iteraciones.

Resultados: $x=-1.0$, $\text{iteraciones}=2$, $error=0$
[Resultados notebook](metodo_interpolacion_cuadratica_3.md)

### Método de Newton

Utilizando el método de Newton solo es necesario definir un valor inicial de x.

Utilizando el método con los siguientes valores: $x=-4$, $\text{precision}=0.0001$ $\text{maxiter}=100$

Nos genera los siguientes resultados: $x=-1.0$, $\text{iteraciones}=1$
[Resultados notebook](metodo_newton-raphson_3)

### Conclusiones

Se concluye que aunque ambos métodos resultan veloces y efectivos para la función que hemos escogido. Si se tuviera que escoger un método para resolverlo, este sería el método de Newton. Ya que es más sencillo de utilizar al solo requerir un punto inicial, y en este tipo de funciones hay un único valor crítico, por lo que no corremos el riesgo de ignorar un mínimo global.

## Punto 4

Tenga en cuenta la siguiente función: $f(x)=-1.5x^{6}-2x^{4}+12x$
Hallar el máximo de la función con todos los métodos. Al usar razón dorada use los puntos 0 y 2 como puntos de partida.

### Razón dorada

Al ejecutar el método de la razón dorada, con el objetivo de maximizar la función y los puntos de partida definidos anteriormente se obtienen los siguientes resultados:

$x=0.9169222533760356$, $\text{iteraciones}=19$, $\text{error}=0.000082$

[Resultados notebook](metodo_razon_dorada_4.md)

### Metodo Newton-Raphson

Se ejecuta el método de Newton con ambos puntos de partida. Con $x=0$ y con $x=2$

Para $x_{inicial}=-0.5$ los resultados son los siguientes:
$x=0.916915282744097$, $\text{iteraciones}=4$
[Resultados notebook](metodo_newton_4.1)

Para $x_{inicial}=2$ los resultados son los siguientes:
$x=0.91691696764598$, $\text{iteraciones}=6$
[Resultados notebook](metodo_newton_4.2)

### Método interpolación cuadrática

Se ejecuta el método de interpolación cuadrática con puntos: $x_0=0$, $x_1=1$ y $x_2=2$. 
Con los siguientes resultados: $x=0.9165337326776142$, $\text{iteraciones}=32$

[Resultados notebook](metodo_interpolacion_cuadratica_4)

### Método búsqueda aleatoria

Se utiliza con los siguientes puntos intervalos: $x \in [-1,2]$, $y \in [-2,14]$.

Con los siguientes resultados:
$x_{max}=0.8836865511641818$, $y_{max}=8.046328272875636$, $best_f=8.670322859573817$.

Él método de búsqueda aleatoria siempre genera mucho desperdicio de cómputo, ya que al ser aleatorio la mejora de un resultado depende del azar.

## Punto 5
$$f(x)=x^{3}+2x^{2}-4x+5$$
Encuentre los diferentes métodos para encontrar la raíz de la función que está en $x=2$ pero:
- Parta de $x_0=1.2$ con Newton-Raphson y compare con los demás métodos con puntos cercanos al indicado.

Todos los métodos utilizados tienen una tolerancia de error de 0.0001.

Los métodos que se pueden utilizar para hallar una raíz son los siguientes: 

### Newton-raphson

Partiendo de $x_0=1.2$ y un valor de tolerancia de error de $0.0001$ se obtienen los siguientes resultados.
$x=-3.53284246653277$, $\text{iteraciones}=30$

También visualizando la gráfica de error podemos observar que la función tiende a oscilar en su recorrido al buscar la raíz, los valores de $x_i$ que se van usando en las iteraciones van avanzan en dirección de la raíz, pero también retroceden un poco cada vez que lo hacen, lo que genera que el error se disminuya en un patrón oscilatorio.

[Resultados notebook](metodo_newton-raphson_5)

### Falsa posición

Tomando como intervalo $[-5, 2]$, se obtienen los siguientes resultados:
$x=-3.5328380821489147$, $\text{iteraciones}=22$

El error del método incrementa a cada iteración(a medida que escala la curva de la función) y luego empieza a disminuir a medida que se acerca a la raíz.

[Resultados notebook](metodo_falsa_posicion_5)

### Bisección

Tomando como intervalo $[-5, 2]$, se obtienen los siguientes resultados:
$x=-3.532843589782715$, $\text{iteraciones}=19$

El error del método disminuye de manera rápida y repentina y luego no progresa en demasía.

[Resultados notebook](metodo_biseccion_5)

### Conclusiones

Sí se definen bien los intervalos donde se busca encontrar la raíz la diferencia entre los métodos no es tan notoria. Pero para eso es necesario conocer de antemano la naturaleza y la forma de la función, por lo que el método más fiable es el método de Newton-Raphson. Ya que todos llegan a un mismo resultado, pero a pesar de ser menos veloz que los otros en este caso, se hace más simple de utilizar.

Si se conoce la forma de la función el mejor método en este caso es el de la bisección.


## Punto 6

Para la función $f(x)=\tanh(x^{2}-9)$
Vamos a hallar la raíz que se encuentra en $x=3$.

### Bisección

Utilizando el intervalo $[0,4]$
Obtenemos como resultado: $x=3.0$, $iteraciones=2$

[Resultados notebook](metodo_biseccion_6)

### Falsa posición

Utilizando el intervalo $[0,4]$
Resultados: $x=2.9999999842532$, $iteraciones=4$.

[Resultados notebook](metodo_falsa_posicion_6)

### Newton-Raphson

Partiendo de $x_0=3.2$. El método colapsa y no permite calcular la raíz.
## Punto 7

Minimizar la función $f(x)=3+6x+5x^{2}+3x^{3}+4x^{4}$

Utilizando bisección en el intervalo $[-2,1]$
Resultados: No existe raíz en el intervalo dado. Además, el método de la bisección no sirve para minimizar.

Utilizando método de newton obtenemos $x=-0.587171693699002$, $iteraciones=3$.

Ahora, pongamos una tolerancia de error más severa. En este caso 0.0001. Que da los siguientes resultados: $x=-0.586682696192003$, $iteraciones=7$

El comportamiento es esperado, ya que al buscar mayor precisión se necesita realizar más iteraciones con cambios más pequeños que se acerquen al punto buscado.
## Punto 8

Minimizar: $f(x)=e^{x}-2x$
### Método de newton

Partiendo de $x=2$ obtenemos:

$x=0.693189402250512$, $iteraciones=4$

[Resultados notebook](metodo_newton_8)
### Método de interpolación cuadrática

Partiendo de $x_0=0$, $x_1=1$ y $x_2=2$

Nos da como resultado para el punto mínimo: $x=0.6931436053634965$, $iteraciones=6$

[Resultados notebook](metodo_interpolacion_cuadratica_8)

### Conclusiones

Ambos métodos dan resultados adecuados, pero el método de Newton es ligeramente más rápido en este caso concreto.
## Punto 9

Para la función $f(x,y)=4x+2y+x^{2}-2x^{4}+2xy-3y^{2}$ se calcula el máximo en el rango $x\in[-2,2]$, $y\in[-2,2]$.

El resultado obtenido es el punto $(0.9097306424260503, 0.9097306424260503, 4.088507754170767)$

Siendo $x=0.9097306424260503$, $y=0.9097306424260503$, $z=4.088507754170767$

[Proceso y resultados](metodo_busqueda_aleatoria_9.md)
