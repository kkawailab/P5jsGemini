# 第5章: 繰り返しと条件分岐

これまでの章で、図形を描いたり、色をつけたり、変数で動きをつけたりする方法を学びました。この章では、プログラムの流れをコントロールするための2つの重要な仕組み、「繰り返し（ループ）」と「条件分岐」を学びます。これらをマスターすれば、より複雑で面白い表現が可能になります。

## 5.1 繰り返し処理: `for`ループ

同じ、あるいは少しずつ違う処理を何度も繰り返したいとき、「ループ」を使います。例えば、円を100個描きたいときに、`ellipse()`を100回書くのは大変です。`for`ループを使えば、数行で実現できます。

### `for`ループの構文

`for`ループは、特定の回数だけ処理を繰り返すための基本的な構文です。

```javascript
for (let i = 0; i < 10; i++) {
  // この中の処理が10回繰り返される
}
```

`()`の中は3つの部分に分かれています。
1.  **初期化 (`let i = 0;`)**: ループが始まる前に一度だけ実行されます。カウンターとして使う変数 `i` を宣言し、`0` を代入しています。
2.  **条件 (`i < 10;`)**: ループの中の処理を実行する前に、この条件がチェックされます。条件が真 (`true`) の間、ループは続きます。この例では、`i` が `10` より小さい間、繰り返されます。
3.  **更新 (`i++`)**: ループの中の処理が終わるたびに実行されます。`i++` は `i = i + 1` と同じ意味で、カウンター変数 `i` の値を1ずつ増やします。

この結果、`i` の値は `0, 1, 2, 3, 4, 5, 6, 7, 8, 9` と変化し、`{}` の中の処理が10回実行されます。

### `for`ループの使用例

`for`ループを使って、たくさんの円を横一列に並べてみましょう。

```javascript
function setup() {
  createCanvas(500, 200);
}

function draw() {
  background(220);
  
  // iが0から9まで10回繰り返す
  for (let i = 0; i < 10; i++) {
    // 円のx座標を i を使って計算する
    // iが0のとき x=25, iが1のとき x=75, ... となる
    let x = 25 + i * 50;
    let y = 100;
    let size = 40;
    
    fill(255, 100, 150);
    noStroke();
    ellipse(x, y, size, size);
  }
}
```

## 5.2 条件分岐: `if`文

「もし〜ならば、Aの処理をする。そうでなければ、Bの処理をする」というように、条件によってプログラムの実行内容を変えたいとき、「条件分岐」を使います。そのための最も基本的な構文が `if`文です。

### `if`文の構文

`if (条件) { ... }`
`()` の中の条件式が真 (`true`) の場合に、`{}` の中の処理が実行されます。

条件式には、**比較演算子**を使います。
- `a > b` (aはbより大きい)
- `a < b` (aはbより小さい)
- `a >= b` (aはb以上)
- `a <= b` (aはb以下)
- `a === b` (aとbは等しい) ※`=`が3つなのに注意！
- `a !== b` (aとbは等しくない)

### `else` と `else if`

- `else`: `if`の条件が偽 (`false`) だった場合の処理を記述します。
- `else if`: 最初の`if`の条件が偽だった場合に、さらに別の条件で分岐させたいときに使います。

```javascript
if (mouseX > width / 2) {
  // マウスが右半分にあれば、Aの処理
} else {
  // そうでなければ（左半分にあれば）、Bの処理
}
```

### `if`文の使用例

マウスカーソルの位置によって、背景色を変えるスケッチです。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  // もしマウスのx座標がキャンバスの幅の半分より大きいなら
  if (mouseX > width / 2) {
    // 背景を水色にする
    background(173, 216, 230);
  } else {
    // そうでなければ（半分より小さいなら）、背景を薄いピンクにする
    background(255, 182, 193);
  }
  
  // マウスの位置に円を描く
  ellipse(mouseX, mouseY, 50, 50);
}
```

---

## 章末問題

### 問題1
`for`ループを使って、画面の端から端まで、10ピクセルごとに垂直な線を20本描いてみましょう。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  stroke(150);
  
  // iを0から19まで20回繰り返す
  for (let i = 0; i < 20; i++) {
    // 線のx座標を計算
    let x = 20 + i * 20;
    
    // 上から下へ線を引く
    line(x, 0, x, height);
  }
}
```
</details>

### 問題2
ボールが画面の右端に到達したら、左端に戻る、という動きを`if`文を使って実装してみましょう。（第4章の円が動くアニメーションを改造します）

<details>
<summary>解答</summary>

```javascript
let circleX = 0;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  ellipse(circleX, 200, 50, 50);
  
  circleX = circleX + 2;
  
  // もしcircleXが画面の幅を超えたら
  if (circleX > width) {
    // circleXを0に戻す
    circleX = 0;
  }
}
```
</details>

### 問題3
`if`文の条件式で、p5.jsの組み込み変数 `mouseIsPressed` を使ってみましょう。この変数は、マウスボタンが押されている間だけ `true` になります。マウスが押されているときだけ、円が大きくなるスケッチを作成してください。

<details>
<summary>解答</summary>

```javascript
let circleSize = 50;

function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // もしマウスが押されていたら
  if (mouseIsPressed === true) {
    // 円のサイズを大きくする
    circleSize = circleSize + 1;
  }
  
  ellipse(width / 2, height / 2, circleSize, circleSize);
}
```
</details>