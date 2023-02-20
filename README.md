# PID Marble Position Control

As a simple project to demostrate closed loop control behavior, a marble balance can be used. 

The goal of this project is to target a wide range of disciplines in one go. 

High Level Areas: 
1. 3D Modeling
2. Circuit Communication i.e I2C
3. Control Theory
4. Task scheduling
5. Precision distance sensing
6. (stretch) PCB Design

<br/><br/>
## Project Overview
- - - -
#### Mechanical Principle
- - - -
![Project Overview Daigram](https://github.com/Killerkarebearz/PID-Marble-Position-Control/blob/main/MarbleFreeBody.svg?raw=true)

The main goal of the mechanical design is to achieve a mechanism that: 
- Is pivotable based on a DC motors output
- Provids a track with defined ends for a marble to run along
- Has limit switches to define the bounds of tilt

The ball will roll freely back and forth along the track and should be controllable and any point along the calibrated range. 

The base will hold the three potentiometers that allow live tuning of the PID Coeffiecient gains. 

<br/><br/>
#### Project Architecture
- - - -

![Project Overview Daigram](https://github.com/Killerkarebearz/PID-Marble-Position-Control/blob/main/MarblePID.svg?raw=true)


For user interface, the user should be able to interact with 3 potentiometers that will convert the analog voltage into a scaled gain factor for each of the PID coeffiecients. 

The control logic will measure the distance of the marble on the track using a LiDAR sensor and converting the reading to the calibrated range of the track. 

![PID Diagram](https://upload.wikimedia.org/wikipedia/commons/4/43/PID_en.svg?raw=true)
With the feedback of the current marble position as well as previous stored positions and a given sample rate, an output command will be sent to a DC motor driver (H-bridge). This command will be PWM to give proportional control. Mechanically, a limit switch will signal when an endstop has been hit and the output will be overriden for protection. 

At initial boot of the system, an auto calibration will run where the endstop is reached for each extreme of tilt and the liDAR measurement is captured. This ranges will be used to map the raw feedback to a 0 - 100% range. 

<br/><br/>
### Component Selection: 
- - - -
This project is planned in two iterations, a roughing using arduino and off the shelf items, and a custom PCB embedded within the 3D model as standalone. 

1. Roughing
    - Microcontroller: Arduino Uno
    - Distance Sensor: VL53L0X
    - Motor Driver: L298N Based Drivers
2. Custom PCB
    - Microcontroller: TBD
    - Distance Sensor: TBD
    - Motor Driver: TBD