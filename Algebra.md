
El objetivo de esta sección no es redefinir los conceptos de álgebra lineal, sino establecer la notación y aclarar algunos conceptos no triviales que se utilizarán a lo largo del texto.

### Vectores

Dado un cuerpo $\mathbb{K}$ (por ejemplo, $\mathbb{R}$ o $\mathbb{C}$), consideraremos por el momento únicamente los vectores que son elementos de un espacio vectorial $\mathbb{K}^n$, a los cuales podemos representar usando en la base canónica $\{ \vec{e}_1,...,\vec{e}_n \}$ de $\mathbb{K}^n$ como:

$$
\vec{v} = \sum_{\mu=0} v^{\mu} \vec{e}_{\mu} = \begin{bmatrix} v^1 \\ v^2 \\ \vdots \\ v^n \end{bmatrix} \quad \text{con } v^{\mu} \in \mathbb{K} 
$$

Los índices **superiores** indican que estamos ante coordenadas **contravariantes**, y nos referimos a estos vectores como **vectores columna**.

El conjunto de todas las aplicaciones lineales $f: \mathbb{K}^n \rightarrow \mathbb{K}$ se denomina el espacio **dual** de $\mathbb{K}^n$ y se denota por $\left(\mathbb{K}^n\right)^*$. Sus elementos se denominan **covectores** y pueden representarse en la base canonica $\{ \vec{e}^1,...,\vec{e}^n \}$ de $(\mathbb{K}^n)^*$ como:

$$
\vec{\omega} = \sum_{{\mu}=0} \omega_{\mu} \vec{e}^{\mu} = \begin{bmatrix} \omega_1 & \omega_2 & \cdots & \omega_n \end{bmatrix} \quad \text{con } \omega_{\mu} \in \mathbb{K}^* 
$$

Los índices **inferiores** indican una transformación **covariante**, y nos referimos a estos como **vectores fila**. Sabemos que el resultado de aplicar los elementos de la base covariante a los de la base contravariante es la delta de Kronecker. 

$$
\vec{e}^{\mu}(\vec{e}_{\nu}) = \delta^{\mu}{}_{\nu} = \begin{cases} 1 \text{ para } \mu = \nu \\ 0 \text{ para } \mu \ne \nu \end{cases}
$$

Teniendo en cuenta esto, el resultado de evaluar un covector $\vec{\omega}$ sobre un vector $\vec{v}$ es:

$$
\vec{\omega}(\vec{v}) = \begin{bmatrix} \omega_1 & \omega_2 & \cdots & \omega_n \end{bmatrix} \begin{bmatrix} v^1 \\ v^2 \\ \vdots \\ v^n \end{bmatrix} = \sum_{\mu,\nu=1}^n \omega_{\mu} v^{\nu} \delta^{\mu}{}_{\nu} = \sum_{\mu=1}^n \omega_{\mu} v^{\nu} \in \mathbb{K}
$$

Este tipo de vectores son solamente casos particulares de transformaciones más generales. De hecho, algunos vectores ni siquiera admiten una representación matricial, ya que no todos los espacios vectoriales son de dimensión finita. Por ello, es fundamental comprender los vectores y covectores como **transformaciones**. 

Dado un espacio vectorial $V$ sobre un cuerpo $\mathbb{K}$, su espacio dual $V^*$ se define como el conjunto de todas las transformaciones lineales $T: V \rightarrow \mathbb{K}$, bajo este contexto, un covector es un ejemplo de un tensor del tipo $(0,1)$.  De la misma forma, un vector puede interpretarse como un tensor de tipo $(1,0)$ con propiedades geométricas que no se discutirán por el momento. 

Cabe destacar que los espacios $\mathbb{R}^n$ o $\mathbb{C}^n$ son isomorfos con respecto a sus duales, lo que se denota como:

$$
(\mathbb{K}^n)^* ≅ \mathbb{K}^n
$$

Esto implica que no hay distinción esencial entre vectores y covectores y podemos considerar a ambos como si pertenecieran al mismo espacio.  

#### Matrices

