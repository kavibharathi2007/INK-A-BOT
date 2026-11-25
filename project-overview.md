  **INK A BOT**
Pollution in, ink out.
Ink a Bot is a wheeled robot that measures air quality, captures carbon soot from polluted air with a suction and filter system, and turns the recovered carbon into usable ink.
---
Table of Contents
Project Summary
Problem Statement
Objectives
Key Features
System Overview
Hardware Components
Complete Process (Top to Bottom)
Control Logic
Ink Formulation
Models
Applications and Impact
Skills Demonstrated
Future Scope


**1. Project Summary**

**Item	Details**

Project name	  **Ink a Bot**
Category    	  **Environmental robotics and embedded systems**
Controller	    **Arduino microcontroller**
Sensors	        **MQ-135 gas sensor, ultrasonic distance sensor**
Display	        **16x2 LCD (live air-quality level)**
Capture method	**Suction system with a filter-based collection unit**
Output	        **Carbon-based ink**

**2. Problem Statement**
Traffic and industrial emissions fill city air with carbon soot. Most devices only measure pollution and report a number. The soot itself is not removed or put to any use.
Ink a Bot closes this gap by combining three jobs in one machine: monitoring, capture and reuse.
Air pollution caused by vehicle emissions and industrial activities releases harmful particulate matter, including soot and carbon-based pollutants, into the atmosphere. These pollutants contribute to poor air quality and environmental degradation, while potentially reusable carbon-rich materials remain unutilized.
There is a need for an innovative, cost-effective, and automated system that can collect airborne particulate pollutants, separate suitable carbon-rich particles, and explore their conversion into reusable ink pigment, thereby promoting pollution management and waste-to-resource utilization.

The core problem we are solving
1. **Air pollution**: Harmful particulate matter accumulates in the atmosphere.
2. **Pollutant collection**: There is a need for an efficient localized collection mechanism.
3. **Waste utilization**: Potentially reusable carbon-rich soot is generally treated as waste.
4. **Resource recovery**: A suitable process is needed to recover and convert collected carbon into usable ink pigment.
   

**INK-A-BOT** – An intelligent mobile pollution-collection robot that monitors particulate pollution, collects airborne particles through a filtration mechanism, and processes suitable recovered carbon-rich material for potential ink production.

**3. Objectives**
Measure ambient air quality continuously and display it clearly.
Move through an area safely without hitting obstacles.
Capture carbon-rich particles from the air in a collection unit.
Recover the collected carbon and convert it into ink.

**4. Key Features**
Waste to wealth: captured soot becomes ink pigment.
Three jobs, one machine: monitoring, capture and reuse.
Mobile: goes to the pollution instead of waiting at a fixed spot.
Live air-quality feedback on an LCD.
Collision-safe movement using an ultrasonic sensor.
Low cost and easy to build from commonly available parts.
Multi-disciplinary: electronics, programming, mechanical design and chemistry.

**5. System Overview**

                    +-----------------------------+
                    |      ARDUINO CONTROLLER     |
                    +-----------------------------+
                      ^          ^          |
                      |          |          v
              +-------+--+  +----+-----+  +--------+     +----------------+
              | MQ-135   |  |Ultrasonic|  |  LCD   |     | Motors/Chassis |
              | gas      |  | sensor   |  | display|     | (movement)     |
              | sensor   |  |(obstacles)|  +--------+     +----------------+
              +----------+  +----------+

   Polluted air --> Suction --> Filter / Collection unit --> Container
                                                              |
                                                              v
                                       Recovered carbon --> Mixing --> INK
```
The robot has two cooperating parts:
Sensing and mobility system: Arduino, MQ-135, ultrasonic sensor, LCD, motors and wheels.
Capture and ink system: suction, filter-based collection unit, container, and the mixing stage that produces ink.
```
**6. Hardware Components**
Component	Role in the project
Arduino microcontroller	Central controller: reads sensors, drives display and movement
**MQ-135** gas sensor	Detects air pollutants and gives the air-quality reading
**Ultrasonic sensor**	Measures distance to obstacles ahead
**16x2 LCD display**	Shows the current air-quality level
**Four-wheel chassis with motors**	Lets the robot travel to the polluted area
**Suction system**	Draws polluted air into the robot
**Filter-based collection** unit	Traps carbon-rich particles from the air
**Collection container**	Holds the captured material
**Beaker and mixing setup**	Blends the recovered carbon into ink
**Metal cabinet body**	Houses and protects the electronics and the collection unit

