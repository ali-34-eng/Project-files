# Project-files#include <Wire.h> 
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27,16,2);
int blue=6;
int red=5;
int white=9;
int yelow=10;
int green=11;
int buzzer=3;
long rx=0;
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  lcd.init();
    lcd.begin(16,2);

  lcd.backlight();//optional
      Serial.println("How Your glucos mesurment: ");

  pinMode(red,OUTPUT);
  pinMode(blue,OUTPUT);
    pinMode(yelow,OUTPUT);
      pinMode(white,OUTPUT);
}

void loop() {
  // put your main code here, to run repeatedly:
   Serial.println("How Are You ");
   Serial.println("You Can Start");
    lcd.print("How Are You");
    lcd.setCursor(0, 1);
     lcd.print("You Can Start");
      for (int i = 0; i < 16; ++i)
    {
        lcd.backlight();
        delay(100);
        lcd.noBacklight();
        delay(50);
    }

    lcd.backlight();
    lcd.clear();
    delay(500);

 //if(Serial.available()>0){
  while(Serial.available()<11){
 rx=Serial.parseInt();
  //char rx=char (Serial.read());

//Serial.print("The DAta:");
//Serial.println(b);

if(rx>0 && rx<=99){
 analogWrite(white,80);
  analogWrite(yelow,00);
   analogWrite(green,00);
   analogWrite(blue,00);
   analogWrite(red,00);
 Serial.println("           Glucos is Low:");
  Serial.println(rx);
  lcd.print("Glucos is Low:");
  lcd.setCursor(0, 1);
   lcd.print(rx);
   
}
else if(rx>=100 && rx<=130){
   lcd.clear();
  analogWrite(yelow,80);
 analogWrite(white,00);
   analogWrite(green,00);
   analogWrite(blue,00);
   analogWrite(red,00);
  Serial.print("          Glucos Stable:");
  Serial.println(rx);
    lcd.print("Glucos Stable:");
    lcd.setCursor(0, 1);
   lcd.print(rx);
}
else if(rx>=131 && rx<=300){
   lcd.clear();
    analogWrite(green,80);
     analogWrite(white,00);
  analogWrite(yelow,00);
   analogWrite(blue,00);
   analogWrite(red,00);
    Serial.print("          glucos high ");
  Serial.println(rx);
     lcd.print("glucos high");
     lcd.setCursor(0, 1);
   lcd.print(rx);
}
  else if(rx>=301 && rx<= 400){
     lcd.clear();
    analogWrite(blue,80);
     analogWrite(white,00);
  analogWrite(yelow,00);
   analogWrite(green,00);
   analogWrite(red,00);
    Serial.print("           VH Tke insulin:");
  Serial.println(rx);
   lcd.print("VH Take insulin:");
    lcd.setCursor(0, 1);
   lcd.print(rx);
  }
  else if(rx>= 401  && rx <= 999){
     lcd.clear();
     analogWrite(red,80);
     analogWrite(white,00);
  analogWrite(yelow,00);
   analogWrite(green,00);
   analogWrite(blue,00);
    Serial.print("        Woring hospital:");
     Serial.println(rx);
     lcd.print("Woring hospital:");
     lcd.setCursor(0, 1);
      lcd.print(rx);
  
tone(buzzer,450);
delay(1000);
noTone(buzzer);
delay(1000);
  }
  else{
     Serial.println("Waiting...");
  delay(1000);
  }
 }
 

   //Serial.print("Stop state");
 while(1){/*empty*/}
}
