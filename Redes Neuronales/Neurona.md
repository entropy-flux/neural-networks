El componente más básico de una red neuronal artificial es la **neurona**, inspirada en las neuronas biológicas, esta recibe señales eléctricas a través de sus **dendritas**, que la conectan con otras neuronas. El mecanismo por el cual llegan estas señales se denomina **sinapsis**. 

Una sinapsis es una conexión especializada entre neuronas, en la cual se transporta eléctrica energía o química mediante sustancias denominadas **neurotransmisores**. La señales se integran en la neurona mediante un proceso que modelaremos como una **agregación ponderada**.

Cada neurona tiene un mecanismo que determina si la neurona se activa. Si una neurona se activa, esta genera un impulso eléctrico denominado **activación**, que viaja a través del **axón**, una larga extensión encargada de transmitir la señal hacia las **dendritas** de otras neuronas. 

![](assets/20250425233804.png)

El proceso de integración de señales a la cual denominaremos simplemente como agregación, y la posterior activación de la neurona pueden verse como dos etapas contiguas en el procesamiento de información dentro de la neurona, de modo que durante la activación son conocidas las realizaciones de la **preactivación**.

### Agregación.

Matemáticamente, una señal puede representarse mediante una variable $X: \Omega \rightarrow \mathcal{X}$ , donde $\Omega$ denota el conjunto de configuraciones. A cada configuración $\omega \in \Omega$ le corresponde una realización específica de la señal $x = X(\omega)$ correspondiente a una característica.  

Durante la fase de agregación, un conjunto $X_1, X_2,..., X_l$ de señales se integran en la neurona. Podemos introducir una función de energía $Z: \mathcal{X}^d \rightarrow \mathbb{R}$ para describir al potencial de la neurona durante la fase de agregación como:

$$
Z(x_1,...,x_l) = z \in \mathbb{R}
$$

De modo que si las señales son ponderadas por pesos $w^1, w^2, ..., w^d$  los cuales podemos interpretar como coordenadas de un espacio. Este potencial puede escribirse como:

$$
z = \sum_{\mu=1}^d x_{\mu} w^{\mu} + z_0
$$

En donde el termino $z_0$ corresponde a un parámetro que representa al potencial en reposo de la neurona.   El espacio producto $\mathcal{X}^d$ se conoce como espacio de características y sus elementos:

$$\mathbf{x} = \begin{bmatrix} x_1 & x_2 & \cdots & x_d\end{bmatrix} \in \mathcal{X}^d$$ 
Son conocidos como **vectores de características**. 

### Activación
 
Podemos pensar en la activación de una neurona como un evento binario, que podemos representar con una variable $A: \Omega \rightarrow \{0, 1\}$ en donde $A(\omega) = 1$ indica que la neurona se activó y $A(\omega) = 0$ indica inactividad.  

El contenido de información de un estado $a \in \mathcal\{0,1\}$ condicionado por un estado de preactivación $z$ se puede cuantificar mediante la información condicional:

$$
S_{A|Z}(a|z) = -\log \rho_{A|Z}(a|z)
$$

En donde $\rho_{A|Z}$ es la probabilidad de activación condicionada por el potencial $z$. Esta probabilidad debe cumplir la condición de normalización:

$$
\sum_{a =0,1} \rho_{A|Z}(a|z) = \rho_{A|Z}(0|z) + \rho_{A|Z}(1|z) = 1
$$

El valor esperado del contenido de información de la activación $S_{A|Z}$ es la entropía condicional, y la podemos expresar como el funcional:

$$
\text{S}[A|z] = \sum_{a=0,1} \rho_{A|Z}(a|z) S_{A|Z}(a|z) = -\sum_{a=0,1}\rho_{A|Z}(a|z) \log \rho_{A|Z}(1|z)
$$

Esta expresión puede simplificarse, denotando la probabilidad de activación simplemente como $\sigma$, de modo que podemos escribir las probabilidades de ambos estados como:

$$
\rho_{A|Z}(1|z) = \sigma(z) \qquad \rho_{A|Z}(0|z) = 1- \sigma(z)
$$

De modo que la entropía de la neurona puede expresarse en términos de la probabilidad $\sigma$ como:

$$
\text{S}[A|z] = -(1-\sigma(z)) \log(1-\sigma(z)) - \sigma(z)\log\sigma(z)
$$

El principio de máxima entropía nos dice que, la función de probabilidad que mejor representa el estado de activación de la neurona, teniendo en cuenta las restricciones impuestas sobre esta, es aquella que maximiza la información esperada para describirla. Sin restricciones, podemos hallar este máximo mediante el calculo de una variación en la entropía:

