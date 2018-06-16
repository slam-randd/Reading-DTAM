## 誤差関数

### 誤差

誤差の定義は単純である．ある3次元空間座標 \\(\mathbf{x} = \pi^{-1}(\mathbf{u}, d)\\) について，

1. \\(\mathbf{x}\\) をフレーム \\(r\\) から観測したときの輝度 \\(I_r(\mathbf{u})\\)
2. \\(\mathbf{x}\\) をフレーム \\(m\\) から観測したときに， \\(\mathbf{x}\\) に対応するピクセル \\(\mathbf{v} = \pi(KT_{mr}\mathbf{x})\\) の輝度 \\(I_r(\mathbf{v})\\)

の差のL1ノルムを誤差としている (元論文図1)．

$$
\rho_r(I_m, \mathbf{u}, d) = I_r(\mathbf{u}) - I_m(\pi(K T_{mr} \pi^{-1}(\mathbf{u}, d)))
$$

$$
C_r(\mathbf{u}, d) = \frac{1}{L(r)} \underset{m \in L(r)}{\sum} || \rho_r(I_m, \mathbf{u}, d) ||_1
$$

### 正則化
正則化項は \\(g(\mathbf{u})||\nabla \xi(\mathbf{u})||_{\epsilon}\\) である．

このうち， \\(|| \nabla \xi(\mathbf{u})||_{\epsilon}\\) は深度のなめらかさを与えるものである．

\\(|| \cdot ||_{\epsilon}\\) は

$$
||\mathbf{x}||_{\epsilon} = \begin{cases}
    \frac{||\mathbf{x}||^2_2}{2\epsilon} & \text{if}\,||\mathbf{x}||_2 \leq \epsilon \\
    ||\mathbf{x}||_1 - \frac{\epsilon}{2} & \text{otherwise}
\end{cases}
$$

で定義される．  
\\(||\mathbf{x}||_2 \leq \epsilon\\) のときはなめらかな復元結果を得られるようL2ノルムを適用している．  
\\(||\mathbf{x}||_2 > \epsilon\\) のときは物体の境界などにおける深度の不連続性を許容するためL1ノルムがかかった値を返す．

\\(g(\mathbf{u})\\) は

$$
g(\mathbf{u}) = e^{-\alpha ||\nabla I_r(\mathbf{u})||^{\beta}_2}
$$

で定義される．この関数は画像の輝度の変化が大きいときに小さな値を取る．

以上より，\\(g(\mathbf{u})||\nabla \xi(\mathbf{u})||_{\epsilon}\\) は画像の輝度変化が大きい部分に対しては深度の不連続性を許容し，輝度変化が小さい部分に対しては不連続性を制約する．

