# SM23-Elec-04

Smart methods 2023 summer training (Electronics and Power Department Task 04)

+ PIR Sensor motion detection System

PIR sensors allow you to sense motion. They are used to detect whether a human has moved in or out of the sensor’s range. They are commonly found in appliances and gadgets used at home or for businesses. They are often referred to as PIR, "Passive Infrared", "Pyroelectric", or "IR motion" sensors.

![PIR-Sensor-Pinout](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/e1a3d514-e988-456d-ba38-560a56a8fc70)

# Advantages of PIR Sensors

+ Small in size
+ Wide lens range
+ Easy to interface
+ Inexpensive
+ Low-power
+ Easy to use
+ Do not wear out

PIRs are made of pyroelectric sensors, a round metal can with a rectangular crystal in the center, which can detect levels of infrared radiation. Everything emits low-level radiation, and the hotter something is, the more radiation is emitted. The sensor in a motion detector is split in two halves. This is to detect motion (change) and not average IR levels. The two halves are connected so that they cancel out each other. If one-half sees more or less IR radiation than the other, the output will swing high or low.

![pir](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/1ab49e48-e8dc-46d2-8660-9785d4937a59)

PIRs have adjustable settings and have a header installed in the 3-pin ground/out/power pads.

![pir_adjustable_settings](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/badea204-1e91-4805-9ad9-2038b4e92fe8)

For many basic projects or products that need to detect when a person has left or entered the area, PIR sensors are great. Note that PIRs do not tell you the number of people around or their closeness to the sensor. The lens is often fixed to a certain sweep at a distance and they are sometimes set off by the pets in the house.

# Components Required
You will need the following components:

+ 1 × Breadboard
+ 1 × Arduino Uno
+ 2 × PIR Sensor (MQ3)
+ 2 × LEDs
+ 2 × Resistor
+ 12 × wires

# Arduino code

Follow the circuit diagram and make the connections as shown in the image below.

![pir_sensor_circuit_connection](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/9b79949e-91bf-4975-8ebd-1d716d6f1b4a)

Open the Arduino IDE software on your computer. Coding in the Arduino language will control your circuit. Open a new sketch File by clicking New.

+ Note: This code only uses one PIR sensor connected to one LED throw Arduino UNO and Breadboard

![enlarge_2023-09-04__3_](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/72c0e012-eceb-4e73-8d85-395067722c67)

+ Code:

```
int ledPin = 13;                  // LED
int pirPin = 2;                   // PIR Out pin
int pirStat = 0;                  // PIR status

void setup() {
  pinMode(ledPin, OUTPUT);        // declare LED as output
  pinMode(pirPin, INPUT);         // declare sensor as input
  Serial.begin(9600);
  Serial.println("Serial Monitor connected");
  delay(1000);
  Serial.print(".");
  delay(500);
  Serial.print(".");
  delay(500);
  Serial.println(".");
  delay(500);
  Serial.println("Please let your sensor calibrate");
  delay(1000);
  Serial.println("for 15 to 30 seconds before testing");
  delay(1000);
  Serial.print(".");
  delay(500);
  Serial.print(".");
  delay(500);
  Serial.println(".");
  delay(500);
}

void loop(){
 pirStat = digitalRead(pirPin); 
 if (pirStat == HIGH) {             // if motion detected
   Serial.println("Motion Detected!");
   digitalWrite(ledPin, HIGH);      // turn LED ON
   delay(100);                      // wait for a second
   digitalWrite(ledPin, LOW);       // turn LED OFF
   delay(100);                      // wait for a second
 } 
 else {
   digitalWrite(ledPin, LOW);       // LED stays off if no motion detected
   Serial.println("No Motion Detected!");
 }
} 

```

# Simulation on tinkercad

PIR sensors motion detection tracking System on tinkercad

+ link: https://www.tinkercad.com/things/lOJbj2qYDrI

<img width="960" alt="2023-09-04 (2)" src="https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/e3331fae-77fe-4c52-aa2f-cd2562c63f36">

Code:

  ```
  const int PIR1_PIN = 3;
const int PIR2_PIN = 4;

int visitors = 0;
int lastRIPdetected = 0;
bool b_PIR1_active = false;

void setup() {
  pinMode(PIR1_PIN, INPUT);  
  pinMode(PIR2_PIN, INPUT);  
  Serial.begin(9600);  
  Serial.println("Visitors are welcome");
}

void loop() {
  
  if (digitalRead(PIR1_PIN) == HIGH) {
    
    if (!b_PIR1_active && lastRIPdetected == 0) {
      b_PIR1_active = true;  
      lastRIPdetected = 1;  
      Serial.println("Visit started");
    }
  } else {
    b_PIR1_active = false;
    if (lastRIPdetected == 1) lastRIPdetected = 2;
  }

 
  if (lastRIPdetected == 2 && digitalRead(PIR2_PIN) == HIGH) {
    visitors++; 
    lastRIPdetected = 0; 
    Serial.println("Visitor entered. Visitors: " + String(visitors));
  }
}
```

# Code Notes

PIR sensor has three terminals - Vcc, OUT and GND. Connect the sensor as follows −

+ Connect the +Vcc to +5v on Arduino board.
+ Connect OUT to digital pin 2 on Arduino board.
+ Connect GND with GND on Arduino.
  
You can adjust the sensor sensitivity and delay time via two variable resistors located at the bottom of the sensor board.

![delay_time_adjust](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/48885bfd-2172-46a4-aaea-7ac00f67be01)

Once the sensor detects any motion, Arduino will send a message via the serial port to say that a motion is detected and the LEDs will be turned on. The PIR sense motion will delay for certain time to check if there is a new motion. If there is no motion detected, Arduino will send a new message saying that the motion has ended.

# Task result

The PIR sensor can be adjusted manually by looking at the back. I had to make some slight adjustments to make the sensor more reactive before I got too far into the coding process.

+ Once the   PIR sensor detects any motion, Arduino will send a message via the serial port to say that a motion is detected and the LEDs will be turned on. The PIR sense motion will delay for certain time to check if there is a new motion.

+ If there is no motion detected by the PIR sensor, Arduino will send a new message saying that the motion has ended via the serial port and the LEDs will be turned off.

+ Important Note: I read in a lot of tutorials that the LED light will stay on until the sensor is done calibrating, but the only time the LED was on when I uploaded the script was when I had the power and ground connected to the wrong pins. When my sensor is connected properly, the LED will stay off when the script is uploaded and that was the only time it would detect the motion properly.

# Resources

+ Arduino website on PIR sensors: https://support.arduino.cc/hc/en-us/articles/4403050020114-Troubleshooting-PIR-Sensor-and-sensitivity-adjustment
+ Ardunno with PIR Motion Sensor tutorial https: www.tutorialspoint.com/arduino/arduino_pir_sensor.htm
+ PIR Motion Sensor with Arduino instructions: https: www.instructables.com/How-to-Use-a-PIR-Motion-Sensor-With-Arduino/
+ To learn more about how to adjust the "settings" of a PIR sensor: https://www.tweaking4all.com/hardware/pir-sensor/
+ Helpful website that explains the "settings" of the PIR sensor: https://learn.adafruit.com/pir-passive-infrared-proximity-motion-sensor/testing-a-pir
+ Arduino project Hub https://projecthub.arduino.cc/
+ PIR Motion Sensor with Arduino youtube tutorial: https://www.youtube.com/watch?v=FxaTDvs34mM
+ Test Clip of PIR Motion Sensor: https://www.youtube.com/watch?v=YDqao92gnFE
