
Las neuronas pueden aglomerarse en **capas** y procesar un conjunto de señales en paralelo. 
### Agregación

Dado un conjunto de señales $X_1, X_2, ..., X_d$ una capa de $n$ neuronas integrarlas en paralelo produciendo señales nuevas señales $Y_{\nu}$ para cada neurona $\nu=1,2,...,n$ de la forma:

$$
Y_{\nu} = \sum_{\mu=1}^d X_{\mu} w^{\mu}{}_{\nu}
$$

En donde $w^{1}{}_{\nu}, w^{2}{}_{\nu}, ...w^{n}{}_{\nu}$ son los pesos sinápticos de la neurona $\nu$.  
## Activación

Para una capa de $d$ neuronas, debemos considerar un estado de activación conjunto $A$ que condicionado no solo por el potencial $Z$ sino también por otra variable a la cual denotamos $N$ y que nos indica el numero de neuronas que se activaron.

Si restringimos la variable $N$ al tomar solo el valor $N(\omega) = 1$, es decir, si permitimos que solo una neurona de la capa se active, entonces la capa llevará a cabo una decisión $d$-aria basada en el potencial de activación $Z$ como evidencia. 

Podemos expresar la entropía de la capa simplemente como:

$$
\text{S}[A|\mathbf{z}] = -\sum_{\nu = 1}^d \rho_{A|Z}(a_{\nu}|\mathbf{z}) \log \rho_{A|Z}(a_{\nu}|\mathbf{z})
$$

En donde $\mathbf{z}$ indica el potencial de activación de la capa y $\rho_{A|Z}(a_{\nu}|\mathbf{z})$ es la probabilidad de que la neurona $\nu$ se active y que las otras queden inactivas. 

La restricción impuesta sobre $N$ nos indica que exactamente una de las neuronas se activara durante la fase de activación, por lo que las probabilidades asociadas a cada estado de la capa deben sumar uno, esta restricción puede escribirse como:

$$
\sum_{\nu=1}^d \rho_{A|Z}(a_{\nu}|\mathbf{z}) = 1
$$

Por otra parte el valor esperado de la energía interna de la capa requiere un análisis semejante al realizado para una neurona individual. Para cada neurona $\nu = 1,...,d$ debemos considerar el caso en el que esta se activa y no contribuye a la energía interna de la capa con probabilidad $\rho_{A|Z}(a_{\nu}|\mathbf{z})$, mas los otros $d-1$ casos en los que no se activa y contribuye con una energía $z_{\nu}$ con probabilidades $\rho_{A|Z}(a_{\lambda}|\mathbf{z})$ de que la neurona $\lambda \neq \nu$ se active, es decir:

$$
\rho_{A|Z}(a_{\nu}|\mathbf{z}) \cdot 0 + \sum_{\lambda \neq \nu} \rho_{A|Z}(a_{\lambda}|\mathbf{z}) z_{\nu} = z_{\nu}(1-\rho_{A|Z}(a_{\nu}|\mathbf{z}) )
$$

Sumando esta misma contribución para cada neurona se obtiene el valor esperado de la energía interna de la capa como:

$$
\text{U}[A|Z] = \sum_{\nu = 1}^d z_{\nu}(1-\rho_{A|Z}(a_{\nu}|\mathbf{z}) )
$$


Buscamos ahora hallar las funciones $\sigma_{\nu}$ que mejor describan las probabilidades de la capa de entrar en un estado de activación $a_{\nu}$ condicionadas por el potencial $Z$. Es decir: 

$$
\sigma_{\nu}(\mathbf{z}) = \rho_{A|Z}(a_{\nu}|\mathbf{z}) \qquad \nu=1,2,...,d
$$
 
Siguiendo el principio de la entropía máxima, debemos maximizar la información libre, teniendo en cuenta las restricciones impuestas

$$
\text{L}[A|\mathbf{z}] = \text{S}[A|\mathbf{z}] - \beta
\text{U}[A|\mathbf{z}]
$$

Esto puede ser logrado utilizando un multiplicador de Lagrange $\alpha$ asociado a la restricción de normalización de modo que una variación de la entropía libre puede escribirse como:

$$
\delta \text{L} [A|\mathbf{z}] = \delta \text{S}[A|\mathbf{z}] - \beta \delta \text{U}[A|\mathbf z] + \alpha \delta \left(1 - \sum_{\nu=1}^d \sigma_{\nu}(\mathbf{z}) \right) 
$$

En donde variaciones de la entropía y la energía debido a variaciones $\delta\sigma_{\nu}$ puede hallarse mediante la derivada variacional y se obtiene que:

$$
\delta \text{S}[A|\mathbf{z}] = -\sum_{\nu=1}^d ( \log \sigma_{\nu}(\mathbf{z}) + 1) \delta \sigma_{\nu}(\mathbf{z})
$$
$$
\delta\text{U}[A|\mathbf{z}] = -\sum_{\nu=1}^d z_{\nu} \delta\sigma_{\nu}(\mathbf{z}) 
$$

Reemplazando, las funciones $\sigma_{\nu}$ que mejor describen es estado de activación de la capa serán aquellas que verifiquen la ecuación:

$$
\delta \text{L}[A|\mathbf{z}] = \sum_{\nu = 1} ^d \delta\sigma_{\nu}(\mathbf{z}) \big[1 -\log \sigma_{\nu}(\mathbf{z}) + \beta z_{\nu} + \alpha \big] = 0 
$$

Si cada sumando se anula, podemos obtener una expresar $\sigma_{\nu}$ como:

$$ 
\sigma_{\nu}(\mathbf{z}) = \exp (\beta z_{\nu} + \alpha - 1) = \exp (\beta z_{\nu}) \exp(\alpha - 1)
$$

Se puede remover $\alpha$ de la expresión sumando sobre todas las neuronas de la capa y usando la condición de normalización, de modo que:

$$ 
\exp(1-\alpha) = \sum_{\lambda = 1}^d \exp(\beta z_{\lambda}) 
$$

Finalmente la probabilidad de que la neurona $\mu$ se active estará dada por la conocida función $\text{Softmax}$:

$$
\sigma_{\nu}(\mathbf{z}) = \frac{\exp(\beta z_{\nu})}{ \sum_{\lambda=1}^d \exp(\beta z_{\lambda})} \equiv \text{Softmax}(\beta z_{\nu})
$$

En donde nuevamente $\beta$ puede es un hiperparametro que determina qué tan abrupta o suave es la transición de la función sigmoide entre los estados relacionado con la temperatura como:

$$
\beta \sim \frac{1}{T}
$$

De modo que para $T \rightarrow \infty$ todos los estados tienen a ser igual de probables y la decisión tiende a ser impredecible, por el contrario para $T \rightarrow 0$ la capa se vuelve determinista. 