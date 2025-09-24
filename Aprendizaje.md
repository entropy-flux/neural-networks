Supongamos un conjunto de $N$ muestras $\Omega = \{ \omega_1, \omega_2, ..., \omega_N \}$ 








$$
L_2 = \sqrt{\sum_{j=1}^N (Z(\omega_j) - z_j)^2}
$$

$$
\frac{\partial L_2}{\partial w ^{\alpha}} = \frac{1}{L_2} \sum_{j=1}^N (Z(\omega_j) - z_j) \frac{\partial Z(\omega_j)}{\partial w^{\alpha}}
$$

$$
Z(\omega_j) = \sum_{\mu \nu} g_{\mu \nu} X^{\mu}(\omega_j)  w^{\nu} 
$$

$$ 
\frac{\partial Z(\omega_j)}{\partial w^{\beta}} = \sum_{\mu \nu} g_{\mu \nu} X^{\mu}(\omega_j)  \frac{\partial w^{\nu}}{\partial w^{\beta}} = \sum_{\mu \nu} g_{\mu \nu} X^{\mu}(\omega_j)  \delta^{\nu}_{\beta}  = X_{\beta}(\omega_j)
$$

$$
\vec{\nabla}_{\mathbf{w}} L_2 = \sum_{\alpha \beta} g^{\alpha \beta} \frac{\partial L_2}{\partial w^{\beta}} \frac{\partial}{\partial w^{\alpha}} = 0
$$

$$
\sum_{j=1}^{N} \sum_{\alpha \beta} \sum_{\mu \nu} g_{\mu \nu} X^{\mu}(\omega_j)  w^{\nu} g^{\alpha \beta} X_{\beta}(\omega_j)  \frac{\partial}{\partial w^{\alpha}} - \sum_{j=1}^{N}\sum_{\alpha \beta} z_j g^{\alpha \beta} X_{\beta}(\omega_j)  \frac{\partial}{\partial w^{\alpha}} = 0
$$

$$
\sum_{\alpha} \left( \sum_{\nu} w^{\nu}  \sum_{j=1}^{N} X^{\alpha}(\omega_j)  X_{\nu}(\omega_j)- \sum_{j=1}^N X^{\alpha}(\omega_j) z_j \right) \frac{\partial}{\partial w^{\alpha}} = 0
$$

$$
\sum_{\nu} w^{\nu}  \sum_{j=1}^{N} X^{\alpha}(\omega_j)  X_{\nu}(\omega_j) = \sum_{j=1}^N X^{\alpha}(\omega_j) z_j
$$

$$
\mathbf{w} (\mathbf{X}^T \mathbf{X}) = \mathbf{X}^T  \mathbf{z}
$$

$$
\mathbf{w} =  (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{z}
$$