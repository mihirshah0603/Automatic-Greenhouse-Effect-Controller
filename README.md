# Greenhouse Environment Control System

## Introduction:
Greenhouse farming has become increasingly popular in recent years, as it offers a controlled environment for growing plants and vegetables. The greenhouse environment is carefully regulated to ensure optimal plant growth, which requires accurate monitoring and control of temperature, sunlight, and water levels. In this project, we present the design and implementation of a greenhouse condition control system using an Arduino Uno microcontroller and Proteus software.

## Software used:
1. Proteus 8 Professional
2. Arduino IDE

## Components used:
1. Arduino UNO
2. Virtual display
3. Light Dependent Resistor (LDR)
4. LM35 Temperature Sensor
5. Digital Potentiometer (POT-HG)
6. Relays
7. LEDs
8. ULN2003A
9. L293D Motor Driver
10. DC Motors

## Circuit:
![Screenshot 2024-05-06 120842](https://github.com/mihirshah0603/Automatic-Greenhouse-Effect-Controller/assets/129767522/07ce5a40-1c5f-4b89-883d-27e71e363acf)

## Code:
```arduino
// Arduino code goes here
const int ledPin = 13;
const int lm35Pin = A4;
const int ldrPin = A0;
const int potPin = A5;
const int shadingMotorPin1 = 3;
const int shadingMotorPin2 = 2;
const int fanPin = 7;
const int pumpPin = 6;
const int lampPin = 5;

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  pinMode(shadingMotorPin1, OUTPUT);
  pinMode(shadingMotorPin2, OUTPUT);
  pinMode(pumpPin, OUTPUT);
  pinMode(fanPin, OUTPUT);
  pinMode(lampPin, OUTPUT);
  pinMode(ldrPin, INPUT);
  pinMode(lm35Pin, INPUT);
  pinMode(potPin, INPUT);
}

void loop() {
  int ldrStatus = analogRead(ldrPin);
  int lm35Status = analogRead(lm35Pin);
  float val = (lm35Status / 1024.0) * 5000;
  float temp = val / 10;
  int potStatus = analogRead(potPin);
  if (temp <= 20) {
    digitalWrite(lampPin, HIGH);
    digitalWrite(fanPin, LOW);
    Serial.print("Its COLD, Turn on the Heater : ");
    Serial.print(temp);
    Serial.println(" *C");
  } else {
    digitalWrite(lampPin, LOW);
    digitalWrite(fanPin, HIGH);
    Serial.print("Its HOT, Turn ON the FAN : ");
    Serial.print(temp);
    Serial.println(" *C");
  }
  if (ldrStatus <= 500) {
    digitalWrite(ledPin, LOW);
    digitalWrite(shadingMotorPin1, HIGH);
    digitalWrite(shadingMotorPin2, LOW);
    Serial.print("Its BRIGHT, Turn off the LED :  ");
    Serial.println(ldrStatus);
  } else {
    digitalWrite(ledPin, HIGH);
    digitalWrite(shadingMotorPin1, LOW);
    digitalWrite(shadingMotorPin2, HIGH);
    Serial.print("Its DARK, Turn on the LED : ");
    Serial.println(ldrStatus);
  }
  if (potStatus <= 200) {
    digitalWrite(pumpPin, HIGH);
    Serial.print("Water level is LOW, Turn ON the Pump : ");
    Serial.println(potStatus);
  } else {
    digitalWrite(pumpPin, LOW);
    Serial.print("Water level is GOOD, Turn OFF the Pump : ");
    Serial.println(potStatus);
  }
  delay(5000);
}
```

## Simulation:
The greenhouse control system was simulated using Proteus software, and the following results were obtained:
1. The temperature readings were displayed on the LED display, and the cooling system was activated when the temperature exceeded the set threshold.
2. The intensity of sunlight was measured, and the shading system was activated when the intensity of sunlight was too high.
3. The water level was measured, and the water pump was activated when the water level was too low.


https://github.com/mihirshah0603/Automatic-Greenhouse-Effect-Controller/assets/129767522/190e9dae-8005-42c1-a392-40518b878591



## Conclusion:
The designed greenhouse condition control system provides an efficient way to monitor and control the temperature, sunlight, and water levels inside a greenhouse. The Arduino Uno microcontroller is used to interface with various sensors and to control their operation based on programmed instructions. The system's performance can be simulated using Proteus software, making it easier to test and optimize the system before deployment.

Feel free to reach out if you have any questions or suggestions for improvement!
