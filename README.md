# QGISで等高線


## この資料について

本資料は2018年9月19日に行われた奈良文化財研究所「遺跡情報記録課程」の「GIS演習」で使用した解説資料です。

## この時間に覚えること

この演習ではラスタデータ（紙地図）からベクタデータ（ポイントデータ）を作成し、ベクタデータからラスタデータ（標高ラスタ）を生成し、さらにもう一度ベクタデータ（等高線）を生成するという複雑な手順を行います。一連の作業でベクタデータとラスタデータの特徴を理解します。

- 紙図面から標高値を取得してポイントベクタを作成する。
- ポイントベクタから標高ラスタを作成する。
- 標高ラスタから等高線を発生させる。

## ドキュメント

- [配布資料](https://github.com/IshiiJunpei/QGISforArcContour/blob/master/040QGIS%E3%81%A7%E7%AD%89%E9%AB%98%E7%B7%9A.pdf)
- [スライド](https://IshiiJunpei.github.io/QGISforArcContour)


# QGISで等高線

Created by Ishii Junpei ( [@ishiijunpei](https://twitter.com/ishiijunpei))


## 作業の内容

- 紙図面から標高値を取得してポイントベクタを作成する
- ポイントベクタから標高ラスタを作成する
- 標高ラスタから等高線を発生させる

---
レイヤ→レイヤの作成→新規シェープファイルレイヤ

<img src="01.png" width=90%>

### 新規ファイルの設定

- タイプ　　　　　　　　　＝点
- ファイルエンコーディング＝UTF-8
- CRSの指定　　　　　　　＝後ほど説明
- 名称＝Level　　　タイプ＝小数点付き数値

<img src="02.png" width=50%>

- EPSGコード　30171
- Tokyo/Japan Plane Rectangular CS XI（日本測地系平面直角座標11系）

<img src="06.png" width=70%>


「Level_point」というファイル名で保存

<img src="03.png" width=70%>

---
### 標高値の入力
上の方にある「鉛筆マーク」をクリック

<img src="04.png" width=90%>

レイヤの編集モードになる

<img src="05.png" width=90%>

---
### 地物の追加

<img src="07.png" width=80%>

- 測量点をクリック
- 標高値を入力

<img src="08.png" width=80%>

---
上記の作業を繰り返して標高値を入力

<img src="09.png" width=80%>

---
### 標高ポイントから標高ラスタを作成
「ラスタ」→「解析」→「グリッド（補完）...」

<img src="11.png" width=90%>

- 入力ファイル　=標高の入ったポイントデータ
- Zフィールド　=標高の入ったフィールド
- アルゴリズム　＝「指数逆分布」が一番なめらか
- 指数　　　　　＝2.0〜4.0くらい

<img src="12.png" width=50%>

---
標高ラスタができる

<img src="13.png" width=80%>

---
ラスタなので段彩図にできる（Yl-Gr）

<img src="14.png" width=80%>

Spectralカラーパレット

<img src="15.png" width=80%>

---
### 等高線の生成
標高ラスタから投稿セインを生成します。

- 「ラスタ」→「抽出」→「等高線」

<img src="16.png" width=90%>

- 入力ファイル＝「DEM」
- 等高線間隔　＝「0.1」

<img src="19.png" width=80%>

- ファイル名　　　＝「contour」
- ファイルの種類　＝「Geopackage」
- エンコード　　　 =「UTF-8」

<img src="20.png" width=70%>

---
### 等高線

<img src="21.png" width=80%>

---
### 陰影図の作成
「ラスタ」→「地形解析」→「陰影図」

<img src="22.png" width=80%>


- 標高レイヤ＝「DEM」
- 出力形式　＝「GeoTIFF」
- Zファクタ =「2」

<img src="23.png" width=60%>

ファイル名　「Shade」

<img src="24.png" width=70%>

---
### 陰影図の出力

<img src="25.png" width=90%>

---
### 「DEM」を段彩図にする

<img src="26.png" width=70%>

陰影図の「混合モード」は「乗算」

<img src="27.png" width=70%>

<img src="28.png" width=90%>

---
## 調査区の形状に「クリップ」

調査区の範囲で等高線を切り抜きます。

- 「レイヤ」→「レイヤの作成」→「新規シェープファイルレイヤ」

<img src="01.png" width=90%>

- タイプ＝ポリゴン
- ファイルエンコーディング＝UTF-8
- CRS＝プロジェクトCRS（EPSG30171:TTokyo / Japan Plane Rectangular11） 

<img src="31.png" width=50%>

ファイル名：「Clip」

<img src="32.png" width=70%>

---
調査区をトレースしてポリゴンを作成します。

- 編集モード切替
- ポリゴン地物を追加

<img src="33.png" width=90%>

- 調査区の形状をトレース
- 最終点をクリックしてから、右クリックで終了

<img src="34.png" width=90%>

id=「01」（整数値なら何でも良い）

<img src="35.png" width=90%>

### 調査区ポリゴン

<img src="36.png" width=90%>

---
### 調査区ポリゴンで等高線をクリップ

-「ベクタ」→「空間演算ツール」→「クリップ」

<img src="29.png" width=90%>

---
- 「入力レイヤ」→クリップされるデータ（等高線）
- 「クリップレイヤ」→クリップする範囲（調査区）

<img src="37.png" width=70%>

- 「保存ファイル」→「contour_clip」
- 「レイヤ名」→「contour_clip」

<img src="38.png" width=50%>

---
### 調査区ポリゴンでクリップされた等高線

<img src="39.png" width=90%>

---
### ラスタのクリップ
等高線と同様に標高ラスタも調査区ポリゴンでクリップします。

<img src="40.png" width=90%>


「ラスタ」→「抽出」→「マスクレイヤによるラスタのクリップ」

<img src="41.png" width=90%>

---
- 入力レイヤ（クリップされる側のレイヤ）＝DEM
- マスクレイヤ（クリップする側のレイヤ）＝Clip
- クリップされた新たなラスタデータの名前を指定して保存＝DEM_clip.tif

<img src="42.png" width=50%>

---
### クリップされたラスタレイヤ

<img src="43.png" width=100%>

---
## 作業のまとめ

- ベクタポイントからDEMを出力する方法は応用が広いのでぜひマスターしてください。
	- 標高データだけでなく、遺物の出土分布の等密度線
- クリップ機能を利用したベクタやラスタの切り抜きは、分析的な作業の前段処理で必ず使います。
	- たとえば河川流域だけを分析対象とする場合の前処理

