### Dropout

En una red neuronal, cada neurona ajusta sus pesos para reducir una función de costo considerando el comportamiento del resto. Esto permite que cada neurona modifique su funcionamiento para corregir los errores de otras, dando lugar a complejas **co-adaptaciones**.

Este mecanismo puede generar sobreajuste, ya que las neuronas aprenden a depender unas de otras de manera muy específica y desarrollan co-adaptaciones que no generalizan bien a datos nuevos. En lugar de aprender representaciones robustas, la red se ajusta excesivamente a las peculiaridades del conjunto de entrenamiento, lo que reduce su capacidad de rendimiento en situaciones no vistas.

Una técnica utilizada para mitigar este problema es el **dropout**. El dropout consiste en desactivar aleatoriamente un conjunto de neuronas en cada iteración, obligando a las unidades a no depender de combinaciones específicas con otras neuronas. Esto promueve representaciones más independientes y robustas que generalizan mejor a nuevos datos.

Supongamos que tenemos una capa de $n$ neuronas la cual produce señales $X_1, X_2, ..., X_n$ de activación. Podemos modelar la no activación de una neurona de esta capa, mediante una variable de Bernoulli $M_{\mu}$ enmascarando a cada activación $X_{\mu}$ con una probabilidad $p$. La realización de una mascara para una muestra $\omega$ puede tomar solo dos valores:

$$
M_{\mu}(\omega) = \begin{cases} 0 \text{ con probabilidad } p \\  1 \text{ con probabilidad } 1-p \end{cases} \qquad \mu = 1, 2, ..., n
$$

En donde $\omega$ es una muestra cualquiera, $M_{\mu}(\omega) = 0$ indicando que la neurona no se activo y $M_{\mu} = 1$ indicando que si. Como cada mascara es una variable aleatoria independiente e idénticamente distribuida, su suma, es una nueva variable aleatoria $N$ dada por:

$$
N = \sum_{\mu = 1}^n M_{\mu}
$$

Y su realización nos indica el numero de unidades activadas en la red. Esta nueva variable sigue una distribución binomial:

$$
N \sim \text{Binomial}(n, p)
$$

Y una misma muestra $\omega$ puede generar hasta $2^n$ configuraciones diferentes, por lo que el modelo puede considerarse como un ensamble estadístico con un numero variable de unidades, al cual denominaremos **ensamble gran canónico**. 

El hecho de que el numero de unidades sea variable en la capa de neuronas, tiene implicancias en su energía libre e impone una nueva restricción en la optimización de su entropía. Esto impide que se puedan utilizar las funciones de activación usuales para ensambles canónicos, lo que limita la utilización del dropout a las capas internas de un modelo.

Dicho esto, consideramos una capa posterior de $d$ neuronas conectada cuyos potenciales de activación son producto de las contribuciones de cada señal producida por la capa con dropout. Las señales producidas son enmascaradas durante la fase de entrenamiento de la red, de modo que estas contribuciones estarán dadas por el producto de variables aleatorias:

$$
M_{\mu} X_{\mu} \qquad \mu = 1,2, ..., n
$$

La realización de estos productos será igual la realización de la señal cuando la neurona se active y nula de lo contrario, es decir:

$$
(X_{\mu}M_{\mu} )(\omega) = \begin{cases} 0 \text{ con probabilidad } p \\ X_{\mu}(\omega) \text{ con probabilidad } 1- p \end{cases} \qquad \mu = 1, 2, ..,n
$$
  
Si $Z_1, ..., Z_d$ son los potenciales de activación de la capa siguiente, durante el entrenamiento, los potenciales estarán dados por:

$$
Z_{\nu} = \sum_{\mu=1}^n (X_{\mu}M_{\mu} ) w^{\mu}{}_{\nu} \qquad \nu = 1, 2, ..., d
$$

Con $w^{\mu}{}_{\nu}$ los pesos de la red. Podemos hallar la energía interna de la segunda capa como la esperanza de $Z$:

$$
\text{U}[Z] = \sum_{\nu=1}^d \sum_{\mu=1}^n \text{E}[X_{\mu}M_{\mu} ] w^{\mu}{}_{\nu} = \sum_{\nu=1}^d \sum_{\mu=1}^n \text{E}[M_{\mu}] \text{E}[X_{\mu}] w^{\mu}{}_{\nu} = (1-p) \sum_{\nu=1}^d \sum_{\mu=1}^n \text{E}[X_{\mu}] w^{\mu}{}_{\nu}
$$

$$
\text{U}[Z] = (1-p) U
$$

En donde $U$ es la energía interna de la capa sin dropout. Como el dropout se aplica solo en la fase de entrenamiento del modelo y no en la fase de inferencia, la diferencia en la energía interna implica que el modelo generara distribuciones diferentes en cada fase. 

Esta discrepancia puede ser resuelta simplemente re-escalando los vectores de características con un factor $1/(1-p)$, de esta manera, se asegura que el valor esperado de la energía interna permanezca constante entre ambas fases, manteniendo la coherencia estadística del modelo.

$$
\text{Dropout}[X] = \begin{cases} \frac{1}{1-p} M \odot X \text{ durante el entrenamiento} \\ \qquad X \qquad \text{ durante la inferencia} \end{cases}
$$

En donde $\odot$ es el producto de Hamadard.