Es necesario también revisar el concepto de matriz. A primera instancia, podemos definir a una matriz $A$ simplemente como una colección de números, organizados en filas y columnas:

$$
A =  \begin{bmatrix}
	a_1^1 & a_2^1 & \cdots & a_n^1 \\
    a_1^2 & a_2^2 & \cdots & a_n^2 \\
    \vdots & \vdots & \ddots & \vdots \\
    a_1^m & a_2^m & \cdots & a_n^m \\
\end{bmatrix}
$$

Sin embargo, esta noción inicial, aunque útil, es limitada, ya que no explica como esta puede operar sobre los vectores de un espacio, por lo que se vuelve necesario profundizar más sobre que son realmente las matrices. 

Podemos decir que una matriz $A \in \mathbb{K}^{m\times n}$ representa a una transformación lineal:

$$ 
A: \mathbb{K}^n \rightarrow \mathbb{K}^m 
$$

En donde $\mathbb{K}^n$ y $\mathbb{K}^m$ son espacios vectoriales sobre el campo $\mathbb{K}$.  Esta definición de matriz como transformación lineal implica que una matriz $A$ toma un vector $\vec{v}$ de $\mathbb{K}^n$ y lo mapea en un vector $\vec{v}'$ de $\mathbb{K}^m$.  Cada fila de $A$ "extrae" una componente del vector de salida, por lo que las filas de $A$ son funcionales del espacio dual $(\mathbb{K}^n)^*$. Dicho esto, expresar entonces a la matriz $A$ como un elemento de un producto tensorial:

$$ 
A \in \mathbb{K}^m \otimes (\mathbb{K}^n)^*
$$

En donde $(\mathbb{K}^n)^*$ es el dual de $\mathbb{K}^n$.  Esta formulación de $A$ como elemento del espacio $\mathbb{K}^m \otimes (\mathbb{K}^n)^*$ sugiere interpretar a la matriz $A$ como un vector columna de dimensión $m$, cuyas filas son covectores:

$$
A = \begin{bmatrix} \vec{a}^1 \\ \vec{a}^2 \\ \vdots \\ \vec{a}^m \end{bmatrix}, \qquad \text{con} \quad \vec{a}^i = \begin{bmatrix} a^i{}_1 & a^i{}_2 & \cdots a^i{}_n\end{bmatrix} \in (\mathbb{K}^n)^*
$$

A partir de la interpretación de la matriz $A$ puede como una colección de $m$ vectores fila, se puede recuperar su representación original:

$$
A = \begin{bmatrix} \vec{a}^1 \\ \vec{a}^2 \\ \vdots \\ \vec{a}^m \end{bmatrix} =  \begin{bmatrix}
	a^1{}_1 & a^1{}_2 & \cdots & a^1{}_n \\
	a^2{}_1 & a^2{}_2 & \cdots & a^2{}_n \\
    \vdots & \vdots & \ddots & \vdots \\
	a^m{}_1 & a^m{}_2 & \cdots & a^m{}_n \\
\end{bmatrix}
$$

Luego si $\vec{v}$ es un vector de $\mathbb{K}^n$ entonces se puede escribir la aplicación de $A$ sobre $\vec{v}$ como la aplicación de cada fila sobre el vector $\vec{v}$.

$$
\vec{v}' =  A(\vec{v}) =   \begin{bmatrix} \vec{a}^1(\vec{v}) \\ \vec{a}^2(\vec{v}) \\ \vdots \\ \vec{a}^m(\vec{v}) \end{bmatrix} = \begin{bmatrix} \sum_{i=1}^n a^1{}_i v^i \\ \sum_{i=1}^n a^2{}_i v^i \\ \vdots \\ \sum_{i=1}^n a^m{}_i v^i \end{bmatrix}
$$


Se definía también de forma simplificada la matriz transpuesta $A^T$ como la matriz $A$ con los índices transpuestos, sin embargo esta definición trae problemas ya que no nos indica como esta matriz transforma. 

Definimos entonces la transpuesta $A$ como a un elemento del espacio $(\mathbb{K}^n)^* \otimes \mathbb{K}^m$. que transforma como:

$$ 
A^T: (\mathbb{K}^m)^* \rightarrow (\mathbb{K}^n)^*
$$

