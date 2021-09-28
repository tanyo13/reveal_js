---

# 基本統計量


---

## 統計学とデータサイエンス

* 


---

## 平均

* 平均 (mean)
  * $x_1, x_2, \ldots, x_n$ : データ
  * $n$ : データ数

$$ \bar{x} = \frac{1}{n}\sum_{i=1}^{n} x_i $$


* トリム平均 (trimmed mean)
  * $x_{(1)}, x_{(2)}, \ldots, x_{(n)}$ データを整列したもの
  * 上端下端の $p$ 個のデータを取り除く
  * 極端な値の影響をのぞける．

$$ \bar{x} = \frac{1}{n-2p}\sum_{i = p+1}^{n-p} x_{(i)} $$

---

## 平均

* 加重平均 (weighted mean)
  * $w_i$ : データ $x_i$ の重み
  * $W = {\sum_{i=1}^{n}w_i}$

$$ \bar{x} = \frac{1}{W} \sum_{i=1}^{n} w_ix_i $$


---

## 中央値

* 中央値 (median)
* データを整列したとき中央に位置するデータの値
  * データが偶数個のときには，適当に処置する．
    たとえば中央2個の平均を取る．
* 中央値の方が，平均より良い指標となることが多い
  * 例: 世帯収入を代表する値
* 平均に比較して，計算が高価
  * 平均: バッチ $O(n)$， オンライン $O(1)$
  * 中央値: 典型的には， バッチ $O(n\log n)$，オンライン $O(n)$
<!-- .element: style="margin-bottom: 60px;" -->
* 加重中央値 (weighted median)
  * データに重みがある
  * データを整列し，重みの総和が上下等しくなる位置の値
  * 外れ値の影響を受けにくい

---

## 外れ値

* 外れ値 (outlier)
* データセットの他の値から大きく離れた値のこと
  * 主観に左右される
* データそのものを不当にしたりエラーにするわけではない
  * 例: 世帯収入データの中の1人の大金持ち
* エラーのせいで外れ値が生じることも多い
  * 単位の見誤り
  * センサー異常
* 代表の値の取り方によって，影響が異なる
  * 平均値には大きな影響を与える
  * 中央値やトリム平均に与える影響は少ない -- 頑健な (robust) 推定値

---

## 標準偏差

* 分散 (variance) :
$$ s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2 $$
* 標準偏差 (standard deviation) : 
$$ s = \sqrt{\text{分散}} $$
* 分散はデータの尺度の2乗だが，標準偏差は同じ尺度であることに注意
* 平均絶対偏差よりも，数学的扱いが便利
* $n-1$ではなく$n$で除することもある
  * $n-1$ で除するものを，不偏分散 (unbiased variance) とよぶ．
    おそらく後述
  * $n$ が大きいときには，両者に大きな差は無い

---

## 散らばり

* 偏差 (deviation) : データと推定値との差
  * データセット $\\{1, 4, 4\\}$ の平均値は3, データ 1 と平均値との偏差は
    -2
* 偏差の代表値を考えたい．
  * 偏差の平均は役に立たない
* 平均絶対偏差 (mean absolute deviation)
  $$ \frac{1}{n} \sum_{i=1}^{n} | x_i - \bar{x} |
  $$

---

## 散らばりの頑健推定

* 中央絶対偏差 (Median Absolute Deviation from the median = MAD) :
$\\{ x_1 - \bar{x}, x_2 - \bar{x}, \ldots, x_n - \bar{x} \\}$
の中央値


---

## 順序にもとづく散らばりの推定

* 順序統計量 (order statistics) : 整列したデータ値にもとづく統計量の総称
* パーセンタイル (percentile) : 
  * P パーセンタイル とは:
    * データの P % がこの値以下
	* データの (100-P) % がこの値以上
  * 50 パーセンタイル = 中央値
* 分位数 (quantile) :   0.8分位数 = 80 パーセンタイル


---

## 順序にもとづく散らばりの推定 (つづき)

* 範囲 (range) : 最大値と最小値の差
  * データの散らばりの指標としてわかりやすいが，
    外れ値から特に影響を受けやすい．
* 四分位範囲 (interquartile range = IQR)
  * 75パーセンタイルと25パーセンタイルの差
  * 「範囲」に比較すれば，外れ値の影響を受けにくい．
