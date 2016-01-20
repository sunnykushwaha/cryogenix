# cryogenix
Gestured Control Bot using Arduino
Using Arduino and an accelerometer you can make a bot which can be controlled by just your hand gesture.

Things needed:
Arduino Uno
L298N motor-driver 
2/3 axis accelerometer 
wire 
DC Motors X 2
Robot chasis
Wheels X 4


These are the connection between the L293D motor driver and the Arduino.

Enable1 --------------------------------> Digital Pin 05
Enable2  -------------------------------->Digital Pin 06
Input 1  -------------------------------->Digital Pin 07
Input 2 ----------------------------------->Digital Pin 08
Input 3 ----------------------------------->Digital Pin 09
Input 4 ----------------------------------->Digital Pin 10

These are the connection between the Accelerometer and the Arduino.
v0 -------------- 5v
X --------------- A0
Y --------------- A1
gnd ------------- gnd

Code for Arduino. 
int LeftMotorForward = 2; // Pin 02 has Left Motor connected on Arduino boards.
int LeftMotorReverse = 3; // Pin 03 has Left Motor connected on Arduino boards.
int RightMotorForward = 4; // Pin 04 has Right Motor connected on Arduino boards.
int RightMotorReverse = 5; // Pin 05 has Right Motor connected on Arduino boards.
int sensorValue00 = 0 ;
  int sensorValue11 = 0 ;
  int sensorValue22 = 0 ;
//-----------------------------------------------------------------------------
void setup() 
{
   Serial.begin(9600);
pinMode(LeftMotorForward, OUTPUT); // initialize the pin as an output.
pinMode(RightMotorForward, OUTPUT); // initialize the pin as an output.
pinMode(LeftMotorReverse, OUTPUT); // initialize the pin as an output.
pinMode(RightMotorReverse, OUTPUT); // initialize the pin as an output.
}

void loop()
{
int sensorValue0 = analogRead(A0);
  int sensorValue1 = analogRead(A1);
  if(sensorValue0 >= 170 && sensorValue0 < 510)
  {
  sensorValue0=map(sensorValue0,170,500,0,90);
  }
  if(sensorValue1 >= 200 && sensorValue1 < 550)
  {
  sensorValue1=map(sensorValue1,195,550,0,90);
  }
  Serial.print("X - AXIS =  ");
  Serial.print(sensorValue0);
  Serial.print("  ");
  Serial.print("Y - AXIS =  ");
  Serial.println(sensorValue1);
  if(sensorValue0 >35 && sensorValue0 <55)
  {
   stop(); 
  }
  if(sensorValue0 >0 && sensorValue0 <15)
  {
   forward(); 
  }
  if(sensorValue0 >80 && sensorValue0 <90)
  {
   reverse(); 
  }
  if(sensorValue1 < 10)
  {
   stop(); 
   left();
   delay(2000);
   forward();
  }
  if(sensorValue1 > 90)
  {
   stop(); 
   right();
   delay(2000);
   forward();
  }
  delay(10);

}
void forward()
{
digitalWrite(RightMotorReverse, LOW); // turn the Right Motor ON
digitalWrite(RightMotorForward, HIGH); // turn the Left Motor ON

digitalWrite(LeftMotorForward, LOW); // turn the Left Motor ON
digitalWrite(LeftMotorReverse, HIGH); // turn  the left Motor ON
}

void reverse()
{
 digitalWrite(LeftMotorForward, HIGH); // turn the Left Motor ON
digitalWrite(LeftMotorReverse, LOW);  // turn the Left Motor On

digitalWrite(RightMotorForward,LOW); // turn the Right Motor ON
digitalWrite(RightMotorReverse, HIGH); // turn the Left Motor ON 
}

void stop()
{
digitalWrite(RightMotorReverse, LOW); // turn the Right Motor OFF
digitalWrite(RightMotorForward, LOW); // turn the Left Motor OFF

digitalWrite(LeftMotorForward, LOW); // turn the Left Motor OFF
digitalWrite(LeftMotorReverse, LOW); // turn  the Left Motor OFF
}
void right()
{
 digitalWrite(LeftMotorForward,LOW ); // turn the Left Motor ON
digitalWrite(LeftMotorReverse, HIGH); // turn the Left Motor ON
digitalWrite(RightMotorForward,LOW); // turn the Right Motor OFF
digitalWrite(RightMotorReverse, LOW); // turn the Left Motor OFF 
delay(2000);
forward();
}
void left()
{
 digitalWrite(LeftMotorForward, LOW); // turn the Left Motor OFF
digitalWrite(LeftMotorReverse, LOW); // turn the Left Motor OFF
digitalWrite(RightMotorForward,HIGH); // turn the Right Motor ON
digitalWrite(RightMotorReverse,LOW); // turn the Left Motor ON
delay(2000);
forward();
}

Upload the code using Arduino IDE and callibrate the bot and enjoy.
