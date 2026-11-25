**1. Arduino UNO**
Activity: Main control unit of INK-A-BOT.

Working Process:
- Receives data from the gas sensor, airflow sensor and ultrasonic sensor.
- Processes the sensor readings.
- Controls the suction mechanism based on predefined conditions.
- Updates the LED display with system status.
- Coordinates the operation of the connected components.
- 
**2. HEPA Filter**
Activity: Fine particulate matter filtration.

Working Process:
- Receives air after the initial particulate filtration stage.
- Captures fine airborne particles through its filtration media.
- Retains captured particles within the filter.
- Allows filtered air to pass to the next filtration stage.
  
**3. Activated Carbon Filter**
Activity: Gas and odor treatment.

Working Process:
- Receives air after particulate filtration.
- Adsorbs certain gaseous pollutants and odors onto its carbon surface.
- Helps improve the quality of outgoing air.
4. PM2.5 Filtration System
Activity: Collection of fine airborne particulate matter.

Working Process:
- Receives polluted air through the intake system.
- Captures PM2.5-sized particles using suitable filtration media.
- Retains the collected particles for controlled recovery.
  
**5. Gas Sensor**
Activity: Detection of selected gaseous pollutants.

Working Process:
- Continuously senses the surrounding air.
- Produces electrical signals corresponding to the detected gas concentration.
- Sends readings to Arduino UNO.
- Helps identify changes in environmental gas conditions

**6. LED Display**
Activity: Real-time system status indication.

Working Process:
- Receives display information from Arduino UNO.
- Displays available sensor readings and operating conditions.
- Indicates system ON/OFF status.
- Provides visual warnings for abnormal airflow or system conditions.
  
**7. 12V Rechargeable Battery**
Activity: Main power supply.

Working Process:
- Supplies electrical energy to the robot.
- Powers the suction blower and motor system through appropriate power circuits.
- Supplies regulated voltage to Arduino UNO and compatible sensors.
- Supports portable field operation.
  
**8. Airflow Detection Sensor**
Activity: Monitoring air movement through the filtration system.

Working Process:
- Measures airflow inside the air intake or filter duct.
- Sends airflow readings to Arduino UNO.
- Helps identify reduced airflow or blockages.
- Triggers a warning or collection shutdown when airflow becomes abnormal.
  
**9. Ultrasonic Sensor**
Activity: Obstacle detection and navigation assistance.

Working Process:
- Transmits ultrasonic sound waves.
- Receives the reflected waves from nearby objects.
- Calculates the distance to obstacles.
- Sends distance measurements to Arduino UNO.
- Supports stopping or changing the robot's direction when obstacles are detected.
  
**10. Power Switches**
Activity: Electrical power control.

Working Process:
- Controls the ON/OFF operation of the robot.
- Enables or disables the main power supply.
- Can separately control the electronics and collection mechanism when wired with suitable circuits.
- Helps with safe system operation and maintenance.

Overall component interaction
1. The 12V rechargeable battery supplies power to INK-A-BOT.
2. Power switches activate the system.
3. Arduino UNO initializes all connected sensors.
4. The gas sensor monitors gaseous pollutants.
5. The ultrasonic sensor detects nearby obstacles.
6. Arduino evaluates environmental readings and collection conditions.
7. The suction blower draws polluted air into the filtration unit.
8. The PM2.5 filtration stage captures fine particles.
9. The HEPA filter captures additional fine airborne particles.
10. The activated carbon filter adsorbs certain gaseous pollutants and odors.
11. The airflow sensor monitors the movement of air through the filtration unit.
12. The LED display provides operating information and warnings.
13. Suitable collected carbon-rich particles are recovered for further characterization and experimental ink production.
