

# 最適化

---

## 最適化

* さまざまな意味で用いられる．
* ここでは，連続関数の最小値・最大値を求めることがテーマ
  * どちらでも同じなので，以下では，常に最小値と書く．

## なぜ最適化?

* 機械学習 (教師あり) でよく用いられる
  * 分類
  * 回帰
* 損失関数を最小化するようなパラメータを求める．

絵を入れる
<!-- .element: class="fixme" -->

---

## 手法

* 最急降下法
* 確率的勾配降下法 (SGD)
* SGDの改良

参考: [scikit-learn マニュアル](https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPRegressor.html?highlight=adam)


---

## 最小値の求め方

微分して0になる点を求め，値を計算すればよい．以上．

...

以上，ではない．

* 微分できるのか?
* 微分して0になる点がたくさんあったらどうするのか
* そもそも微分が0になる点をどう探すのか?


---

## 最小値を求めるアイディア

* 関数のグラフを書く．
* グラフの面の上に，どこか適当な点を出発点として定める．
* その点で各方面への傾斜を計算して，一番傾斜がきつい方向にちょっと降りてみる．
* そこで傾斜を計算し直す．繰り返す．
* 傾斜が十分小さくなったら，そこが求める値．

* 最急降下法 (steepest descent)，
  または，勾配降下法 (gradient descent) と呼ばれる．
  * 「最も速い」わけではない
* 原理として重要だが，このまま使われることは少ない．

本当に最小値にたどり着けるのか?

---

## 凸関数

* 凸関数 (convex function)
  * $ f(tx + (1-t)y) \leq tf(x) + (1-t)f(y) $  (ただし，$t \in [0, 1]$)
  * (適当な仮定の下で) どこでも2回微分が負にならないと言い換えられる．

* 凸関数の場合には，必ず最小値に行きそう．
* そうでないと，くぼみの底だけれど，最小値ではないところにいってしまうかも．
  * 局所最適 (local optimal) などと呼ばれる．

絵を入れる
<!-- .element: class="fixme" -->

* あいにく，興味のある関数はほとんど凸ではない．
* 実際，局所最適になってしまうこともしばしばある．


---

## 傾斜

* 傾斜 (gradient)
* 「一番傾斜がきつい方向」はどう選ぶのか?
* 微分すればわかる．
   $$
   \textrm{grad} f(x) = \left[\frac{\partial f(x)}{\partial x_1},
   \ldots,
   \frac{\partial f(x)}{\partial x_k}
   \right]
   $$
* どう微分する?
  * 解析的 (式変形)
    * 記号計算アプリケーションの利用 (WolframAlpha, SymPy, ...)
  * 数値的に計算する．[例](https://cs231n.github.io/optimization-1/#gradcompute)

---

## 学習率

* 学習率 (learning rate) または ステップサイズ (step size)
* 値の更新: $ w' \leftarrow w - \eta \\;\text{grad} f(w) $
  * $\eta$ が学習率
* 学習率が小さすぎると，収束が遅い．
* 学習率が大きすぎると，収束しない．

絵を入れる
<!-- .element: class="fixme" -->

実験をすべきだろう
<!-- .element: class="fixme" -->


---

## 確率的勾配法

* 機械学習では，最小化したい関数は，次のような形をしていることが多い．
  $$ f(w_1, \ldots, w_k) = \sum_{i = 1}^{N} g(x_i; w_1, \ldots, w_k)
  $$
  * $w_1, \ldots, w_k$ が適切に定めたいパラメータ
  * $x_1, \ldots, x_N$ は観測値で，$N$ は巨大な数．
* したがって，こうなる:
  $$ \text{grad}f = \sum_{i=1}^{N} \text{grad}g $$
* 最急降下法をそのまま適用すると，$\text{grad}f$ を計算する必要があるから，
  右辺を全部の $i$ について計算することになる．
  * 解の1回の更新に $N$ 回の計算が必要．
  * いかにも効率が良くない．

---

## 確率的勾配法

* 1回計算するたびに解を更新して，効率を上げる方法
  $\to$ 確率的勾配法 (Stochastic Gradient Descent = SGD)

* 手続き
  * 適当な初期値 $w = w_0$ から出発．
  * 収束するか，所定の反復回数に達するまで繰り返す:
    * 観測値 $\\{x_i \mid i = 1, \ldots, N\\} $ をシャッフル
    * 解を更新: $ w' \leftarrow w - \eta \\;\text{grad} g(x_i) $

* 本来のSGDは上記「1回ごと」だが，中間的な方法として，
  1と$N$の間の回数だけ計算して $w$ を更新することもある．
  1回の更新に使う観測値の集合をミニバッチ (mini-batch) と呼ぶ．
  この場合も SGD と呼ぶことがある．

* ニューラルネットワークの最適化で良く用いられる．

---