$$
\delta \text{S}[A|z] = -\big[\log\sigma(z) - \log(1-\sigma(z)) \big]\delta\sigma = -\log \left[\frac{\sigma(z)}{1-\sigma(z)} \right] \delta\sigma
$$

En donde $\delta \text{S}[A|z]$ representa una variación de la entropía dada una variación $\delta \sigma$. Para una entropía máxima, la variación se anula, por lo que la función de probabilidad $\sigma$ verifica que:

$$
\log \left[\frac{\sigma(z)}{1-\sigma(z)} \right] = 0 \Rightarrow \sigma(z) = \frac{1}{2}
$$

Esto nos dice que sin restricciones, ambos estados son equiprobables. Si bien esta función de probabilidad maximiza la información esperada, la *información útil* que puede ser utilizada para realizar una decisión es nula, y deja a la neurona en un estado de *indecisión absoluta*, por lo que es necesario considerar los intercambios de energía de la neurona con el medio como restricción.

Sea $U_{A|Z}(a|z)$ la energía interna del sistema para un estado de activación $a$ condicionado por un potencial $z$. Podemos escribir su valor esperado y una variación de este ultimo en términos de una variación de la probabilidad como:

$$
\text{U}[A|z] = \sum_{a=0,1} \rho_{A|Z}(a|z) U_{A|Z}(a|z) = (1 - \sigma(z))U_{A|Z}(0|z) + \sigma(z) U_{A|Z}(1|z)
$$
 
$$
\delta \text{U[A|z]} = \big[ U_{A|Z}(1|z) - U_{A|Z}(0|z) \big] \delta \sigma \equiv \Delta U_{A|Z}(z) \delta \sigma
$$

La entropía se relaciona con la energía mediante un parámetro intensivo $\beta$ tal que:

$$
dS_{A|Z} = \beta dU_{A|B}
$$

Este parámetro impone una restricción sobre la entropía y nos permite definir a la información útil o **entropía libre**, como la diferencia entre la información esperada, menos un termino proporcional a la energía, y cuyo valor esperado viene dado:

$$
\text{L}[A|z] = \text{S}[A|z] - \beta \text{U}[A|z] 
$$

De esta forma, maximizando el valor esperado de la información útil, se halla la función de probabilidad $\sigma$ que optimiza el nivel de decisión. Una variación de la información libre puede escribirse simplemente como:

$$
\delta \text{L}[A|z] = \delta \text{S}[A|z] + \beta \delta \text{U}[A|z]  = 
-\log \left[\frac{\sigma(z)}{1-\sigma(z)} \right] \delta\sigma - \beta \Delta U_{A|Z}(z) \delta \sigma
$$

Luego, el valor esperado de la información libre se maximiza si, la variación se anula, por lo que la función de probabilidad $\sigma$ que anula la variación verifica que:

$$
\log \left[\frac{\sigma(z)}{1-\sigma(z)} \right] = -\beta \Delta U_{A|Z}(z)
$$

$$
\Rightarrow \sigma(z) = \big[ 1-\sigma(z) \big] \exp \big[ -\beta \Delta U_{A|Z}(z) \big] = \frac{\exp \big[ -\beta \Delta U_{A|Z}(z) \big]}{1 + \exp \big[ -\beta \Delta U_{A|Z}(z) \big]}
$$

Al activarse, la neurona transmite una señal liberando una energía igual al potencial alcanzado durante la fase de agregación, de modo que esta vuelve al estado de reposo que tenia antes de integrar las señales. En el caso de no activarse, el sistema absorbe la señal aumentando la energía interna en una cantidad igual al potencial alcanzado por la neurona, de modo que la diferencia entre la energía interna entre ambos estados para una neurona simplemente será: 

$$
\Delta U_{A|Z}(z) = U_{A|Z}(1|z) - U_{A|Z}(0|z) = -z
$$

Finalmente la probabilidad de activación de una neurona dado un potencial de $z$ alcanzado durante la fase de agregación será la conocida función sigmoidea:  

$$
\sigma(z) = \frac{1}{1+\exp(-\beta z)} \equiv \text{Sigmoid}(\beta z)
$$

En donde $\beta$ puede ser considerado un hiperparametro que determina qué tan abrupta o suave es la transición de la función sigmoide entre los estados. Desde una perspectiva termodinámica, $\beta$ puede interpretarse como el inverso de una **temperatura** $T$ del sistema:

$$
\beta \sim \frac{1}{T}
$$

De modo que para $T \rightarrow \infty$ ambos estados tienen a ser igual de probables y la decisión tiende a ser **aleatoria** e impredecible. Por el contrario para $T \rightarrow 0$ se favorece fuertemente uno de los estados y la decisión tiende a ser **determinista** y predecible.