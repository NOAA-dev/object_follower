# object_follower
A basic model of Object_following bot using Arduino
#include <Servo.h>
//setting up constants
Servo servo_1;
const int echo=8;
const int pulse=11;
double distance;
double duration;
int pos = 0;


void setup() {
  Serial.begin(9600);
  servo_1.attach(10);
  pinMode(pulse,OUTPUT);
  pinMode(echo,INPUT);
  pinMode(2,OUTPUT);
  pinMode(3,OUTPUT);
  pinMode(4,OUTPUT);
  pinMode(5,OUTPUT);
  pinMode(6,OUTPUT);
  pinMode(9,OUTPUT);
  pinMode(13,OUTPUT);
  analogWrite(13,255);
}

void loop() {
  int mool = 0;
  while(mool == 0){
  servo_1.write(90);
  measure();
  delay(1000);
    if(distance<40&&distance>10){
    forward();
    delay(250);
    stop();
    }else{
    mool =1;
    break;
  }
  }mool =0;
  while(mool == 0){
    if(distance<10&&distance>0){
    back();
    delay(250);
    stop();
    }else{
    mool = 1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90+30);
  measure();
  
  if(distance<40&&distance>10){
    left();
    delay(20);
    stop();
  }else{
    mool = 1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90-30);
  measure();
  
  if(distance<40&&distance>10)
  {
    right();
    delay(20);
    stop();
  }else{
    mool = 1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90+60);
  measure();
  
  if(distance<40&&distance>10){
    left();
    delay(60);
    stop();
  }else{
    mool = 1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90-60);
  measure();
  
  if(distance<40&&distance>10){
    right();
    delay(60);
    stop();
  }else{
    mool = 1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90+90);
  measure();
  if(distance<40&&distance>10){
    left();
    delay(90);
    stop();
  }else{
    mool=1;
    break;
  }
  }mool =0;
  while(mool == 0){
  servo_1.write(90-90);
  measure();
  
  if(distance<40&&distance>10){
    right();
    delay(90);
    stop();
  }else{
    mool = 1;
    break;
  }
  }
 





}
void measure(){
  delay(1000);
  for(int i=0;i<5;i++){
    digitalWrite(pulse,0);
    delay(2);
   digitalWrite(pulse,1);
   delay(10);
   digitalWrite(pulse,0);
   duration = pulseIn(echo,HIGH);
   distance= (duration*0.0343)/2;
  }
  
  Serial.print(distance);
  Serial.print(" | ");
  Serial.println(duration);
}
void stop(){
  digitalWrite(2,0);
  digitalWrite(3,0);
  
  digitalWrite(4,0);
  digitalWrite(5,0);

  analogWrite(6,0);
  analogWrite(9,0);
}
void right(){
  digitalWrite(2,1);
  digitalWrite(3,0);
  
  digitalWrite(4,1);
  digitalWrite(5,0);

  analogWrite(6,150);
  analogWrite(9,150);
}
void left(){
  digitalWrite(2,0);
  digitalWrite(3,1);
  
  digitalWrite(4,0);
  digitalWrite(5,1);

  analogWrite(6,150);
  analogWrite(9,150);
}
void forward(){
  digitalWrite(2,1);
  digitalWrite(3,0);
  
  digitalWrite(4,0);
  digitalWrite(5,1);

  analogWrite(6,150);
  analogWrite(9,150);
}
void back(){
  digitalWrite(2,0);
  digitalWrite(3,1);
  
  digitalWrite(4,1);
  digitalWrite(5,0);

  analogWrite(6,150);
  analogWrite(9,150);
}

