# 拡張for文
Chapter02でfor文を習ったのを覚えているだろうか。
<br>実はfor文で配列を扱う場合、さらに簡潔に書くことができる。
<br>書き方は、

```java
for([配列の型]　[変数名]:[配列名]){
  //処理
}
```
となる。

## 配列

配列の要素を2倍する例を拡張for文にすると、以下のようになる。

```java
int[] array={10,20,30,40,50};
int count=0;

for(int i:array){//iに要素が順番に代入される
  array[count]=i*2;
  count++;
}

println(array);//{20,40,60,80,100}
```

<br>ただ、上の例のようにループした回数が必要になる場合は、普通のfor文を使用する方がよい。
<br>なので、拡張for文の使いどころとしては、配列の要素を変更しない処理が最適である。

## ArrayList

実は、先ほど学んだArrayListも拡張for文で書くことができる。

```java
ArrayList<Float>float_list=new ArrayList<Float>();

for(int i=0;i<100;i++){
  float_list.add(random(0,100));//ランダムな数値で初期化
}

for(float f:float_list){
  println(f);//float_list内のすべての要素を表示
}
```

このように、配列の変数の部分をArrayListの変数に変えるだけで拡張for文を使うことができる。<br>
今回は配列とArrayListの例を紹介したが、他にもHashMapやHashSetなど色々なもので拡張for文が使えるので調べてみてほしい。