En la matriz $A^T$ los elementos no solo se transponen, sino que que sus índices covariantes se vuelven contravariantes y viceversa, el elemento $a^i{}_j$ pasa a ser el elemento $a_i{}^j$. Puede entonces escribirse la transpuesta de la matriz $A$ matricialmente como:

$$
A^T = \begin{bmatrix} \vec{a}_1 & \vec{a}_2 & \cdots & \vec{a}_m \end{bmatrix}
=  \begin{bmatrix}
	a_1{}^1 & a_2{}^1 & \cdots & a_m{}^1 \\
	a_1{}^2 & a_2{}^2 & \cdots & a_m{}^2 \\
    \vdots & \vdots & \ddots & \vdots \\
	a_1{}^n & a_2{}^n & \cdots & a_m{}^n \\
\end{bmatrix}
$$

Luego si $\vec{\omega}$ es un vector del dual $(\mathbb{K}^n)^*$, es ahora $\vec{\omega}$ quien toma cada vector columna de $A^T$ y extrae una componente de un vector dual de salida $\vec{\omega}'$ de $(\mathbb{K}^m)^*$. Esto puede escribirse como:

$$
\vec{\omega} A^T = \begin{bmatrix} \omega(\vec{a}_1) & \omega(\vec{a}_2) & \cdots & \omega(\vec{a}_m)\end{bmatrix} = \begin{bmatrix}
\sum_{i=1}^na_1{}^i\omega_i & \cdots & \sum_{i=1}^na_m{}^i\omega_i
\end{bmatrix} = \vec{\omega}'
$$

Esta interpretación de una matriz transpuesta no solo clarifica que acción tienen los covectores sobre esta, sino que también simplifica entender la composición de transformaciones lineales.

Veamos ahora la multiplicación de matrices. Sean $A \in \mathbb{K}^m \otimes (\mathbb{K}^n)^*$ y $B \in \mathbb{K}^n \otimes (\mathbb{K}^p)^*$ matrices, es decir transformaciones:

$$
A: \mathbb{K}^n \rightarrow \mathbb{K}^m \qquad B: \mathbb{K}^p \rightarrow \mathbb{K}^n
$$

Luego la multiplicación de matrices $AB$ es simplemente la composición:

$$
AB: \mathbb{K}^m \rightarrow \mathbb{K}^n
$$

Estas matrices son casos particulares de lo que se conoce como tensores de tipo $(1,1)$.
 
### Tensores

Un **tensor** es un objeto matemático que permite describir relaciones en espacios vectoriales de forma independiente del sistema de coordenadas elegido. 

El ejemplo más sencillo de tensor es un **escalar** en un cuerpo $\mathbb{K}$, cuyo valor es independiente de cualquier sistema de coordenadas que se tome. Un vector también puede considerarse un tensor. Dado un espacio vectorial $V$ de dimensión $d$  y un vector $\vec{v} \in V$ podemos tomar una base $B = \{ \vec{e}_1, ..., \vec{e}_d \}$ de $V$ tal que:

$$
\vec{v} = \sum_{\mu} v^{\mu} \vec{e}_{\mu}
$$

En donde $v^{\mu}$ son las coordenadas de $\vec{v}$. Luego si escribimos a cada elemento de la base $B$ en términos de vectores una nueva base $B' = \{\vec{f}_{1}, ..., \vec{f}_{d}\}$ como:

$$
\vec{e}_{\mu} = \sum_{\nu} \Lambda_{\mu}{}^{\nu} \vec{f}_{\nu}
$$

Podemos escribir el mismo vector $\vec{v}$ en términos de la nueva base:

$$
\vec{v} = \sum_{\mu} v^{\mu} \sum_{\nu} \Lambda_{\mu}{}^{\nu} \vec{f}_{\nu} = \sum_{\nu} \left(\sum_{\mu} v^{\mu} \Lambda_{\mu}{}^{\nu} \right) \vec{f}_{\nu} \equiv \sum_{\nu} \tilde{v}^{\nu} \vec{f}_{\nu}
$$

