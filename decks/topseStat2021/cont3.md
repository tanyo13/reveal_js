
# 推定

---

## 推定

* 母集団の平均が知りたい．標本をとった．
* 標本の平均をもって母集団の推定量 (estimate) として良いか?
  * 点推定
  * よさそうだが，なぜ?
* 「平均」を「分散」「標準偏差」「範囲」に置き換えても良いか?
  * 全部OKとは言えなさそう
* 推定した値は，どれくらい正確 (だと期待される) か?
  * → 区間推定

---

## 点推定の基準

* 推定量に望まれる性質
* 不偏推定量 (unbiased estimator) : $ E(\hat{\theta}) = \theta$
  * $\hat{\theta}$ : 推定量，$\theta$ : 真の値
  * つねに，標本平均は，母平均の不偏推定量になる
* 一致推定量 (consistent estimator) : 
  $\forall \epsilon > 0.\\; \displaystyle{\lim_{n\to\infty} P(|\hat{\theta_n} - \theta| > \epsilon) = 0}$
  * $\hat{\theta_n}$ : 標本サイズが$n$の時の推定量
  * ほとんどの場合，標本平均は，母平均の一致推定量になる．(大数の法則)

---

## 最尤法

* 最尤法 (maximum-likelihood method)
* パラメタ $\theta_1, \ldots, \theta_k$ で定まる確率分布
  からの標本が与えられた時，パラメタを推定する方法
  * 機械学習などでは，まさにこれを行う．
* 分布を $f$，標本値を $x_1, \ldots, x_n$ とする．
* 尤度関数 (likelihood function) $ \displaystyle{L(\theta) := \prod_{i = 1}^{n} f(x_i; \theta)}$
  を最大にする $\theta$ を，推定値 $\hat{\theta}$ とする．
* 適用する際には，
  $\displaystyle{\frac{\partial}{\partial \theta}\log L(\theta) = 0}$ となる 
  $\theta$ を
  求めることが多い．

---

## 各分布の点推定

* 正規分布
  * 平均 : $\hat{\mu} = \overline{X} = \displaystyle{\frac1n \sum\_{i=1}^{n} X_i} $
    * 最尤法で求められる．
  * 分散 : $ \widehat{\sigma^2} = \displaystyle{\frac{1}{n-1} \sum_{i=1}^{n} (X_i - \overline{X})^2 } $
    * 最尤法で求めると，$\frac{1}{n-1}$ ではなく $\frac{1}{n}$ となる．
	  不偏推定量であるかどうか確認すると，修正が必要であることが分かる．
* 二項分布
  * $ \hat{p} = \overline{X}$ (成功 = 1, 失敗 = 0 として計算)
* ポアソン分布
  * $ \hat{\lambda} = \overline{X} $

---

## 区間推定

* 区間推定 (interval estimation) 
* 真の母数 $\theta$ が，区間 $ [L, U] $ に入る確率が
  $P(L \leq \theta \leq U) < 1 - \alpha$ 
  となるような，$L$, $U$ を求める．($L$, $U$ は確率変数)
  * $L$: 下側信頼限界 (lower confidence limit)
  * $L$: 上側信頼限界 (upper confidence limit)
  * $1-\alpha$ : 信頼係数 (confidence coefficient)
  * $[L, U]$ : 信頼区間 (conficdence interval)
    * 例: $\alpha = 0.05$ なら「95%信頼区間」
* 平均に関しては，同じ信頼係数では，区間の幅の長さは，標本サイズ $n$ に対して，
  おおむね $1/\sqrt{n} $ に比例する (中心極限定理)
* 具体的な標本から信頼区間を求めたときに，
  「真の母数が信頼区間に入る確率が $1-\alpha$ だ」
  <strong>というわけではない</strong> ことに注意．

---

## 正規母集団

* 母集団が正規分布である場合
* 母平均の信頼区間
  * 母分散 $\sigma^2$ が既知の時: 
    $ \displaystyle{\left[\overline{X} - \frac{c\sigma}{\sqrt{n}}, \overline{X} + \frac{c\sigma}{\sqrt{n}}\right]}$
    * $\overline{X}$ は標本平均
	* $c$ は，標準正規分布 $N(0, 1)$ の $\displaystyle{\frac{\alpha}{2}}$ 点．
	  
  * 母分散 $\sigma^2$ が未知の時: 
    $ \displaystyle{\left[\overline{X} - \frac{cs}{\sqrt{n}}, \overline{X} + \frac{cs}{\sqrt{n}}\right]}$
    * $\overline{X}$ は標本平均，$s$ は標本 (不偏) 分散
    * $c$ は，自由度 $n-1$ の $t$ 分布の$\displaystyle{\frac{\alpha}{2}}$ 点．
* $\displaystyle{\frac{\alpha}{2}}$ 点は，伝統的には，数表を引いて求めた．

---

## 二項母集団，ポアソン母集団

* 母集団が二項分布に従うの場合
  * $n$ が大きいとき，中心極限定理により，正規分布で近似できる．
  * 母平均の信頼区間 (近似的) :
    $ \displaystyle{\left[\overline{X} - c\sqrt{\overline{X}(1-\overline{X})/n},\\; \overline{X} + c\sqrt{\overline{X}(1-\overline{X})/n}\right]} $
    * $\overline{X}$ は標本平均
	* $c$ は，標準正規分布 $N(0, 1)$ の $\displaystyle{\frac{\alpha}{2}}$ 点．
* 母集団がポアソン分布に従う場合
  * $n$ が大きいとき，中心極限定理により，正規分布で近似できる．
  * 母平均の信頼区間 (近似的) :
    $ \displaystyle{\left[\overline{X} - c\sqrt{\overline{X}/n},\\; \overline{X} + c\sqrt{\overline{X}/n}\right]} $
    * $\overline{X}$ は標本平均
	* $c$ は，標準正規分布 $N(0, 1)$ の $\displaystyle{\frac{\alpha}{2}}$ 点．

---


