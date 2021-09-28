
# 正規分布の標本分布

---

## 標本平均の分布: 分散が既知

* $\text{N}(\mu, \sigma^2)$ に従う母集団
* 標本平均 $ \displaystyle{\overline{X} = \frac{1}{n}\sum_{i=1}^{n} X_i }$
  の分布は，$\text{N}(\mu, \sigma^2/n)$ に従う
* $\displaystyle{Z := \frac{\overline{X} - \mu}{\sqrt{\sigma^2/n}}}$ 
  は $\textrm{N}(0, 1)$ に従う．
* $\overline{X}$ は $\mu$ の推定値として役立つ
* $n$ が増加すると，より正確になるが，誤差は，$\sqrt{n}$ のオーダーでしか減少しない

---

## $\chi^2$分布

* $Z_1, \ldots, Z_k$ を，独立な $N(0, 1)$ に従う分布とするとき，
  $\chi^2 := \sum_{i=0}^{n} Z_i ^ 2$ の分布を，
  自由度 $k$ の$\chi^2$分布 (カイ二乗分布，$\chi^2$-distribution) と呼ぶ．
  $\chi^2(k)$ と書く．
* 良く用いられる分布であり，伝統的には数表が整備されている．
  * 現在では，ライブラリに必ず用意されている


---

## $t$分布

* $Y$, $Z$ : 独立な確率変数
  * $Z$ は $\text{N}(0, 1)$ に従う．
  * $Y$ は 自由度$k$の$\chi^2$分布$\chi^2(k)$ に従う．
* $\displaystyle{ t := \frac{Z}{\sqrt{Y/k}} }$ が従う分布を，
  自由度 $k$ の $t$分布 ($t$-distribution) と呼ぶ．
  $t(k)$ と書く．
* 良く用いられる分布であり，伝統的には数表が整備されている．
  * 現在では，ライブラリに必ず用意されている


---

## 標本平均の分布: 分散が未知

* 標本平均 $ \displaystyle{\overline{X} = \frac{1}{n}\sum_{i=1}^{n} X_i }$
  の分布は，$N(\mu, \sigma/\sqrt{n})$ に従う
* $\displaystyle{Z := \frac{\overline{X} - \mu}{\sqrt{\sigma^2/n}}}$
  は $\textrm{N}(0, 1)$ に従うが，$\sigma^2$ がわかっていなければ計算できない．
* $\sigma^2$ を $s^2$ で代用する: 
  $\displaystyle{t := \frac{\overline{X} - \mu}{\sqrt{s^2/n}}}$
  * 分母の $s/\sqrt{n}$ は，(標本平均の)標準誤差 (standard error) と呼ばれる．
    これは，標本平均の標準偏差の推定値として用いられる．
* $t$ は，自由度 $n-1$ の $t$ 分布 $t(n-1)$ に従う．
  * $ \displaystyle{t = \left. \frac{ \overline{X} - \mu }{ \sqrt{\sigma^2/n} } \middle/      \sqrt{ \left. \frac{(n-1)s^2}{\sigma^2} \middle/ (n-1) \right. } \right. }$ と書けることに注意．




---

## 標本分散の分布

* $ \displaystyle{ s^2 := \frac{1}{n-1}\sum_{i=1}^{n} (X_i - \overline{X})^2  }$
* $E(s^2) = \sigma^2$
* 母集団が正規分布であるとき，$s^2$ は，自由度 $n-1$ の $\chi^2$分布に従う．
  * 自由度$n$ではないことに注意