**7. Complete Process (Top to Bottom)**

The full workflow runs in three phases.
Phase 1: Sense and Move
Step 1. Power up.
The **Arduino starts**, the sensors initialise and the LCD shows the **robot is ready**.
Step 2. Sense the air.
The **MQ-135 sensor** continuously reads the air. The reading is classified into a level such as Good, Moderate or Poor.
Step 3. Show the level.
The current air-quality level is displayed on the LCD so anyone nearby can read it.
Step 4. Move safely.
The **robot travels on its four wheels**. The **ultrasonic sensor** measures the distance to objects ahead, and the controller stops or turns the robot to **avoid collisions**.
Phase 2: Capture
Step 5. Draw in air.
The suction system pulls polluted air into the body of the robot.
Step 6. Capture carbon.
The air passes through the **filter-based collection unit**, which traps **carbon-rich particles**.
Step 7. Collect.
The trapped material gathers in the collection container.
Phase 3: Reuse
Step 8. Recover.
Once enough material is collected, it is taken out of the collection unit and the carbon is recovered.
Step 9. Make ink.
The recovered carbon is used as the pigment and **mixed evenly** with the other **ink ingredients** in a beaker.
Step 10. Finished ink.
The result is **usable ink**. Pollution has become a product.
Process at a glance

Power up -> Sense air (MQ-135) -> Show level (LCD) -> Move safely (ultrasonic)
   -> Suction draws in air -> Filter traps carbon -> Container collects
   -> Recover carbon -> Mix with ink base -> Finished ink
``

**8. Control Logic**
A simple outline of the program running on the Arduino. Adjust it to match your actual code.
``
SETUP:
    initialise LCD, MQ-135, ultrasonic sensor, motors
    show "Ready" on LCD

LOOP (repeats while the robot runs):
    reading   = read MQ-135
    level     = classify(reading)        # Good / Moderate / Poor
    show level on LCD

    distance  = read ultrasonic sensor
    if distance < safe_limit:
        stop, then turn away from the obstacle
    else:
        move forward

    run suction so air passes through the filter
``

**9. Ink Formulation**
The recovered carbon is the pigment. It is mixed with the other parts of a standard ink formulation.
Ingredient	Role in the ink
**Pigment**	        Gives the ink its colour; here, the recovered carbon
**Resin or binder**	Holds the pigment together and fixes it on the surface
**Humectants**	    Keep the ink from drying out too quickly
**Surfactants**   	Help the ink flow and spread smoothly
**Biocide**       	Prevents microbial growth and extends shelf life

**10. Models**
Model	Description
Working prototype	Built model with a metal cabinet body on a four-wheel chassis, LCD display, ultrasonic sensor, gas sensor, filter-based collection unit and container, labelled "INK A BOT".
Concept model	AI-generated vision of the final product: a transparent-panel body showing the Arduino and collection chamber, with an air-quality display on top.
Add your photos in an `images/` folder and link them here:
``

**11. Applications and Impact**
Area	What Ink a Bot offers
Environment	Removes carbon particles from the air and shows air quality in real time
Circular economy	Reuses waste soot as ink pigment instead of discarding it
Cities and roads	Works at traffic junctions, roadsides and industrial zones
Education	Hands-on demo of sensing, robotics and green chemistry
Research	Starting point for studying sustainable inks from captured carbon

**12. Skills Demonstrated**
Embedded programming and sensor interfacing with Arduino.
Robot design: chassis, motors, obstacle detection and display.
Air-quality monitoring and filtration.
Chemistry of ink formulation and mixing.
System integration: sensing, movement, capture and reuse working as one workflow.

**13. Future Scope**
Stronger suction and higher-capacity filtration.
IoT connection to send air-quality data to a phone app or cloud dashboard.
Solar-powered operation for longer outdoor work.
Fully autonomous route planning to reach the most polluted spots.
Lab testing of the ink for print quality, drying time and safety.
A compact, transparent-panel final design as shown in the concept model.


	
