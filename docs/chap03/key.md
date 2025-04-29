# キーボードで操作する

## 押されているキーを取得
現在押しているキーの情報は`key`(char型)と`keyCode`(int型)という変数に自動で代入される。
```java
// void setup() { ... }
void draw(){
  println(key);//最後に押されたキーが文字として表示される
  println(keyCode);//最後に押されたキーが数字として表示される
}
```

## キーに関する関数
キーにもマウスと同様に押されているかなどを判定する関数などがある。
* `keyPressed`変数 ... boolean型で、キーが押されている間trueになる
* `keyPressed`関数 ... キーが押されたときに呼び出される
* `keyReleased`関数 ... キーが離されたときに呼び出される

```java
// void setup() { ... }
void draw(){
  background(30);
  //キーを押している間画面が明るくなる
  if(keyPressed)background(230);
}

void keyPressed(){
  //キーを押した瞬間だけ図形が描画される
  fill(90);
  noStroke();
  rect(0,0,100,100);
}

void keyReleased(){
  //キーを離した瞬間だけ図形が描画される
  fill(170);
  noStroke();
  rect(0,0,100,100);
}
```

キーボードでもマウスと同様にキーを押したときだけtrueになる変数を作ることができる。<br>
内容は同じなので割愛。

## その他の入力
* `keyTyped`関数 ... キーをタイプしたときに呼び出される。タイミングは`keyReleased`と同じ

## それ、本当に文字ですか?
最初に紹介した`key`変数だが、ShiftやCtrl、Backspaceなどといった文字では表せないものが代入されることがある。<br>
そのような文字は通常どう頑張っても表示できないので、本当に文字であるかを判定する方法を教える。
```java
if(key!=CODED)println("this is a key:"+key);
```
このようにすると、文字ではない値を除くことができる。<br>
仕組みとしては、文字では表せない`key`と同じ内容を持つ`CODED`と比較することで、文字で表せない場合は処理をスキップしている。