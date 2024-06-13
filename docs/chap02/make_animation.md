<link href="../css/original.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
# アニメーションを作る
この節では、Chapter2で学んだことを使ってアニメーションを作る。<br/>
<br/>
↓今回制作するアニメーション(再掲)
![animation](../img/chap02/chap02.gif)

## 必要な変数の初期化
今回のアニメーションでは右に動く図形と左に動く図形を描画するので、それぞれの位置や大きさ、色などを保存する配列を作成する必要がある。
<details class="accordion">
  <summary>初期化のコード(長いので折りたたみ)</summary>
  <pre>
<code class="lang-java">
//右向きに動く図形の情報
float[] right_x;
float[] right_y;
float[] right_size;
color[] right_color;

//左六kに動く図形の情報
float[] left_x;
float[] left_y;
float[] left_size;
color[] left_color;

//速度
float speed=1;

//図形の数
int rectangle_count=50;

void setup(){
  size(960,540);
  
  //色の指定方法を設定。
  //HSBはHue(色相)、Saturation(彩度)、Brightness(明るさ)で色を指定する。
  colorMode(HSB,360,100,100,255);
  
  right_x=new float[rectangle_count];
  right_y=new float[rectangle_count];
  right_size=new float[rectangle_count];
  right_color=new color[rectangle_count];
  
  left_x=new float[rectangle_count];
  left_y=new float[rectangle_count];
  left_size=new float[rectangle_count];
  left_color=new color[rectangle_count];
}</code>
  </pre>
</details>

## 図形の配置や色をランダムにする
初期化をしたは良いものの、このまま図形を動かすとお察しの通り図形が画面に描画されないという事態が発生する。<br/>
なので、初期化と同時に色や位置をばらす必要がある。<br/>
ここでようやくfor文によるループを使うので、腕試しに「右向きと左向きのそれぞれの位置(x,y)とサイズと色をランダムに決める」というプログラムを自分で考えてみるのもアリだろう。
<details class="accordion">
  <summary>腕試しをしたい人のために折り畳み</summary>
  <pre>
<code class="lang-java">
void setup(){
  size(960,540);
  
  colorMode(HSB,360,100,100,255);
  
  right_x=new float[rectangle_count];
  right_y=new float[rectangle_count];
  right_size=new float[rectangle_count];
  right_color=new color[rectangle_count];
  
  //ここでfor文
  for(int i=0;i&lt;rectangle_count;i++){
    right_size[i]=random(2,30);
    right_x[i]=random(0,width);
    right_y[i]=random(0,height);
    right_color[i]=get_color();
  }
  
  left_x=new float[rectangle_count];
  left_y=new float[rectangle_count];
  left_size=new float[rectangle_count];
  left_color=new color[rectangle_count];
  
  //ここでfor文
  for(int i=0;i&lt;rectangle_count;i++){
    left_size[i]=random(2,30);
    left_x[i]=random(0,width);
    left_y[i]=random(0,height);
    left_color[i]=get_color();
  }
}

color get_color(){
  return color(random(0,360),20,random(70,100),128);
}</code>
  </pre>
</details>

今回は色を決める処理を`get_color()`関数で実装した。

## 図形を動かす
これでようやくアニメーションをする準備ができたので、最後にアニメーションをさせるプログラムを書く。<br/>
最初に`speed`という変数を宣言しているので、for文と`speed`を使って図形を動かす。
<details class="accordion">
  <summary>アニメーションの折り畳み</summary>
  <pre>
<code class="lang-java">
void draw(){
  //今回はHSBで色を制御するので、Bで明るさのみを設定
  background(0,0,95);
  stroke(0,0,30);
  
  //右向きの図形を処理
  for(int i=0;i&lt;rectangle_count;i++){
    fill(right_color[i]);
    rect(right_x[i],right_y[i],right_size[i],right_size[i]);
    right_x[i]+=speed;
    //画面外に出たら左端に戻す
    if(right_x[i]&gt;width){
      right_x[i]=0;
    }
  }
  
  //左向きの図形を処理
  for(int i=0;i&lt;rectangle_count;i++){
    fill(left_color[i]);
    rect(left_x[i],left_y[i],left_size[i],left_size[i]);
    left_x[i]-=speed;
    //画面外に出たら右端に戻す
    if(left_x[i]&lt;0){
      left_x[i]=width;
    }
  }
}</code>
  </pre>
</details>

## プログラム全文
<details class="accordion">
  <summary>今回のプログラム</summary>
  <pre>
<code class="lang-java">float[] right_x;
float[] right_y;
float[] right_size;
color[] right_color;

float[] left_x;
float[] left_y;
float[] left_size;
color[] left_color;

float speed=1;

int rectangle_count=50;

void setup(){
  size(960,540);
  
  colorMode(HSB,360,100,100,255);
  
  right_x=new float[rectangle_count];
  right_y=new float[rectangle_count];
  right_size=new float[rectangle_count];
  right_color=new color[rectangle_count];
  
  for(int i=0;i&lt;rectangle_count;i++){
    right_size[i]=random(2,30);
    right_x[i]=random(0,width);
    right_y[i]=random(0,height);
    right_color[i]=get_color();
  }
  
  left_x=new float[rectangle_count];
  left_y=new float[rectangle_count];
  left_size=new float[rectangle_count];
  left_color=new color[rectangle_count];
  
  for(int i=0;i&lt;rectangle_count;i++){
    left_size[i]=random(2,30);
    left_x[i]=random(0,width);
    left_y[i]=random(0,height);
    left_color[i]=get_color();
  }
}

void draw(){
  background(0,0,95);
  stroke(0,0,30);
  
  for(int i=0;i&lt;rectangle_count;i++){
    fill(right_color[i]);
    rect(right_x[i],right_y[i],right_size[i],right_size[i]);
    right_x[i]+=speed;
    if(right_x[i]&gt;width){
      right_x[i]=0;
    }
  }
  
  for(int i=0;i&lt;rectangle_count;i++){
    fill(left_color[i]);
    rect(left_x[i],left_y[i],left_size[i],left_size[i]);
    left_x[i]-=speed;
    if(left_x[i]&lt;0){
      left_x[i]=width;
    }
  }
}

color get_color(){
  return color(random(0,360),20,random(70,100),128);
}</code>
  </pre>
</details>

## Chapter2のまとめ
Chapter2では、主にアニメーションをすることに重点を置いて配列やfor文やランダムなどといった構文を紹介した。<br/>
これらの構文はこの先もずっと出てくるので、もし分からなくなったらもう一度Chapter2に戻って確実に使えるようになってほしい。