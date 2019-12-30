# Fourier Transform
$F(\omega)=\int_{-\infty}^{\infty}f(t)e^{-i\omega t}dt$

$=\int_{-\infty}^\infty f(t)\cos(\omega t)-i\int_{-\infty}^\infty f(t)\sin(\omega t)$

$F(\xi)=\int_{-\infty}^{\infty}f(t)e^{-i2\pi \xi t}dt$

Inverse:

$f(t) = \frac{1}{2\pi}\int_{-\infty}^\infty F(\omega)e^{i\omega t}d\omega$

$=\int_{-\infty}^\infty F(\xi)e^{i2\pi\xi t}d\xi$

---
# Discrete-Time Fourier Transform
对连续时间非周期信号进行抽样（乘积），得到的离散时间非周期信号再求傅里叶变换的过程就是DTFT。其实等同于信号频谱与脉冲信号频谱的卷积，这样得到的就是连续且周期DTFT频谱（把频谱进行了周期延拓）

$F(\omega)=\sum_{n=0}^Nf(n)e^{-i\omega n}$

Inverse:

$f(n)=\frac{1}{2\pi}\int_{-\infty}^{\infty}F(\omega)e^{i\omega n}d\omega$

---

# Discrete Fourier Transform
对连续信号分析不可能，对无限长的离散信号做分析也是不可能的。所以我们又引入了DFT。DFT可以看成是对DTFT得到的周期性频域的采样。由于周期性只保留一个周期的频域结果从而得到时频域都有限的序列。

DFT可以看作有限长离散信号经过周期延拓之后作DFS（离散傅里叶级数）。DFS的所有基函数，其角频率都是$2\pi/N$的整数倍，即基频为 $2\pi/N$。和FS的基频$1/T$进行类比，可以发现在离散语境下的N和连续语境下的T是同一个意义。所以在DFS语境下，N为周期序列的一个周期，回到DFT语境下，就是“将有限长离散信号进行周期延拓”的“周期”，它一般要大于等于信号的长度。

离散傅里叶变换得到的频谱是中心对称的频谱，只取前N/2分析即可。

f(n)补零之后的DFT增加了在f(nT)连续频域谱上的采样。采样点数从N增加到M，从而提高了DFT频谱的分辨率。




$F(k)=\sum_{n=0}^Nf(n)e^{-i\frac{2\pi k}{N}n}$

inverse:
$f(n)=\sum_{k=0}^NF(k)e^{i\frac{2\pi k}{N}n}$

---

# FFT
https://jakevdp.github.io/blog/2013/08/28/understanding-the-fft/

如果N不是2为基础的整数次的倍数，则可以补零


---

# 栅栏效应
不管是时域采样还是频域采样，都有相应的栅栏效应。只是当时域采样满足采样定理时，栅栏效应不会有什么影响。而频域采样的栅栏效应则影响很大，“挡住”或丢失的频率成分有可能是重要的或具有特征的成分，使信号处理失去意义。

---

# 频谱泄露
频谱泄露就是分析结果中，出现了本来没有的频率分量。

信号为无限长序列，运算需要截取其中一部分（截断），于是需要加窗函数，加了窗函数相当于时域相乘，于是相当于频域卷积，于是频谱中除了本来该有的主瓣之外，还会出现本不该有的旁瓣，这就是频谱泄露！为了减弱频谱泄露，可以采用加权的窗函数，加权的窗函数包括平顶窗、汉宁窗、高斯窗等等。而未加权的矩形窗泄露最为严重。

---

# Short-Time Fourier transform
$x[k,m]=\displaystyle\sum_{n=0}^{N-1}x[m\delta+n]w(n)e^{-i\omega n}$
where $m$ is the time-frame index; $\delta$ is the hop size; $n$ is the window size

