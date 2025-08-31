El concepto de **información propia** se deriva de la probabilidad de ocurrencia de un evento particular determinado por una variable aleatoria, y cuantifica la **incertidumbre** asociada a dicho evento. Su valor puede definirse de forma tal que cumpla con los siguientes axiomas:

- Un evento con probabilidad $1$ tiene incertidumbre nula y no aporta información relevante.
    
- Cuanto menos probable es un evento, mayor es su incertidumbre y más información aporta.
    
- Si dos eventos independientes se observan por separado, la cantidad total de información es la suma de las informaciones propias de estos eventos individuales.
    

De esta forma, dada una variable aleatoria $X: \Omega \rightarrow \mathcal{X}$, se puede estimar el contenido de información de una ocurrencia $x \in \mathcal{X}$ como:

$$
S_X(x) = -\log \rho_X(x)
$$

donde $\rho_X: \mathcal{X} \rightarrow [0, 1]$ es la función de masa de probabilidad de la variable $X$. Cuando se dispone de información adicional proveniente de otra variable aleatoria $Y$, se puede considerar la **información condicional**. Esta cuantifica la incertidumbre de un evento $x \in \mathcal{X}$ dado que se ha observado un evento $y \in \mathcal{Y}$ asociado a otra variable aleatoria $Y$. La información condicional se define como:

$$
S_{X|Y}(x|y) = -\log\rho_{X|Y}(x|y)
$$
donde $\rho_{X|Y}(x|y)$ es la función de masa o probabilidad condicional condicional. Este valor representa la información que aporta la observación de $x$ cuando ya se conoce $y$, y permite refinar la estimación de incertidumbre al incorporar conocimiento contextual o dependencias estadísticas entre variables.

El valor esperado de la incerteza de una variable aleatoria se conoce como **entropía** y cuantifica la cantidad esperada de información necesaria para describir el estado de una variable. La entropía puede escribirse como el funcional: 

$$
\text{S}[X] = -\sum_{\mathcal{x \in \mathcal X}} \rho_X(x) \log \rho_X(x)
$$

Si consideramos dos variables aleatorias $X$ e $Y$ entonces es posible cuantificar la incertidumbre sobre sus posibles valores simultáneos mediante la entropía conjunta. Esta magnitud mide la cantidad total de información requerida para describir el par $(X, Y$) y se define como:

$$
\text{S}[X,Y] =- \sum_{x\in\mathcal{X}} \sum_{y\in\mathcal{Y}} \rho_{X,Y}(x,y) \log\rho_{X,Y}(x,y) 
$$

En donde $\rho_{X,Y}$ es la distribución conjunta de probabilidad. La **entropía conjunta** generaliza la entropía univariada al contexto de múltiples variables, permitiendo capturar tanto la incertidumbre combinada como las relaciones de dependencia o independencia entre ellas. Si las variables $X$ y $Y$ son independientes, se cumple la siguiente propiedad:

$$
\text{S}[X,Y] = \text{S}[X] + \text{S}[Y]
$$

Esta expresión está en concordancia con el tercer axioma previamente mencionado. Una extensión natural del concepto de entropía conjunta es la **entropía condicional**, que mide la incertidumbre restante de una variable $Y$ dado el conocimiento de la variable $X$. La cual se puede escribir como:

$$
\text{S}[X|Y] = \text{S}[X,Y] - \text{S}[Y] = -\sum_{y\in \mathcal{Y}} \rho_Y(y) \sum_{x\in \mathcal{X}} \rho_{X|Y}(x,y) \log\rho_{X|Y}(x,y)
$$

**El principio de máxima entropía** establece que, partiendo de datos previos debidamente concretados, la distribución de probabilidad que mejor representa el estado de conocimiento actual de un sistema es aquella que maximiza la entropía.