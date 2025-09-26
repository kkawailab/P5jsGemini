# 第4章: 変数

プログラミングにおける最も重要な概念の一つが「変数」です。変数を使うことで、値を記憶したり、後から変更したりできるようになり、プログラムで表現できることが一気に広がります。特に、アニメーションやインタラクションを作る上で、変数は欠かせない存在です。

## 4.1 変数とは？

変数とは、数値や文字列などのデータを入れておくための「名前付きの箱」のようなものです。

- **名前（変数名）**: 箱につけるラベルです。後から中身を取り出すときに、この名前を使います。
- **値**: 箱の中に入れるデータです。

なぜ変数が必要なのでしょうか？
- **再利用**: 同じ値を何度も使いたいとき、変数に入れておけば、その名前を呼び出すだけで済みます。
- **管理のしやすさ**: 後から値を変更したくなったとき、変数を使っていれば、一箇所変更するだけで、その変数が使われているすべての場所が更新されます。
- **動的な表現**: 変数の中身を少しずつ変えていくことで、アニメーションが作れます。

## 4.2 変数の使い方

変数を使うには、まず「宣言」し、次に「代入」します。

### 宣言と代入

JavaScript (p5.js) では `let` というキーワードを使って変数を宣言します。

```javascript
// 'let' を使って 'x' という名前の変数を宣言する
let x;

// '=' を使って、変数 'x' に 100 という値を代入する
x = 100;

// 宣言と代入は同時に行うこともできます。こちらが一般的な書き方です。
let circleSize = 50;
```

一度宣言した変数の値は、後から何度でも変更できます。

```javascript
let score = 0;
score = 10; // score の中身が 10 になる
score = score + 5; // score の中身が 15 になる (現在の値 10 + 5)
```

## 4.3 変数でアニメーションを作ろう

変数の値を `draw()` ループの中で少しずつ変えることで、アニメーションを実現できます。

まず、円のx座標を管理する変数 `circleX` を用意します。この変数は `setup()` と `draw()` の両方で使いたいので、関数の外側で宣言するのがポイントです。

```javascript
// 変数は、setupやdrawの外側で宣言することで、
// スケッチ全体で使えるようになります。
let circleX = 50;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 変数 circleX を使って円を描画
  ellipse(circleX, 200, 80, 80);
  
  // circleXの値を毎回1ずつ増やす
  circleX = circleX + 1;
}
```

このコードを実行すると、`draw()` が呼ばれるたびに `circleX` の値が `1` ずつ増えていくため、円が右に動いていくアニメーションになります。

## 4.4 p5.jsの便利な組み込み変数

p5.jsには、あらかじめ用意されている便利な変数がいくつかあります。これらは自分で宣言しなくても自由に使えます。

- `width`, `height`: キャンバスの幅と高さを表す変数です。`createCanvas()` で指定した値が自動的に入ります。例えば、キャンバスの中央のx座標は `width / 2` で求めることができます。
- `mouseX`, `mouseY`: マウスカーソルの現在のx座標とy座標を常に記録している変数です。これらを使うと、マウスの動きに合わせたインタラクティブな作品が簡単に作れます。

### `width`, `height` の使用例

```javascript
function setup() {
  createCanvas(600, 400);
}

function draw() {
  background(220);
  
  // width/2 と height/2 を使って、常にキャンバスの中央に円を描く
  ellipse(width / 2, height / 2, 100, 100);
}
```

### `mouseX`, `mouseY` の使用例

```javascript
function setup() {
  createCanvas(400, 400);
  noStroke();
}

function draw() {
  background(220);
  
  // マウスカーソルの位置に円を描く
  fill(255, 0, 0, 150); // 少し透明な赤色
  ellipse(mouseX, mouseY, 50, 50);
}
```
このコードを実行して、マウスを動かしてみてください。円がマウスに追従するはずです。

---

## 章末問題

### 問題1
変数 `rectY` を作り、その値を `draw()` の中で毎回 `2` ずつ増やしてください。その変数を使って四角形を描画し、上から下へ動くアニメーションを作成しましょう。

<details>
<summary>解答</summary>

```javascript
let rectY = 0;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // rectY を四角形のy座標として使用
  rect(150, rectY, 100, 100);
  
  // rectYの値を2ずつ増やす
  rectY = rectY + 2;
}
```
</details>

### 問題2
`mouseX` と `mouseY` を使って、円の色を変化させるスケッチを作成してみましょう。`fill()` の引数に `mouseX` や `mouseY` を使ってみてください。（ヒント: 色の範囲は通常0-255です。`mouseX` の値が大きくなりすぎないように調整が必要かもしれません。）

<details>
<summary>解答例</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // mouseXを赤、mouseYを青の強さに対応させる
  // そのまま使うと値が255を超えてしまうので、
  // 255で割った余りを使うなどの工夫をする (ここでは % 255 を使用)
  let r = mouseX % 255;
  let b = mouseY % 255;
  
  fill(r, 0, b);
  
  ellipse(width / 2, height / 2, 200, 200);
}
```
</details>

### 問題3
`width`, `height`, `mouseX`, `mouseY` の4つの組み込み変数を使って、キャンバスの四隅とマウスカーソルを結ぶ4本の線を描画するスケッチを作成してください。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
  strokeWeight(2);
}

function draw() {
  background(220);
  
  // マウスカーソルの位置
  let mx = mouseX;
  let my = mouseY;
  
  // 左上 (0, 0) からマウスへ
  line(0, 0, mx, my);
  
  // 右上 (width, 0) からマウスへ
  line(width, 0, mx, my);
  
  // 左下 (0, height) からマウスへ
  line(0, height, mx, my);
  
  // 右下 (width, height) からマウスへ
  line(width, height, mx, my);
}
```
</details>