# 第7章: インタラクション

これまでは、あらかじめプログラムされた通りに動くスケッチを作成してきました。この章では、ユーザーのマウス操作やキーボード入力に反応する「インタラクティブな」作品の作り方を学びます。これにより、作品は単なるアニメーションから、ユーザーが参加できる体験へと進化します。

## 7.1 イベント関数とは？

インタラクションを実現するために中心的な役割を果たすのが「イベント関数」です。

イベント関数は、`draw()` のように常に実行されるのではなく、「マウスがクリックされた」「キーが押された」といった特定の**イベント（出来事）が発生したときに、p5.jsによって自動的に呼び出される**特別な関数です。

## 7.2 マウスイベント

マウスの操作に反応するためのイベント関数や変数が用意されています。

### `mousePressed()`
マウスボタンが**押された瞬間**に、一度だけ実行される関数です。

```javascript
function setup() {
  createCanvas(400, 400);
  background(220);
}

function draw() {
  // draw()は空でもOK
}

// マウスが押されるたびに、その場所に円を描く
function mousePressed() {
  noStroke();
  fill(255, 0, 0, 100); // 半透明の赤
  ellipse(mouseX, mouseY, 50, 50);
}
```
このスケッチを実行し、キャンバス上を何度もクリックしてみてください。クリックした場所に円が描かれていきます。

### `mouseReleased()`
マウスボタンが**離された瞬間**に、一度だけ実行される関数です。

### `mouseIsPressed` 変数
これは関数ではなく、**マウスボタンが押されている間 `true` になり、離されている間 `false` になる**ブール型の変数です。`draw()`ループの中で使うことで、「押している間だけ〜する」という処理が簡単に書けます。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // もしマウスが押されているなら
  if (mouseIsPressed === true) {
    // 背景を黒にする
    background(0);
  }
  
  ellipse(width / 2, height / 2, 100, 100);
}
```

## 7.3 キーボードイベント

キーボードからの入力に反応することもできます。

### `keyPressed()`
いずれかのキーが**押された瞬間**に、一度だけ実行される関数です。

### `key` 変数と `keyCode` 変数
`keyPressed()`関数の中で、どのキーが押されたかを知るために、p5.jsは2つの便利な変数を用意しています。
- `key`: 押されたキーの**文字**を保持します。（例: `'a'`, `'B'`, `' '` (スペース)）
- `keyCode`: すべてのキーに割り当てられたユニークな番号です。特に矢印キーやSHIFTキーなど、文字ではないキーを判別するのに使います。（例: `UP_ARROW`, `LEFT_ARROW`, `SHIFT`）

```javascript
let x = 200;
let y = 200;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  ellipse(x, y, 50, 50);
}

// キーが押されたときに実行
function keyPressed() {
  // もし押されたキーが左矢印キーなら
  if (keyCode === LEFT_ARROW) {
    // x座標を10減らす
    x = x - 10;
  } 
  // もし押されたキーが右矢印キーなら
  else if (keyCode === RIGHT_ARROW) {
    // x座標を10増やす
    x = x + 10;
  }
}
```
このスケッチを実行し、左右の矢印キーを押してみてください。円が左右に動くはずです。

## 7.4 状態を管理する

イベント関数は、`draw()`ループの外で、イベントが発生したときにだけ実行されます。そのため、イベントの結果を`draw()`ループに反映させるには、**状態を管理する変数**を介して情報をやり取りするのが一般的なテクニックです。

例えば、「キーを押すたびに円の表示/非表示を切り替える」スケッチを考えてみましょう。

```javascript
// 円が表示されているかどうかを管理する変数（状態変数）
let isCircleVisible = true;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // もし円が表示状態なら、円を描く
  if (isCircleVisible === true) {
    ellipse(width / 2, height / 2, 100, 100);
  }
}

// キーが押されたら、状態を反転させる
function keyPressed() {
  // isCircleVisibleの値を現在の反対にする
  // trueならfalseに、falseならtrueになる
  isCircleVisible = !isCircleVisible;
}
```

---

## 章末問題

### 問題1
マウスをクリックするたびに、円の色がランダムに変わるスケッチを作成してください。ヒント: `random(255)` を使うと0から255までのランダムな数値を取得できます。

<details>
<summary>解答</summary>

```javascript
// 色を保存する変数
let r = 255;
let g = 255;
let b = 255;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  fill(r, g, b);
  ellipse(width / 2, height / 2, 200, 200);
}

// マウスが押されたら、色変数の値をランダムにする
function mousePressed() {
  r = random(255);
  g = random(255);
  b = random(255);
}
```
</details>

### 問題2
`keyPressed()` を使い、数字の `'1'` キーが押されたら背景が赤に、`'2'` キーが押されたら緑に、`'3'` キーが押されたら青に変わるスケッチを作成してください。

<details>
<summary>解答</summary>

```javascript
// 背景色を保存する変数
let bgColor;

function setup() {
  createCanvas(400, 400);
  bgColor = color(220); // 初期色はグレー
}

function draw() {
  background(bgColor);
}

function keyPressed() {
  if (key === '1') {
    bgColor = color(255, 0, 0); // 赤
  } else if (key === '2') {
    bgColor = color(0, 255, 0); // 緑
  } else if (key === '3') {
    bgColor = color(0, 0, 255); // 青
  }
}
```
</details>

### 問題3
（応用）`mouseIsPressed` と `line()` を使って、マウスをドラッグしている間だけ線が描ける、簡易的なお絵かきツールを作成してください。ヒント: `draw()` の中で、現在のマウス位置 `(mouseX, mouseY)` と、**1フレーム前**のマウス位置 `(pmouseX, pmouseY)` を結ぶ線を描きます。`pmouseX` と `pmouseY` もp5.jsの組み込み変数です。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
  background(255);
}

function draw() {
  // マウスが押されている間だけ
  if (mouseIsPressed === true) {
    strokeWeight(4);
    stroke(0);
    // 1フレーム前のマウス位置と現在のマウス位置を結ぶ
    line(pmouseX, pmouseY, mouseX, mouseY);
  }
}

// 'c'キーでクリアする機能を追加
function keyPressed() {
  if (key === 'c') {
    background(255);
  }
}
```
</details>