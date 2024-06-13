<link href="../css/original.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>

# マウスを使った作品を作る

<details class="accordion">
  <summary>全体のコード</summary>
  <pre>
<code class="lang-java">
float circle_x;
float circle_y;
float circle_size=20;

void setup(){
  size(960,540);
  set_circle_position();
}

void draw(){
  background(30);
  fill(200,50);
  stroke(200);
  circle(circle_x,circle_y,circle_size);
  textAlign(CENTER);
  textSize(13);
  fill(200);
  if(circle_y>height*0.5){
    text("Click here!",circle_x,circle_y-circle_size);
  }else{
    text("Click here!",circle_x,circle_y+circle_size*1.3);
  }
}

void mousePressed(){
  if(dist(circle_x,circle_y,mouseX,mouseY)<=circle_size*0.5)set_circle_position();
}

void set_circle_position(){
  circle_x=random(circle_size*0.5,width-circle_size*0.5);
  circle_y=random(circle_size*0.5,height-circle_size*0.5);
}</code>
  </pre>
</details>