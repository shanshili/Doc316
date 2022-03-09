# 卡尔曼滤波器算法

1960年，卡尔曼发表了他著名的用递归方法解决离散数据线性滤波问题的论文。 从那以后，得益于数字计算技术的进步，卡尔曼滤波器已成为推广研究和应用的主题，尤其是在自主或协助导航领域。

卡尔曼滤波器由一系列递归数学公式描述。它们提供了一种高效可计算的方法来估计过程的状态，并使估计均方误差最小。 卡尔曼滤波器应用广泛且功能强大：它可以估计信号的过去和当前状态，甚至能估计将来的状态，即使并不知道模型的确切性质。

:::{note} 想要学习卡尔曼滤波器，个人推荐该系列视频： [(b站)卡尔曼滤波器](https://www.bilibili.com/video/BV1ez4y1X7eR)

一些资料：[百度网盘](https://pan.baidu.com/s/1bKELOhi6kIZ5C52OxSLPLg) 提取码：e26g
:::

## 算法推导与分析

首先将系统分为测量量$x_k$ 和过程量$Z_k$ ,

$$ x_k=Ax_{k-1}+Bu_{k-1}+w_{k-1} \\Z_k=Hx_k+v_k $$

其中，$w$ 为过程噪声，假设其符合正态分布$P(w)~(0,Q)$ ；$v$ 为测量噪声，假设其符合正态分布 $P(v)~(0,R)$。 由于噪声无法估计和测量，因此设先验估计和测的估计两中间量

$$ \widehat{x_k^-}=Ax_{k-1}+Bu_{k-1} \\ \widehat{{x_k}_{mea}}=Hx_k$$

卡尔曼滤波算法经过加权后的结果称作后验估计$\hat{x_k}$

$$ \widehat{x_k}=\widehat{{x_k}^-}+G\left(\widehat{x_{k_{mea}}}-\widehat{{x_k}^-}\right)\\G=K_kH $$

若$G=0$ ，后验估计等于先验估计，若 $G=1$ ，后验估计等于测得估计，即 $G$越大，系统越相信测量量。同时 $K_k$与$G$成正比，$K_k=0$ ，后验估计等于先验估计，
$K_k=H^-$，后验估计等于测的估计。而由于不知道误差，因此也无法设定$K_k$ ，故引入过程误差

$$ e_k=x_k-\widehat{x_k} $$

其中假设$e_k$符合正态分布$P(e_k)~(0,P_k)$，其量化了实际值与后验估计的差距。其中，

$$ P_k=E\left[e\ e^T\right]=E\left[\left(x_k-\widehat{x_k}\right)\left(x_k-\widehat{x_{k-1}}\right)^T\right] $$

联立上式，使$\frac{dtr(P_k)}{dK_k}$为0，即寻找 $P_k$最小自然方差，使 $K_k$最优，经推导得卡尔曼算法核心，卡尔曼增益

$$ K_k=\frac{P_k^-H^T}{HP_k^-H^T+R} $$

若调整$R$ ，$R$ 越大， $K_k \rightarrow 0$ ，系统相信估算值而非测量值，反之则更相信测量值。 其中 $P_k^-$ 为先验估计部分，除表示实际值与后验估计差值的$e_k$
以外，定义实际值与先验估计的差值$e_k^-$

$$ e_k^-=x_k-\widehat{x_k^-} $$

假设$e_k^-$符合正态分布 $P(e_k^-)~(0,P_k^-)$ ，同样对于$P_k^-$ ，有

$$ P_k^-=AP_{k-1}A^T+Q $$

可见$Q$与$P_k^-$成正比，$R一$定时，$Q$越小，$K_k\rightarrow0$，系统相信估算值而非测量值，反之则更相信测量值。
系统运行时，首先根据上一次的后验估计进行加权先验估计$\widehat{x_k^-}$，若为首次则可遵循预设值，或首次测量值；
接着根据给定的过程噪声协方差矩阵$Q$和上一次的误差协方差矩阵计算先验误差协方差矩阵$P_k^-$，若为首次则可遵循预设值； 根据给定的测量噪声协方差矩阵$R$和$P_k^-$，计算卡尔曼增益$K_k$；在最关键的一步中，
通过以上关键变量和测量结果可得到后验估计，即系统给出的估计值；最后更新后验误差协方差矩阵$P_k$。 使用卡尔曼滤波器的关键在于首先确定系统的性质，根据结果的连续性或离散性等选择合适的卡尔曼滤波器。
其次，需要通过一段系统实测的数据离线调试滤波器参数，以达到最适合系统的输出结果。

## 代码实现

示例为一个Python语言函数，其传入一个由原始数据构成的数组，返回一个由经卡尔曼算法估计的估计值数组。

```python
import numpy as np


def Kalman(dat):
    times = len(dat)
    # 过程噪声 - 协方差矩阵
    # 根据Pk-定义公式，Q与其成正比，根据K的定义公式，Pk-越小，K->0，相信估算而非测量量
    Q = 1e-2
    # 测量噪声 - 协方差矩阵
    # 根据K的定义公式，R越大，K->0，相信估算而非测量量
    R = 0.8
    Xhat = np.zeros(times)  # 后验估计
    X_hat = np.zeros(times)  # 先验估计
    Kk = np.zeros(times)  # 卡尔曼增益
    P = np.zeros(times)  # 误差 - 协方差矩阵
    P_ = np.zeros(times)  # 先验误差
    P[0] = 10
    Xhat[0] = dat[0]
    for n in range(1, times):
        # X - ^ (k) = A * X ^ (k - 1)
        X_hat[n] = Xhat[n - 1]
        # P - (n) = A * P(k - 1) * AT + Q
        P_[n] = P[n - 1] + Q
        # Kk[n] = P_[n] / (P_[n] + R)
        Kk[n] = P_[n] / (P_[n] + R)
        # Xhat[n] = X_hat[n] + Kk[n] * (dat[n] - X_hat[n])
        Xhat[n] = X_hat[n] + Kk[n] * (dat[n] - X_hat[n])
        # P[n] = (1 - Kk[n]) * P_[n]
        P[n] = (1 - Kk[n]) * P_[n]
    return Xhat
```

示例为一个C语言函数，展示了卡尔曼滤波迭代无需存储更多历史值的特性。该函数由read_data()读入当次原始数据raw，并根据公式计算。
最终返回该次迭代后的卡尔曼估计值est。

```C
float Kakman(void)
{
    char i = 10;
    // 过程噪声 - 协方差矩阵, 根据Pk-定义公式，Q与其成正比，根据K的定义公式，Pk-越小，K->0，相信估算而非测量量
    float Q = 0.0005;
    // 测量噪声 - 协方差矩阵, 根据K的定义公式，R越大，K->0，相信估算而非测量量
    float R = 0.001;
    float Kk = 0;
    float Xhat_prev = read_data();
    float Xhat_cur = 0, X_hat_prev = 0, X_hat_cur = 0, P__cur = 0, P__prev = 0, P_prev = 0, P_cur = 10;
    float raw;
    float est;
    while (i--)
    {
        raw = (float)read_data();
        // X - ^ (k) = A * X ^ (k - 1)
        X_hat_cur = Xhat_prev;
        // X_hat[n] = Xhat[n - 1]
        // P - (n) = A * P(k - 1) * AT + Q
        // P_[n] = P[n - 1] + Q
        P__cur = P_prev + Q;
        // Kk[n] = P_[n] / (P_[n] + R)
        Kk = P__cur / (P__cur + R);
        // Xhat[n] = X_hat[n] + Kk[n] * (dat[n] - X_hat[n])
        Xhat_cur = X_hat_cur + Kk * (raw - X_hat_cur);
        // P[n] = (1 - Kk[n]) * P_[n]
        P_cur = (1 - Kk) * P__cur;
        P_prev = P_cur;
        P__prev = P__cur;
        X_hat_prev = X_hat_cur;
        Xhat_prev = Xhat_cur;
    }
    est = Xhat_cur;
    return est;
}
```
