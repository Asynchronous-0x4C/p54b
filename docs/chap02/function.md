<script type="text/javascript" async src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.7/MathJax.js?config=TeX-MML-AM_CHTML">
</script>
<script type="text/x-mathjax-config">
 MathJax.Hub.Config({
 tex2jax: {
 inlineMath: [['$', '$'] ],
 displayMath: [ ['$$','$$'], ["\\[","\\]"] ]
 }
 });
</script>

# 関数ってなに？
>コンピュータプログラミングにおいて、プログラム中で意味や内容がまとまっている作業をひとつの手続きとしたものである。-Wikipediaより

## もっと簡単に
引用した内容を簡単に説明すると、関数は複数の処理をまとめて再利用できるようにしたものと言える。<br>
例えるなら、お金を入れてスイッチを押せばあとは自動で飲み物が出てくる自販機のようなもの。

## 引数と戻り値
関数には引数と戻り値というものが存在する。
- 引数 ... 関数に渡す値。自販機ではお金や押すスイッチといった飲み物を買うのに必要な情報にあたる。
- 戻り値 ... 関数が返す値。自販機では結果出てくる飲み物に当たる。

## 宣言する
```java
[戻り値の型] [名前]([引数]){
  //処理
  return [戻り値];//戻り値の型がvoidの場合は必要ない。
}

//以下例
//戻り値なし、引数なし
void example1(){
  rect(10,10,30,30);
  ellipse(60,60,40,40);
}

//戻り値なし、引数あり
void example2(float x,float y){//","で区切ると複数の引数をとることができる
  rect(x,y,10,10);
}

//戻り値あり、引数あり
float example3(float x,float y,float z){
  return x*y+z;
}
```
## 関数を使う
基本的には以下の通りになる
```java
[関数名]([引数]);//引数には変数も使える

//変数に戻り値を代入する場合
[変数]=[関数名]([引数]);

//以下例
//代入なし、引数なし
example1();

//代入なし、引数あり
float a=50;
example2(30,a);

//代入あり、引数あり
float a=23;
float result;
result=example3(a,12,30);//resultには306が代入される
```
上の例から分かる通り、前に紹介したrect()やellipse()も立派な関数である。
## 関数の上手な使い方
プログラム中でよく出てくる割に長い処理を纏めるときや、図形を表示する処理と計算する処理を分け、分かりやすくするときなどに使うと効果的。