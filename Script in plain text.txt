#include <LiquidCrystal.h>
int sensePin1 = A0;
int sensePin = A1;
int buttonPin = 8;
int buttonState = 0;
int sensorInput1;
int sensorInput2;
double temp1;
double temp2;
int lcdState = 0;
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

void setup()
{
  Serial.begin(9600);
  lcd.begin(16, 2);
  pinMode(buttonPin, INPUT);
}

void loop()
{
  sensorInput1 = analogRead(A0);
  sensorInput2 = analogRead(A1);
  temp1 = (double)sensorInput1 / 1024;
  temp1 = temp1 * 5;
  temp1 = temp1 - 0.5;
  temp1 = temp1 * 100;
  temp2 = (double)sensorInput2 / 1024;
  temp2 = (temp2 * 5 - 0.5) * 100;
  
  lcd.setCursor(0, 0);
  lcd.print("Inside:");
  lcd.print(temp1);
  lcd.print("\xDF" "C");
  lcd.setCursor(0, 1);
  lcd.print("Outside:");
  lcd.print(temp2);
  lcd.print("\xDF" "C");
  

  delay(5000);
  lcd.clear();
    
  Serial.println(temp1);
}