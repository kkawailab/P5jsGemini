# 第6章: 関数

私たちはこれまで、`setup()` や `draw()` といった「関数」を当たり前のように使ってきました。これらはp5.jsが特別に用意した関数ですが、実は自分でオリジナルの関数を作ることができます。関数を使いこなすことで、コードが整理され、再利用しやすくなり、より複雑なプログラムを効率的に書けるようになります。

## 6.1 関数とは？

関数とは、**特定の処理をひとまとめにし、名前をつけたもの**です。言わば、プログラムの「部品」です。

例えば、「顔を描く」という処理には、輪郭の円、2つの目、口の線を描く、といった複数のステップが含まれます。これらを一つの `drawFace` という関数にまとめておけば、`drawFace()` と一行書くだけで、いつでも顔を描くことができるようになります。

### 関数を使うメリット
- **再利用性**: 同じ処理を何度も書きたいとき、関数を一度定義しておけば、その名前を呼び出すだけで済みます。
- **可読性（読みやすさ）**: `draw()` の中にたくさんのコードが書かれていると、何をしているのか分かりにくくなります。処理を関数に分けることで、`draw()` の中が `drawPlayer();` `drawEnemies();` `drawScore();` のようにスッキリし、プログラム全体の流れが追いやすくなります。
- **保守性**: 例えば「目の色を変えたい」と思ったとき、関数を使っていれば、その関数の中だけを修正すれば、すべての描画に反映されます。

## 6.2 関数の作り方と使い方

関数は「定義」と「呼び出し」の2つのステップで使います。

### 関数の定義

`function` キーワードに続けて、好きな関数名をつけ、`()` と `{}` を書きます。`{}` の中に、実行したい処理を記述します。

```javascript
// 「drawRobot」という名前の関数を定義する
function drawRobot() {
  // 体
  rect(150, 150, 100, 100);
  // 頭
  ellipse(200, 100, 80, 80);
  // 目
  point(180, 90);
  point(220, 90);
  // 口
  line(190, 110, 210, 110);
}
```

### 関数の呼び出し

定義した関数は、`draw()` の中など、好きな場所から `関数名()` の形で呼び出すことができます。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 上で定義した drawRobot 関数を呼び出す
  drawRobot();
}

// --- 自作関数の定義はここから ---
function drawRobot() {
  // 体
  rect(150, 150, 100, 100);
  // 頭
  ellipse(200, 100, 80, 80);
  // 目
  point(180, 90);
  point(220, 90);
  // 口
  line(190, 110, 210, 110);
}
```

## 6.3 引数（ひきすう）で、もっと便利に

先ほどの `drawRobot()` は、いつも同じ場所に同じロボットを描くことしかできません。もし、違う場所に、違うサイズや色で描きたい場合はどうすればよいでしょうか？そこで登場するのが**引数（ひきすう）**です。

引数とは、関数を呼び出すときに、関数に情報を渡すための特別な変数です。

### 引数のある関数の定義

関数名の後の `()` の中に、受け取りたい情報の名前（引数名）をカンマで区切って書きます。

```javascript
// x座標, y座標, 色 を引数として受け取る関数
function drawRobot(x, y, bodyColor) {
  // 体
  fill(bodyColor);
  rect(x, y, 100, 100);
  // 頭 (体の位置からの相対位置で描く)
  fill(200);
  ellipse(x + 50, y - 50, 80, 80);
  // ...以下略
}
```

### 引数のある関数の呼び出し

呼び出すときに、`()` の中に渡したい具体的な値（データ）を書きます。

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  // 1体目のロボット: (50, 150)の位置に、赤色で描画
  drawRobot(50, 150, color(255, 0, 0));
  
  // 2体目のロボット: (250, 200)の位置に、青色で描画
  drawRobot(250, 200, color(0, 0, 255));
}

// --- 自作関数の定義 ---
function drawRobot(x, y, bodyColor) {
  noStroke();
  // 体
  fill(bodyColor);
  rect(x, y, 100, 100);
  // 頭
  fill(200);
  ellipse(x + 50, y - 50, 80, 80);
  // 目
  stroke(0);
  point(x + 30, y - 60);
  point(x + 70, y - 60);
}
```
`color()` はp5.jsの関数で、RGB値を色データに変換します。

---

## 章末問題

### 問題1
`x`, `y`, `size` の3つの引数を受け取り、その位置に、指定された `size` で花を描く `drawFlower(x, y, size)` という関数を定義してください。花のデザインは自由です（例：中央の円と、その周りの複数の円）。

<details>
<summary>解答例</summary>

```javascript
function setup() {
  createCanvas(400, 400);
  drawFlower(200, 200, 100); // テストで呼び出してみる
}

function draw() {
  // この問題ではdrawは空でもOK
}

// 花を描く関数
function drawFlower(x, y, size) {
  // 花の中心
  fill(255, 255, 0); // 黄色
  noStroke();
  ellipse(x, y, size * 0.5, size * 0.5);
  
  // 花びら (5枚)
  fill(255, 100, 150, 200); // 半透明のピンク
  ellipse(x - size * 0.3, y - size * 0.3, size * 0.4, size * 0.4);
  ellipse(x + size * 0.3, y - size * 0.3, size * 0.4, size * 0.4);
  ellipse(x - size * 0.3, y + size * 0.3, size * 0.4, size * 0.4);
  ellipse(x + size * 0.3, y + size * 0.3, size * 0.4, size * 0.4);
  ellipse(x, y, size * 0.4, size * 0.4);
}
```
</details>

### 問題2
問題1で作成した `drawFlower()` 関数を `for` ループの中で呼び出し、画面下部に沿って、大きさの違う花を5つ描いてみましょう。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(500, 400);
}

function draw() {
  background(220);
  
  for (let i = 0; i < 5; i++) {
    let x = 50 + i * 100;
    let y = 350;
    let size = 30 + i * 10; // 少しずつ大きくする
    drawFlower(x, y, size);
  }
}

// (問題1のdrawFlower関数をここにコピーする)
function drawFlower(x, y, size) {
  // ... (中身は同じ)
}
```
</details>

### 問題3
`draw()` の中で、`mouseX` の値に応じてサイズが変わり、`mouseY` の値に応じて色が変わるような `drawFlower()` を呼び出し続けてみましょう。インタラクティブな花を描画できます。

<details>
<summary>解答</summary>

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  background(220);
  
  let size = mouseX; // x座標でサイズを決定
  let r = mouseY % 255; // y座標で赤の強さを決定
  
  // 花を描く（色は解答例のものを少し変更）
  noStroke();
  fill(r, 100, 150, 200);
  ellipse(width/2 - size * 0.3, height/2 - size * 0.3, size * 0.4, size * 0.4);
  ellipse(width/2 + size * 0.3, height/2 - size * 0.3, size * 0.4, size * 0.4);
  ellipse(width/2 - size * 0.3, height/2 + size * 0.3, size * 0.4, size * 0.4);
  ellipse(width/2 + size * 0.3, height/2 + size * 0.3, size * 0.4, size * 0.4);
  
  fill(255, 255, 0);
  ellipse(width/2, height/2, size * 0.5, size * 0.5);
}

// この解答では、drawFlower関数を定義せず、直接draw()の中にロジックを書いています。
// もちろん、drawFlower(width/2, height/2, mouseX, color(mouseY % 255, 100, 150)); のように
// 関数を呼び出す形でも実装できます。
```
</details>