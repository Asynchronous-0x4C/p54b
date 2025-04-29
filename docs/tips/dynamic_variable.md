# 動的に変化する変数?
たとえば、こんなふうに図形を描画するクラスを定義したとする。

```Java
class Shape{
  float x;
  float y;
  float width;
  float height;

  Shape(float x,float y,float width,float height){
    this.x=x;
    this.y=y;
    this.width=width;
    this.height=height;
  }

  void display(){
    fill(30);
    noStroke();
    rectMode(CENTER);
    rect(x,y,width,height);
  }
}
```

このクラスを使って画面の半分の大きさの図形を中央に描画するとなると、こんなふうになるだろう。

```Java
Shape shape;

void setup(){
  //各種設定

  shape=new Shape(width*0.5,height*0.5,width*0.5,height*0.5);
}

void draw(){
  //いろんな描画

  shape.display();
}
```

普通のプログラムでは何も困ることは無いのだが、ウィンドウのサイズが変わるようなプログラムを作る際にはちょっとした不都合なことが発生する。<br>
それは、**ウィンドウのサイズが変化しても図形のサイズは変化しない**ということだ。

それもそのはず、`Shape`クラスに渡しているのは単なる`int`型の`width`、`height`という変数であるから、元の値が変更されたとしてもそれを`Shape`クラスが知る由もない。

このように、変数を動的に更新したいという場面はたびたび起こる。<br>
そして、この問題を解決するのが、**関数型インターフェース**というものだ。

## 関数型インターフェース
詳しくは[ここ](../theory/class.html)で解説するが、Processing(Java)には「関数型インターフェース」という、関数をあたかも変数のように扱うことができる仕組みがある。

そして、標準では主にこのような種類のものを使うことができる

|名前|引数|戻り値|
|----|----|-----|
|`Runnable`|0個|0個|
|`Supplier`|0個|1個|
|`Consumer`|1個|0個|
|`Function`|1個|1個|
|`BiConsumer`|2個|2個|
|`BiFunction`|2個|1個|

使い方としては、以下のようになる。

```Java
//必要なパッケージをインポート
import java.util.function.*;

//引数をとらず、float型を返す関数型インターフェース
//ラムダ式という記法で簡単に初期化できる
Supplier<Float> supply=()=>{
  return 10;
};

println(supply.get())//10 と表示される
```

コードを追ってみると、結局のところ関数型インターフェースというのは純粋な関数ではなく、単にメソッドを1つ持ったクラスであることが分かるだろう。

ここまでで関数型インターフェースというものがどんなものなのか何となく分かったと思う。<br>
なので、次はこれを使って問題を解決してみる。

まずはクラスの定義から。

```Java
import java.util.function.*;

class Shape{
  Supplier<Float> x;
  Supplier<Float> y;
  Supplier<Float> width;
  Supplier<Float> height;

  Shape(Supplier<Float> x,Supplier<Float> y,Supplier<Float> width,Supplier<Float> height){
    this.x=x;
    this.y=y;
    this.width=width;
    this.height=height;
  }

  void display(){
    fill(30);
    noStroke();
    rectMode(CENTER);
    rect(x.get(),y.get(),width.get(),height.get());
  }
}
```

今回、ひとまず全ての変数を`Supplier<Float>`に置き換えた。

次に、プログラム本体を書き換える。

```Java
import java.util.function.*;

Shape shape;

void setup(){
  //各種設定

  shape=new Shape(()=>{return width*0.5},()=>{return height*0.5},()=>{return width*0.5},()=>{return height*0.5});
}

void draw(){
  //いろんな描画

  shape.display();
}
```

少し長くなってしまったが、こんなふうに変更することで、ウィンドウのサイズを変えてもちゃんと比率が保たれるようになる。