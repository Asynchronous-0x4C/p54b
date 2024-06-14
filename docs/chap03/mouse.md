# マウスからの入力

## カーソル

現在のマウスカーソルの座標が`mouseX`, `mouseY`という変数に自動で代入されている。
これを以下のように使用できる。

```java
// void setup() { ... }
void draw() {
  background(225);
  ellipse(mouseX, mouseY, 20, 20);
}
```

## マウスボタン

* `mousePressed`変数 ... boolean型で、マウスが押されている間trueになる。
* `mousePressed`関数 ... マウスが押されたときに呼び出される
* `mouseReleased`関数 ... マウスが離されたときに呼び出される

```java
//void setup() { ... }
void draw() {
  //マウスを押しているときだけ背景が白になる
  if(mousePressed){
    background(225);
  }else{
    background(30);
  }
}

void mousePressed(){
  //マウスを押した瞬間だけ図形が描画される
  fill(200,100,100);
  noStroke();
  rect(0,0,100,100);
}

void mouseReleased(){
  //マウスを離した瞬間だけ図形が描画される
  fill(100,100,200);
  noStroke();
  rect(0,0,100,100);
}
```

`mousePressed`関数と`mouseReleased`関数は必ず`viod draw()`の後に実行されるので、マウスを押したときだけtrueになる変数を作ることができる。<br/>
このように「何かをした瞬間だけtrueになる」変数は、ボタンなどのUI(User Interface)を作る時に重宝する。

```java
//変数を宣言
boolean mousePress=false;

//void setup() { ... }

void draw(){
  //処理

  //全ての処理が終了したらfalseに戻す
  mousePress=false;
}

void mousePressed(){
  //押されたときにtrueになる
  mousePress=true;
}
```

## その他の入力

* `mouseButton`変数 ... int型で、押されたマウスのボタンの番号(`LEFT`,`RIGHT`,`CENTER`)を保持する。
* `mouseMoved`関数 ... マウスが動かされたときに呼び出される
* `mouseClicked`関数 ... マウスがクリックされたときに呼び出される(`mouseReleased`関数と同じタイミング)
* `mouseDragged`関数 ... マウスがドラッグ(ボタンを押しながら動かす)されたときに呼び出される
* `mouseWheel`関数 ... マウスホイールが回されたときに呼び出される。このとき、引数を設定[^1]すれば回された向きを取得できる。

---

[^1]:`void mouseWheel(MouseEvent event){}`