# 文字列の操作
Processingではタイマーなどで文字列を使うのだが、たまに「文字列を分割したい」といったように文字列を操作したくなる場面が出てくる。<br>
なので、文字列の操作について学んでおこう。

## String型の操作
String型には、文字列を操作する便利な関数がたくさんある。<br>
* `.split([分割に使う文字列])` ... 指定した文字で文字列を分割する
* `.substring([始めの文字数]) .substring([始めの文字数],[終わりの文字数])` ... 始めから終わりの1つ手前までの間の文字列を取り出す(終わりを指定しない場合、文字列の最後までが取り出される)
* `.replace([置き換える対象の文字列],[置き換える文字列])` ... 特定の文字列を置き換える
* `.indexOf([調べたい文字列])` ... 特定の文字列が何文字目から始まるのかを調べる
* `.contains([調べたい文字列])` ... 特定の文字列が含まれるか調べる
* `.length()` ... 文字列の文字数を取得する
* `.equals([別の文字列])` ... 文字列が**別の文字列と同じ文字列を持つか**を判定する

**これらの関数は「元の文字列の変数は変更せず、変更した後の文字列を返す」ということに注意!**

例:
```java
String s="ABCDEEFFF";

println(s.split("D"));//[ABC,EEFFF]と表示される

println(s.substring(2,4));//CDと表示される

println(s.replace("E","X"));//ABCDXXFFと表示される

println(s.indexOf("D"));//3と表示される

println(s.contains("W"));//falseと表示される

println(s.length());//9と表示される
```

### ==と.equals()の違い
先ほどStringには`.equals()`という関数があることを紹介したが、これはif文などで使う`==`と何が違うのだろうか。<br>
実行した結果を見てみよう。
```java
String s="Simple_shooting";

println(s==s);//true

println(s=="Simple_shooting");//false

println(s.equals("Simple_shooting"));//true
```
実は、`==`では文字列が一致するかを正確に判定することができない。<br>
詳しくはクラスの部分で説明するが、Processingにおいては`int`、`float`、`boolean`、`char`などの基本の型だけが特別に`==`で正確に内容が一致するかを調べることができ、それ以外の型では`.equals()`を使わないと正しく内容の一致を判定することができない。

## StringBuilder
Processing(本当はJava)にはStringBuilderというものがあり、String型ではできないような複雑な操作を行うことができる。<br>
StringBuilderは文字列を組み上げていく過程で使うのがいいだろう。<br>
StringBuilderには以下のような関数がある。
* `.append([繋げたい文字列])` ... 文字列を最後尾に繋げる
* `.insert([挿入したい位置],[挿入したい文字列])` ... 文字列を指定した位置に挿入する
* `.substring([]) .substring([],[])` ... Stringの`.substring()`と同じ
* `.deleteCharAt([削除したい文字の位置])` ... 指定した位置の文字を削除する
* `toString()` ... String型の文字列に変換する

**StringBuilderでは、`.substring()`以外は元の文字列を変更する。**

例:
```java
//newという構文は今はおまじないとして覚えておこう
StringBuilder b=new StringBuilder("Text");

println(b.append(" _(:3」∠)_"));//Text _(:3」∠)_

println(b.insert(4,"::"));//Text:: _(:3」∠)_

println(b.deleteCharAt(1));//Txt:: _(:3」∠)_
```