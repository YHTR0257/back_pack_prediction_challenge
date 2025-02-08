# Challenge log

何を考えて、何をしているのかを書き出していく。
取った行動の狙いを明確にする。


## 20250208

コンペに参加！！！
本で学んだことを試していきたい。

### Done
- EDA
- - Trainは300000個のデータ
- - Testは200000個のデータ
- - ターゲットはPrice。
- - float型になる compartmentsとweight capacityの分布はtrainとtestでそこまで大きくは変わっていない。
- - 欠損値は全体の３％程度。compartments以外の全ての部分に存在。weight capacityが極端に少ない
- - Brands are Puma, Nike, Adidas, Under Armour, Jansport.
- - Materials are Leather, Canvas, Nylon, Polyester.
- - Compartments are 1~10.
- - Laptop compartment is Yes or No.
- - Waterproof is Yes or no.
- - Style are tote, backpack, messenger.
- - Color are Green, Blue, Black, Red, Pink and Gray.

カテゴリ変数が多いため、次元がかなり多くなってしまう。RandomForestなどは不向き・・・？やはりNNか
Sizeは0(Small),1(Medium),2(Large)でできる

カテゴリ間での標準偏差、平均、データ数を表示する。

大きく変化しているカテゴリーに対してはOne Hot Encodingを適用するのがいいかもしれない。ちょっと計算負荷が高すぎる。


今回のデータには
Laptop compartment, Size, WaterproofはLabel Encodingでいい
それ以外の4つのカテゴリ変数をどのようにして扱うかが難しい。

分散の感じを見る限り、Materialの影響度は大きそうなためこれはOnehotEncodingで
Laptop Compartment = 2のデータ数が少ないため、そこで大きな差が出ている。それ以外は結構均等に分布している。

ColorもLabel Encodingで良さげ。そこまで大きな分散を持っていない。
Brand, Material, Styleに対してTarget Encodingを行う。

学習モデルはXGBoost、Light GBM、NNのどれか
普通にアンサンブルしてもいいかもしれない。
optuna LightGBMを使ってみる。

### What learn

- Encoding方法
Count Encoding, Label Encoding
- - 今回のデータに関してはCount Encodingは適用しにくそう。自然言語処理などでは結構活躍するのではないか
- - Target Encodingは通用しそう。Priceのmeanが一番良さげ。組み合わせたものも追加しておくといい。

- Target Encodingでの注意点
Leakageに注意すること。Overfittingと似ている概念。回避する方法として
- - Greedy Target Encoding
- - Leave-one-out Target Encoding
- - Holdout Target Encoding これが一番いい方法
- - Smoothing

### Next

- Optuna LightGBMを使ってみる

### Problems


- 

---

#### Temps

### Done

### What learn

### Next

### Problems

### 