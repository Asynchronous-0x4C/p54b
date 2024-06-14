<link href="../css/original.css" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>

# 万有引力リベンジ

<details class="accordion">
  <summary>全体のコード</summary>
  <pre>
<code class="lang-java">
ArrayList&lt;Debri&gt;　objects=new ArrayList&lt;&gt;();

String type;

float asteroid_mass=7.34e2;

float star_mass=5.97e4;

float blackhole_mass=4.97e8;

PVector click_point;

final float G=6.67e-7;

void setup(){
  size(1280,720);
  
  set_target("blackhole");
  
  click_point=new PVector();
  
  preset();
}

void draw(){
  noStroke();
  fill(30,100);
  rect(0,0,width,height);
  
  for(Debri d:objects){
    d.display();
    d.update();
  }
  
  for(Debri d:objects){
    for(Debri d2:objects){
      if(d==d2)continue;
      get_vector(d,d2);
    }
  }
  
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
  
  switch(type){
    case "asteroid":objects.add(new Asteroid(click_point,release_point));break;
    case "star":objects.add(new Star(click_point,release_point));break;
    case "blackhole":objects.add(new Blackhole(click_point,release_point));break;
  }
}

void keyPressed(){
  switch(key){
    case 'a':set_target("asteroid");break;
    case 's':set_target("star");break;
    case 'b':set_target("blackhole");break;
  }
}

void set_target(String t){
  type=t;
}

PVector get_vector(Debri a,Debri b){
  PVector dir=b.position.copy();
  dir.sub(a.position);
  float dist=dir.mag();
  float accell=G*b.mass/(dist*dist);
  dir.normalize();
  dir.mult(accell);
  a.vector.add(dir);
  return a.vector;
}

void preset(){
  Blackhole b=new Blackhole(new PVector(width*0.5,height*0.5),new PVector());
  b.mass=blackhole_mass;
  
  Star s=new Star(new PVector(width*0.5,height*0.5+150),new PVector(1.5,0));
  s.mass=star_mass;
  
  Asteroid a=new Asteroid(new PVector(width*0.5,height*0.5+170),new PVector(1.31,0));
  a.mass=asteroid_mass;
  
  objects.add(b);
  objects.add(s);
  objects.add(a);
}

abstract class Debri{
  PVector position;
  PVector vector;
  
  float mass;
  boolean isDead;
  
  Debri(){
    position=new PVector();
    vector=new PVector();
    isDead=false;
  }
  
  void set_position(PVector position){
    this.position.set(position);
  }
  
  void set_vector(PVector vector){
    this.vector=vector;
  }
  
  void set_mass(float mass){
    this.mass=mass*random(1,1.5);
  }
  
  abstract void display();
  
  abstract void update();
}

class Asteroid extends Debri{
  
  Asteroid(PVector position,PVector vector){
    super();
    set_position(position);
    set_vector(vector);
    set_mass(asteroid_mass);
  }
  
  void display(){
    noStroke();
    fill(230);
    ellipse(position.x,position.y,5,5);
  }
  
  void update(){
    position.add(vector);
  }
}

class Star extends Debri{
  
  Star(PVector position,PVector vector){
    super();
    set_position(position);
    set_vector(vector);
    set_mass(star_mass);
  }
  
  void display(){
    noStroke();
    fill(230,100,100);
    ellipse(position.x,position.y,15,15);
  }
  
  void update(){
    position.add(vector);
  }
}

class Blackhole extends Debri{
  
  Blackhole(PVector position,PVector vector){
    super();
    set_position(position);
    set_vector(vector);
    set_mass(blackhole_mass);
  }
  
  void display(){
    noStroke();
    fill(0);
    ellipse(position.x,position.y,50,50);
  }
  
  void update(){
    position.add(vector);
  }
}</code>
  </pre>
</details>