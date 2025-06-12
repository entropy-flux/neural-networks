El concepto de energía proporciona una forma de estructurar una distribución de probabilidad sobre un espacio de configuraciones posibles, asignando a cada estado una medida escalar que puede interpretarse como un costo o preferencia. Dada una variable aleatoria $X: \Omega \rightarrow \mathcal{X}$  podemos asociarle a esta, una **función de energía**:

$$
E: \mathcal{X} \rightarrow \mathbb{R}
$$

Tal que $E$ asigna a cada posible realización $x \in \mathcal{X}$ un valor escalar $E(x)$, interpretado como la **energía** asociada a dicho estado. 

Notemos que esta definición funciona tanto como para una variable aleatoria individual, definida sobre los reales, como para una variable definida por otras $X_1, X_2, ..., X_n$, sobre un espacio conjunto $\mathcal{X}_1 \times \cdots \times \mathcal{X}_n$. De esta forma la energía puede depender de las interacciones entre variables y permite modelar preferencias que reflejen relaciones o restricciones entre variables.

Por otra parte es necesario también definir la energía condicional. Dadas dos variables aleatorias $X: \Omega \rightarrow \mathcal{X}$  e $Y: \Omega \rightarrow \mathcal{Y}$ podemos definir una función de energía condicional como:

$$
E(x|y): \mathcal{X} \times \mathcal{Y} \rightarrow \mathbb{R}
$$

Donde para cada valor de $y \in \mathcal{Y}$ la función $x \mapsto E(x|y)$ asigna una función de energía a cada posible valor de $x$ condicionado por $y$. 