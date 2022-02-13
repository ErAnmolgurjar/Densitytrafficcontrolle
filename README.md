# Densitytrafficcontrolle
We built an Arduino Traffic Light Controller and in this post, you are going to learn about how to make an density based traffic light controller using Arduino. The main purpose of this project is, if there will be no traffic on the other signal, one shouldn’t wait for that signal. The system will skip that signal and will move on the next one.
Arduino is the main part of this project and it will be used to read from ultrasonic sensor HC-SR04 and calculate the distance. This distance will tell us if any vehicle is near the signal or not and according to that the traffic signals will be controlled.
The main task was to avoid use of delay because we have to continuously read from the ultrasonic sensors and also at the same time, we have to control signals which requires the use of delay function.
So we have used the timerone library which is used to repetitively measure a period of time in microseconds and at the end of each period, an interrupt function will be called. In this function, we will read from the sensors and in the loop function, we will control the traffic signals.

# Working of Density Based Traffic Light Controller Using Arduino
The working of the project is divided into three steps

1.If there is traffic at all the signals, then the system will work normally by controlling the signals one by one.

2.If there is no traffic near a signal, then the system will skip this signal and will move on to the next one. For example, if there is no vehicle at signal 2, 3 and currently    the system is allowing vehicles at signal 1 to pass. Then after signal 1, the system will move on to signal 4 skipping signal 2 and 3.

3.If there is no traffic at all the 4 signals, system will stop at the current signal and will only move on the next signal if there will be traffic at any other signal.
# Components Required Density Based Traffic Light Controller Using Arduino
The components you are going to require for this project are as follows

Arduino Mega 2560

4 X HC-SR04 ultrasonic sensors

4 X Red LEDs

4 X Green LEDs

4 X Yellow LEDs

12 X 220 ohm resistors

Jumper cables

Breadboards
# Circuit Diagram Density Based Traffic Light Controller Using Arduino
Four ultrasonic sensors are interfaced with the Arduino. Arduino will read from these sensors and will calculate the distance. This sensor can measure from 2 to 400 cm.

Ultrasonic sensor basically emits an ultrasonic wave from the trigger and it is received by the echo after deflecting an object. In order to generate a wave, we will have to set the trigger at high for 10 us which will send an 8 cycle sonic burst at 40 KHz which will hit the object and after hitting the object, the wave will be received by the echo. The echo will then tell us the time that the wave have traveled in us (micro seconds). We will then convert this time into distance travelled by using S = v*t.
LED’s are connected to the Arduino through the 220 ohm resistors. It is necessary to use the resistor with the LED. The resistor limits the current flowing through the LED. If you won’t use it then the LED will burn out soon. You can use the resistor of value from 100 ohm to 10k ohm with the LED. Larger the value of LED, lesser the current will pass.
# Code Explanation
First of all, we included the timerone library. This library is used to repetitively measure a period of time in microseconds and at the end of each period, an interrupt function will be called.

We have used this library because we want to read from the sensors and control LED’s at the same time. We will have to use the delay in between the traffic signal so we can’t read from the sensors continuously. Therefore we have used this library which will allow us to call a function in which we will read from the sensors continuously and in the loop function, we will control the traffic signals.

#include<TimerOne.h>

In the setup function, we have used the Timer1.initialize(microseconds) function. This must be called before you use any of the other methods of timerone library. “Microseconds” is actually the period of time the timer takes. It is optionally to specify the timer’s period here. The default period is 1 second. Keep in mind that it breaks analogWrite() on digital pins 9 and 10.

Timer1.initialize(100000);

Timer1.attachInterrupt(softInterr) calls a function each time the timer period finishes. We have set the timer period at 100000 so our function will be called after 100 milli seconds.

Timer1.attachInterrupt(softInterr);

In the loop function it is looking if there is any vehicles under the 5 cm distance or not. If there will be vehicle, then the function to that signal will be called.

‘Softinterr()’ is the interrupt function and it will called after every 100 milliseconds. In this function, we have read from the ultrasonic sensors and have calculated the distance.
