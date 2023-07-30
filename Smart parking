#include <LiquidCrystal_I2C.h>           //LIBRARY FOR I2C MODULE
LiquidCrystal_I2C lcd(0x3F, 16, 2);      //ADDRESS OF 16X2 I2C LCD MODULE
#include <Servo.h>

Servo myservo1;

int IR1 = 3;             //ENTRANCE SENSOR CONNECTED TO PIN 3 OF ARDUINO
int IR2 = 5;             //ENTRANCE SENSOR CONNECTED TO PIN 5 OF ARDUINO

int Slot = 3;            // Total number of parking Slots

int flag1 = 0;
int flag2 = 0;

void setup() {
  lcd.init();
  lcd.backlight();
  pinMode(IR1, INPUT);
  pinMode(IR2, INPUT);

  myservo1.attach(9);              //SERVO MOTOR ATTACHED TO PIN 9 OF ARDUINO UNO
  myservo1.write(100);

  lcd.setCursor (0, 0);
  lcd.print("     ARDUINO    ");
  lcd.setCursor (0, 1);
  lcd.print(" PARKING SYSTEM ");
  delay (2000);
  lcd.clear();
}

void loop() {

  if (digitalRead (IR1) == LOW && flag1 == 0) {                //DETECTING OBSTACLE AT ENTRY SENSOR
    if (Slot > 0) {
      flag1 = 1;
      if (flag2 == 0) {
        myservo1.write(0);
        Slot = Slot - 1;
      }
    } else {
      lcd.setCursor (0, 0);
      lcd.print("    SORRY :(    ");                           //IF NO SLOTS LEFTS IT DISPLAYS SORRY :(  MESSAGE
      lcd.setCursor (0, 1);
      lcd.print("  Parking Full  ");
      delay (3000);
      lcd.clear();
    }
  }

  if (digitalRead (IR2) == LOW && flag2 == 0) {               //DETECTING OBSTACLE AT EXIT SENSOR
    flag2 = 1;
    if (flag1 == 0) {
      myservo1.write(0);                                     //INTIALLY GATE IS CLOSE WHICH IS OF 0 DEGREE                
      Slot = Slot + 1;
    }
  }

  if (flag1 == 1 && flag2 == 1) {                            //IF FLAG VALUE=1 GATE OPENS
    delay (1000);
    myservo1.write(100);
    flag1 = 0, flag2 = 0;
  }

  lcd.setCursor (0, 0);
  lcd.print("    WELCOME!    ");
  lcd.setCursor (0, 1);
  lcd.print("Slot Left: ");
  lcd.print(Slot);                                           //DISPLAYS NO OF SLOTS AVAILABLE IN LCD
}