* 例: データセット $\\{3, 1, 5, 3, 6, 7, 2, 9\\}$
  * 整列: $\\{1, 2, 3, 3, 5, 6, 7, 9\\}$
  * 25パーセンタイル : 2と3の間 → 2.5
    * いろいろな補間法有り
  * 75パーセンタイル : 6と7の間 → 6.5
  * 四分位範囲 = 6.5 - 2.5 = 4.0
* 全データの整列を要するので，計算に時間がかかる．
  近似的に求める場合もある．

---

## 可視化 - 箱ひげ図

* 箱ひげ図 (boxplot)
* いろいろな種類がある．良く用いられるもの:
  * 箱の上辺 : 75パーセンタイル
  * 箱の中央線 : 中央値
  * 箱の下辺 : 25パーセンタイル
  * ひげ (点線) : IQRの1.5倍を超えないもっとも遠いデータまで
  * 点 (小円) : ひげの外側にあるデータ

---

## ヒストグラム

* 度数分布表 (frequency table) 
* ヒストグラム (histogram)

---

## 密度プロット

* カーネル密度推定 (kernel density estimation)
  * $\hat{f}$ : 推定密度関数
  * $K(x)$ : カーネル関数．全域の定積分は1
    * 典型的には，平均0, 分散1 のガウス分布
  * $h$ : 平滑パラメータ (バンド幅)

$$ \hat{f}\_h(x) = 
   \frac{1}{nh} 
   \sum\_{i=1}^{n} \\;K\\!\left(\frac{x - x_i}{h}\right) $$


---

## カテゴリデータ

* 二値データ (binary data) : 2つの値のどちらかを取るデータ
  * 0/1, True/False, Yes/No など，
* カテゴリデータ (category data) : 定まった複数個のいずれかの値を取るデータ
  * 優/良/可, 名詞/動詞/形容詞/その他 など，
* 棒グラフ (bar chart) によって可視化できる
* グラフによる可視化に関する注意
  * Wikipedia の記事 「[誤解を与える統計グラフ](https://ja.wikipedia.org/wiki/%E8%AA%A4%E8%A7%A3%E3%82%92%E4%B8%8E%E3%81%88%E3%82%8B%E7%B5%B1%E8%A8%88%E3%82%B0%E3%83%A9%E3%83%95)」 
  * 円グラフ (pie chart) の使用の是非に関しては，
  [議論](https://www.perceptualedge.com/articles/visual_business_intelligence/save_the_pies_for_dessert.pdf)がある．

---

## カテゴリデータの代表値

* 最頻値 (mode)
  * もっとも件数の多いデータ
* 期待値 (expected value)
  * カテゴリが同じ尺度の離散値を表している場合に使える
  * 頻度 (= そのカテゴリの件数 / 総数) を重みとした，値の加重平均
  

---

## 相関

* 散布図 (scatterplot)
  * 数量変数 X と Y との関係を図に表したグラフ
  * 一つのデータの X, Y の値のところに点を打つ．
* 相関係数 (correlation coefficient)
  * 数量変数 X, Y が互いに関連する程度を図った指標
  * -1 以上 1 以下
    * 正の大きな値: X が増えると Y も増える傾向にある
	* 負の大きな値: X が増えると Y は減る傾向にある
	* 絶対値の小さな値: X と Y の間には関係があまりない
  * $s_x$ : X の標準偏差, $s_y$ : Y の標準偏差
  

$$ \text{相関係数}\quad r = 
      \frac{
	    \sum_{r=1}^{n}(x_i - \bar{x})(y_i - \bar{y})
	  }{
        (n-1) s_x s_y
	  }
$$ 

---

## 相関 (つづき)

* 相関行列 (correlation matrix) : 
  複数の変数間の相関を表した行列
  * ヒートマップで可視化できる

---

## 大量の2変量の可視化

* 散布図は，大量のデータ値を可視化するのには不向き
* 六角ビニング (hexagonal binning)
  * 六角形の色の濃さで数量を表す
* 等高線プロット (contour plot)
  * 等高線で数量を表す

---

## 省略?

以下は省略するつもり
<!-- .element: class="fixme" -->

* 分割表 (contingency table)
* 箱ひげ図による比較，バイオリンプロット
* 多変量の可視化

---


# 課題1


---

## 課題1

以下の問の1問以上を解答せよ．
2問以上解答した場合には，その中で最も高い得点を
この課題の評点とする．
