# SM23-Elec-04

Arduino - Electronics and Power Department Task 04 - PIR Sensor motion detection

PIR sensors allow you to sense motion. They are used to detect whether a human has moved in or out of the sensor’s range. They are commonly found in appliances and gadgets used at home or for businesses. They are often referred to as PIR, "Passive Infrared", "Pyroelectric", or "IR motion" sensors.

![pir_sensor](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/33d29edf-85f8-4ed1-95d9-6041acad80b9)


# Advantages of PIR Sensors −

Small in size
Wide lens range
Easy to interface
Inexpensive
Low-power
Easy to use
Do not wear out

PIRs are made of pyroelectric sensors, a round metal can with a rectangular crystal in the center, which can detect levels of infrared radiation. Everything emits low-level radiation, and the hotter something is, the more radiation is emitted. The sensor in a motion detector is split in two halves. This is to detect motion (change) and not average IR levels. The two halves are connected so that they cancel out each other. If one-half sees more or less IR radiation than the other, the output will swing high or low.

![pir](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/1ab49e48-e8dc-46d2-8660-9785d4937a59)

PIRs have adjustable settings and have a header installed in the 3-pin ground/out/power pads.

![pir_adjustable_settings](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/badea204-1e91-4805-9ad9-2038b4e92fe8)


For many basic projects or products that need to detect when a person has left or entered the area, PIR sensors are great. Note that PIRs do not tell you the number of people around or their closeness to the sensor. The lens is often fixed to a certain sweep at a distance and they are sometimes set off by the pets in the house.

# Components Required
You will need the following components:

+ 1 × Breadboard
+ 1 × Arduino Uno R3
+ 2 × PIR Sensor (MQ3)
+ 2 × LEDs
+ 12 × wires

# Arduino code

Follow the circuit diagram and make the connections as shown in the image below.

![pir_sensor_circuit_connection](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/9b79949e-91bf-4975-8ebd-1d716d6f1b4a)

Open the Arduino IDE software on your computer. Coding in the Arduino language will control your circuit. Open a new sketch File by clicking New.

Code:
```
#define pirPin 2
int calibrationTime = 30;
long unsigned int lowIn;
long unsigned int pause = 5000;
boolean lockLow = true;
boolean takeLowTime;
int PIRValue = 0;

void setup() {
   Serial.begin(9600);
   pinMode(pirPin, INPUT);
}

void loop() {
   PIRSensor();
}

void PIRSensor() {
   if(digitalRead(pirPin) == HIGH) {
      if(lockLow) {
         PIRValue = 1;
         lockLow = false;
         Serial.println("Motion detected.");
         delay(50);
      }
      takeLowTime = true;
   }
   if(digitalRead(pirPin) == LOW) {
      if(takeLowTime){
         lowIn = millis();takeLowTime = false;
      }
      if(!lockLow && millis() - lowIn > pause) {
         PIRValue = 0;
         lockLow = true;
         Serial.println("Motion ended.");
         delay(50);
      }
   }
}
```
# Code Notes

PIR sensor has three terminals - Vcc, OUT and GND. Connect the sensor as follows −

+ Connect the +Vcc to +5v on Arduino board.
+ Connect OUT to digital pin 2 on Arduino board.
+ Connect GND with GND on Arduino.
  
You can adjust the sensor sensitivity and delay time via two variable resistors located at the bottom of the sensor board.

![delay_time_adjust](https://github.com/Naif-Al-Ajlani/SM23-Elec-04/assets/98528261/461de9d1-a2e9-42cf-ab1c-ec1f306aedef)

Once the sensor detects any motion, Arduino will send a message via the serial port to say that a motion is detected and the LEDs will be turned on. The PIR sense motion will delay for certain time to check if there is a new motion. If there is no motion detected, Arduino will send a new message saying that the motion has ended.

# Result
You will see a message on your serial port if a motion is detected and the LEDs will be tuned on another message when the motion stops and the LEDs will be off.
