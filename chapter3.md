# 第3章: 色とスタイル

前の章では図形の形と位置を学びましたが、すべての図形は白い塗りと黒い線で描かれていました。この章では、図形に色をつけたり、線の太さを変えたりする方法を学び、表現の幅を広げます。

## 3.1 色の指定方法

p5.jsでは、主に2つの方法で色を指定します。

### グレースケール
0から255までの1つの数値で、黒から白までの明るさを表現します。
- `0`: 黒
- `127`: グレー
- `255`: 白

### RGBカラー
光の三原色である赤(Red)、緑(Green)、青(Blue)の組み合わせで色を表現します。それぞれの色の強さを0から255までの数値で指定します。

` (R, G, B) `

- `(255, 0, 0)`: 赤
- `(0, 255, 0)`: 緑
- `(0, 0, 255)`: 青
- `(255, 255, 0)`: 黄 (赤と緑のミックス)
- `(0, 0, 0)`: 黒
- `(255, 255, 255)`: 白

## 3.2 背景、塗り、線の設定

### 背景色: `background()`

`background()`は、すでに第1章で使いました。キャンバス全体を特定の色で塗りつぶします。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  // 背景を青色にする
  background(50, 100, 200);
  
  ellipse(200, 200, 100, 100);
}
```

### 塗りの色: `fill()` と `noFill()`

`fill()`は、これ以降に描かれる図形の「塗り」の色を設定します。`noFill()`を使うと、図形は塗りつぶされなくなります（透明になります）。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 塗りを赤色に設定
  fill(255, 0, 0);
  // この円は赤色で塗りつぶされる
  ellipse(100, 200, 100, 100);
  
  // 塗りをなくす
  noFill();
  // この円は塗りつぶされない
  ellipse(300, 200, 100, 100);
}
```

### 線の色と太さ: `stroke()`, `noStroke()`, `strokeWeight()`

- `stroke()`: これ以降に描かれる図形の「線（枠線）」の色を設定します。
- `noStroke()`: 図形の線をなくします。
- `strokeWeight()`: 線の太さをピクセル単位で設定します。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 線の色を緑に、太さを10ピクセルに設定
  stroke(0, 255, 0);
  strokeWeight(10);
  // この四角形は太い緑色の線で描かれる
  rect(50, 50, 100, 100);
  
  // 線をなくす
  noStroke();
  // この四角形は線なしで描かれる
  rect(250, 250, 100, 100);
}
```

## 3.3 スタイルの適用順序

**非常に重要なルール:** `fill()` や `stroke()` などのスタイル設定は、一度設定されると、**それ以降に描画されるすべての図形に適用され続けます**。別のスタイルを適用するには、再度 `fill()` や `stroke()` を呼び出す必要があります。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 1つ目の円: 赤い塗り、線なし
  fill(255, 0, 0); // 塗りを赤に
  noStroke();      // 線をなしに
  ellipse(100, 200, 100, 100);
  
  // 2つ目の円: 青い塗り、黒い線
  fill(0, 0, 255); // 塗りを青に
  stroke(0);       // 線を黒に
  strokeWeight(1); // 太さを1に戻す
  ellipse(300, 200, 100, 100);
}
```

---

## 章末問題

### 問題1
キャンバスの中央に、**黄色い塗り**で、**太さ5ピクセルの紫色の線**を持つ円を描いてみましょう。
- 黄色: `(255, 255, 0)`
- 紫色: `(128, 0, 128)`

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 塗りを黄色に設定
  fill(255, 255, 0);
  // 線の色を紫色に設定
  stroke(128, 0, 128);
  // 線の太さを5に設定
  strokeWeight(5);
  
  // 中央に円を描画
  ellipse(200, 200, 150, 150);
}
```
</details>

### 問題2
`noStroke()` を使って、線がない四角形を3つ描きましょう。それぞれ、赤、緑、青の色で塗りつぶしてください。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 線をなくす（最初に一度設定すればOK）
  noStroke();
  
  // 1. 赤い四角形
  fill(255, 0, 0);
  rect(50, 150, 80, 80);
  
  // 2. 緑の四角形
  fill(0, 255, 0);
  rect(160, 150, 80, 80);
  
  // 3. 青い四角形
  fill(0, 0, 255);
  rect(270, 150, 80, 80);
}
```
</details>

### 問題3
`noFill()` を使って、塗りつぶしのない図形を2つ描きましょう。
1. 1つ目は、太さ10の赤い線で描いた円。
2. 2つ目は、1つ目の円の上に、太さ3の青い線で描いた四角形。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 塗りつぶしは使わない
  noFill();
  
  // 1. 赤い円
  stroke(255, 0, 0);
  strokeWeight(10);
  ellipse(200, 200, 150, 150);
  
  // 2. 青い四角形
  stroke(0, 0, 255);
  strokeWeight(3);
  rect(150, 150, 100, 100);
}
```
</details>