En donde $\tilde{v}^{\nu}$ serán las nuevas coordenadas del vector $\vec{v}$. Si bien $\vec{v}$ posee ahora otra representación, sigue siendo el mismo objeto, ya que cuando sus coordenadas varían, los vectores de base varían también contrarrestando la variación de las primeras, preservando la naturaleza del objeto. Debido a esto puede decirse que un vector es un tensor.

En general, dado un espacio vectorial $V$ y su dual $V^∗$, podemos definir a un **tensor** de tipo $(k,l)$ sobre $V$ y un campo escalar $\mathbb{K}$ es una aplicación multilineal: 

$$
T \colon \underbrace{V^* \times \dots \times V^*}_{k \text{ veces}} \times \underbrace{V \times \dots \times V}_{l \text{ veces}} \to \mathbb{K}
$$

Donde $k$ y $l$ denotan el número de argumentos covariantes (duales) y contravariantes (primales), respectivamente. 

En el ejemplo anterior, dijimos que un vector $\vec{v} \in V$ es de hecho un tensor. Teniendo en cuenta la nueva definición de tensores como aplicaciones multilineales,

podemos ver al vector $\vec{v}$ como un tensor del tipo $(1,0)$, es decir, una aplicación $T: V^{*} \rightarrow \mathbb{K}$ que toma un covector y devuelve un escalar, definida como:

$$
T(\omega) = \omega(\vec{v}) \qquad \text{con } \omega \in V^*
$$

Se define la **contracción** de un tensor como una operación que asocia un tensor de tipo $(k-1, l-1)$ a uno de tipo $(k, l)$, al emparejar un índice covariante con uno contravariante mediante el producto interno.
 

También se define el **producto tensorial** de dos tensores $T$ de tipo $(k, l)$ y $T'$ de tipo $(k', l')$, denotado $T \otimes T'$, que da como resultado un tensor de tipo $(k + k', l + l')$.






### Producto escalar 

Dado un espacio vectorial $V$ un producto pseudo-escalar es un mapa bilineal $g: V \times V \rightarrow \mathbb{R}$ simétrico y no degenerado. 

Sea $F: V \rightarrow V^*$ una aplicación definida por el producto escalar, es decir $F$ toma vectores $\vec{v} \in V$ y devuelve la métrica evaluada parcialmente en $\vec{v}$ de modo que el resultado $F(\vec{v})$ es un covector que toma otro vector $\vec{u}$ y devuelve $g(\vec{v}, \vec{u})$.

Dada una base $\vec{e}_1, ..., \vec{e}_n$ de $V$ su base dual asociada $\vec{e}^1, ..., \vec{e}^n$ esta definida por el requisito:

$$\vec{e}^{\mu}(\vec{e}_{\nu}) = \delta^{\mu}{}_{\nu}$$

Podemos entonces escribir el producto escalar como:

$$
g(\vec{u}, \vec{v}) = \sum_{\mu \nu} g_{\mu \nu} u^{\mu} v^{\nu}
$$

Si $\omega \in V^*$ podemos escribir la acción de evaluar $\omega$ en un vector como:

$$
\omega(\vec{v}) = \sum_{\mu} \omega_{\mu} v^{\mu}
$$

$$
F(\vec{v}) = g(\sum_{\mu} v^{\mu} \vec{e}_{\mu},) = \sum_{\mu} v^{\mu} g(\vec{e}_{\mu}, ) \equiv \sum_{\mu} v_{\mu} \vec{e}^{\mu}
$$

En donde se define la coordenada covariante de un vector $\vec{v}$ en términos de su coordenada contravariante:

$$
v_{\mu} \equiv \sum_{\nu}g(\vec{e_{\nu}}, \vec{e_{\mu}}) v^{\nu} = \sum_{\nu} g_{\mu \nu} v^{\nu}
$$

Luego el producto interno entre dos vectores $\vec{u}, \vec{v} \in V$ puede ser escrito como:

$$
g(\vec{u}, \vec{v}) = \sum_{\mu \nu} u^{\mu} v^{\nu} g_{\mu \nu}  = \sum_{\mu} u^{\mu} v_{\mu}
$$
