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
