# 図形の描画

`セミコロン ; を忘れずに！`

## 線を引く

```java
line(x1, y1, x2, y2);
```

- x1, y1：始点の座標
- x2, x2：終点の座標

## 四角を描く

```java
rect(x, y, w, h);
```

- x：x座標
- y：y座標
- w：横幅
- h：高さ

![square](../img/chap01/square.png)


## 円を描く

```java
ellipse(x, y, w, h);
```

- w：x方向（横）の直経
- h：y方向（縦）の直径

![ellipse](../img/chap01/ellipse.png)


## 三角形を描く

```java
triangle(x1, y1, x2, y2, x3, y3);
```

### サンプル

```java
size(400, 400);
triangle(200, 20, 40, 300, 300, 350);
```

![triangle](../img/chap01/triangle.png)

基本はこの４つ。

## 補足

あとに描いた図形が下の図形を上書きする。

![plus_alpha](../img/chap01/some_shape.png)
