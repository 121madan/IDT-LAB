# IDT-LAB
Optional
#include <LiquidCrystal.h>
// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
const int trigPin = 8, echoPin = 10;
//Input the area and depth of the tank
float Area = 28.2743338823;
float Total_depth = 11.5;
float duration, distance;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
void setup() {
// set up the LCD's number of columns and rows:
lcd.begin(16, 2);
// Print a message to the LCD.
lcd.print("Depth: ");
lcd.setCursor(0, 1);
lcd.print("Volume: ");
//Setting up the UltraSonic sensor
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
Serial.begin(9600);
}
void loop() {
digitalWrite(trigPin,LOW);
delayMicroseconds(2);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
//calculating depth with the sensor
duration = pulseIn(echoPin, HIGH);
distance = (duration*0.0343)/2;
//printing the depth
lcd.setCursor(7, 0);
lcd.print(distance);
lcd.setCursor(7, 1);
// printing the volume
lcd.print((Total_depth - distance)*Area);
lcd.setCursor(14,0);
lcd.print("cm");}
