<link href="../css/original.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>

# 万有引力を使ったゲームを作る

<details class="accordion">
  <summary>全体のコード</summary>
  <pre>
<code class="lang-java">
PVector[] asteroid;
PVector[] asteroid_v;
float[] asteroid_m;
boolean[] asteroid_l;
float asteroid_mass=7.34e2;

PVector[] star;
PVector[] star_v;
float[] star_m;
boolean[] star_l;
float star_mass=5.97e4;

PVector[] blackhole;
PVector[] blackhole_v;
float[] blackhole_m;
boolean[] blackhole_l;
float blackhole_mass=4.97e8;

PVector[] target;
PVector[] target_v;
float[] target_m;
boolean[] target_l;
float target_mass=1;

int object_count=100;

PVector click_point;

final float G=6.67e-7;

void setup(){
  size(1280,720);
  
  asteroid=new PVector[object_count];
  asteroid_v=new PVector[object_count];
  asteroid_m=new float[object_count];
  asteroid_l=new boolean[object_count];
  
  for(int i=0;i&lt;object_count;i++){
    asteroid[i]=new PVector();
    asteroid_v[i]=new PVector();
  }
  
  star=new PVector[object_count];
  star_v=new PVector[object_count];
  star_m=new float[object_count];
  star_l=new boolean[object_count];
  
  for(int i=0;i&lt;object_count;i++){
    star[i]=new PVector();
    star_v[i]=new PVector();
  }
  
  blackhole=new PVector[object_count];
  blackhole_v=new PVector[object_count];
  blackhole_m=new float[object_count];
  blackhole_l=new boolean[object_count];
  
  for(int i=0;i&lt;object_count;i++){
    blackhole[i]=new PVector();
    blackhole_v[i]=new PVector();
  }
  
  set_target("blackhole");
  
  click_point=new PVector();
  
  preset();
}

void draw(){
  noStroke();
  fill(30,100);
  rect(0,0,width,height);
  
  fill(230);
  display(asteroid,asteroid_v,asteroid_l,5);
  fill(230,100,100);
  display(star,star_v,star_l,15);
  fill(0);
  display(blackhole,blackhole_v,blackhole_l,50);
  
  calc_gravity(asteroid,asteroid_v,asteroid_l);
  calc_gravity(star,star_v,star_l);
  calc_gravity(blackhole,blackhole_v,blackhole_l);
  
  if(mousePressed){
    PVector mouse=new PVector(mouseX,mouseY);
    mouse.sub(click_point);
    float radius=mouse.mag();
    
    noFill();
    stroke(240);
    ellipse(click_point.x,click_point.y,radius*2,radius*2);
    line(click_point.x,click_point.y,mouseX,mouseY);
  }
}

void mousePressed(){
  click_point.set(mouseX,mouseY);
}

void mouseReleased(){
  PVector release_point=new PVector(mouseX,mouseY);
  release_point.sub(click_point);
  release_point.mult(0.25);
  
  for(int i=0;i&lt;object_count;i++){
    if(!target_l[i]){
      target[i].set(mouseX,mouseY);
      target_v[i].set(release_point);
      target_m[i]=target_mass*random(1,1.5);
      target_l[i]=true;
      return;
    }
  }
}

void keyPressed(){
  switch(key){
    case 'a':set_target("asteroid");break;
    case 's':set_target("star");break;
    case 'b':set_target("blackhole");break;
  }
}

void set_target(String type){
  switch(type){
    case "asteroid":
      target=asteroid;
      target_v=asteroid_v;
      target_m=asteroid_m;
      target_l=asteroid_l;
      target_mass=asteroid_mass;
      break;
    case "star":
      target=star;
      target_v=star_v;
      target_m=star_m;
      target_l=star_l;
      target_mass=star_mass;
      break;
    case "blackhole":
      target=blackhole;
      target_v=blackhole_v;
      target_m=blackhole_m;
      target_l=blackhole_l;
      target_mass=blackhole_mass;
      break;
  }
}

void display(PVector[] a,PVector[] a_v,boolean[] a_l,float size){
  for(int i=0;i&lt;object_count;i++){
    if(a_l[i]){
      PVector p=a[i];
      ellipse(p.x,p.y,size,size);
      a[i].add(a_v[i]);
    }
  }
}

void calc_gravity(PVector[] a,PVector[] a_v,boolean[] a_l){
  for(int i=0;i&lt;object_count;i++){
    if(!a_l[i])continue;
    for(int j=0;j&lt;object_count;j++){
      if(!asteroid_l[j])continue;
      if(a==asteroid&&i==j)continue;
      a_v[i]=get_vector(a_v[i],a[i],asteroid[j],asteroid_m[j]);
    }
    for(int j=0;j&lt;object_count;j++){
      if(!star_l[j])continue;
      if(a==star&&i==j)continue;
      a_v[i]=get_vector(a_v[i],a[i],star[j],star_m[j]);
    }
    for(int j=0;j&lt;object_count;j++){
      if(!blackhole_l[j])continue;
      if(a==blackhole&&i==j)continue;
      a_v[i]=get_vector(a_v[i],a[i],blackhole[j],blackhole_m[j]);
    }
  }
}

PVector get_vector(PVector v,PVector p,PVector p2,float m2){
  PVector dir=p2.copy();
  dir.sub(p);
  float dist=dir.mag();
  float a=G*m2/(dist*dist);
  dir.normalize();
  dir.mult(a);
  v.add(dir);
  return v;
}

void preset(){
  blackhole[0].set(width*0.5,height*0.5);
  blackhole_m[0]=blackhole_mass;
  blackhole_l[0]=true;
  
  star[0].set(width*0.5,height*0.5+150);
  star_v[0].set(1.5,0);
  star_m[0]=star_mass;
  star_l[0]=true;
  
  asteroid[0].set(width*0.5,height*0.5+170);
  asteroid_v[0].set(1.31,0);
  asteroid_m[0]=asteroid_mass;
  asteroid_l[0]=true;
}</code>
  </pre>
</details>