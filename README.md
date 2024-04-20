# FlightControlSurfaceControllingViaServoMotor

```c

#include <Servo.h>

// Potansiyometrelerin bağlı olduğu pinler
const int elaronPotPin1 = A0;
const int elaronPotPin2 = A1;
const int elevatorPotPin = A2;
const int rudderPotPin = A3;
// Gaz kelebeği pinleri
const int throttlePotPin = A4;
const int throttleServoPin = 11; // PWM çıkışı

// Servo nesneleri
Servo elaronServo1;
Servo elaronServo2;
Servo elevatorServo;
Servo rudderServo;
// Gaz kelebeği servo nesnesi
Servo throttleServo;

void setup() {
  // Servo pinleri
  int elaronServoPin1 = 5;
  int elaronServoPin2 = 6;
  int elevatorServoPin = 9;
  int rudderServoPin = 10;
  
  // Gaz kelebeği servo pinini bağla
  throttleServo.attach(throttleServoPin);

  // Servo nesnelerini bağla
  elaronServo1.attach(elaronServoPin1);
  elaronServo2.attach(elaronServoPin2);
  elevatorServo.attach(elevatorServoPin);
  rudderServo.attach(rudderServoPin);
}

void loop() {
  // Potansiyometrelerden okunan değerler
  int elaronValue1 = analogRead(elaronPotPin1);
  int elaronValue2 = analogRead(elaronPotPin2);
  int elevatorValue = analogRead(elevatorPotPin);
  int rudderValue = analogRead(rudderPotPin);
  // Gaz kelebeği değeri
  int throttleValue = analogRead(throttlePotPin);

  // Potansiyometre değerlerini servo sinyallerine dönüştürme (0-1023 aralığından 0-180 aralığına)
  int elaronAngle1 = map(elaronValue1, 0, 1023, 0, 180);
  int elaronAngle2 = map(elaronValue2, 0, 1023, 0, 180);
  int elevatorAngle = map(elevatorValue, 0, 1023, 0, 180);
  int rudderAngle = map(rudderValue, 0, 1023, 0, 180);
  // Gaz kelebeği değerini servo sinyaline dönüştürme (0-1023 aralığından 0-180 aralığına)
  int throttleAngle = map(throttleValue, 0, 1023, 0, 180);

  // Servo sinyallerini gönderme
  elaronServo1.write(elaronAngle1);
  elaronServo2.write(elaronAngle2);
  elevatorServo.write(elevatorAngle);
  rudderServo.write(rudderAngle);
  // Gaz kelebeği sinyalini gönderme
  throttleServo.write(throttleAngle);

  // Servo sinyali güncellenmesi için kısa bir bekleme
  delay(15);
}


```
