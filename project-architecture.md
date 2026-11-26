# INK-A-BOT — Project Architecture

## 1. Project overview

INK-A-BOT is proposed as a mobile environmental robotics platform. Its intended system combines:

- A mobile chassis with DC motors.
- Obstacle detection and autonomous navigation.
- Air intake and a staged filtration assembly.
- Air-quality and airflow monitoring.
- Arduino-based control and status display.
- A separate, controlled research pathway for evaluating captured particulate material for possible reuse.

**Important scope clarification:** The Arduino sketch supplied for this document implements the robot's drive and obstacle-avoidance subsystem. It does not currently control the air-filtration hardware, gas sensor, airflow sensor, PM2.5 sensor, LED display, blower, or material-recovery process. Those are proposed additional subsystems and require further circuit design and code.

## 2. High-level system architecture

```text
                         INK-A-BOT
                             |
       +---------------------+----------------------+
       |                     |                      |
       v                     v                      v
 MOBILE ROBOT         AIR-FILTRATION          MONITORING &
 SUBSYSTEM             SUBSYSTEM               CONTROL
       |                     |                      |
       |                     |                      |
 Arduino UNO          Air intake              Arduino UNO
       |                     |                      |
 L298N driver         Coarse screen             Ultrasonic sensor
       |                     |                  + Servo scanning
       |                PM2.5 filter                 |
 DC motors                 |                    Gas sensor
       |                HEPA filter                  |
 Robot movement            |                    Airflow sensor
                      Activated carbon                |
                           |                     Optional PM2.5
                         Blower                     sensor
                           |                          |
                       Filtered-air              LED display
                         outlet                      |
                                                Status / alerts

                             |
                             v
                 CONTROLLED MATERIAL RESEARCH
                             |
                  Sealed filter / collection
                             |
                  Laboratory characterization
                             |
                  Validated processing, if suitable
                             |
                   Experimental eco-ink research
```

The diagram shows the intended complete project concept. The supplied sketch currently implements only the mobile robot subsystem described below.

## 3. Mobile robot hardware architecture

### 3.1 Arduino UNO — main controller

The Arduino UNO executes the obstacle-avoidance program. It reads distance measurements from the ultrasonic sensor through the NewPing library, commands the servo to scan directions, and controls the L298N motor driver.

In the supplied sketch, the UNO:
1. Configures motor-driver pins as outputs.
2. Attaches the servo motor.
3. Centers the ultrasonic sensor.
4. Takes initial distance readings.
5. Repeatedly checks the front distance.
6. Stops and reverses when an obstacle is within the configured threshold.
7. Scans right and left.
8. Turns towards the side with the larger measured clearance.
9. Continues forward when the front path is clear.

### 3.2 L298N motor driver

The L298N is the interface between the low-power Arduino control signals and the higher-current DC motors.

| L298N control | Arduino UNO pin | Purpose in sketch |
|---|---:|---|
| ENA | D5 | PWM speed control for motor channel A |
| IN1 | D10 | Left motor direction input 1 |
| IN2 | D11 | Left motor direction input 2 |
| IN3 | D9 | Right motor direction input 1 |
| IN4 | D8 | Right motor direction input 2 |
| ENB | D6 | PWM speed control for motor channel B |

The sketch treats channel A as the left motor and channel B as the right motor. Confirm the actual motor wiring because motor polarity and channel assignment can differ between builds.

**Important:** If the L298N board has ENA/ENB jumper caps installed, remove them when using Arduino PWM on D5/D6. Use a suitable motor supply, common ground with the Arduino, and appropriate power protection. Do not power the motors directly from an Arduino I/O pin.

### 3.3 DC motors and movement

The code controls two motor channels:

- **Forward:** both motors are commanded forward.
- **Backward:** both motors are commanded backward.
- **Right turn:** left motor forward, right motor backward.
- **Left turn:** left motor backward, right motor forward.
- **Stop:** direction inputs are set LOW and both enable PWM outputs are set to zero.

This is a differential-drive arrangement. The robot changes direction by driving its left and right wheels in different directions.

### 3.4 Ultrasonic sensor

The ultrasonic sensor measures the distance to an object in front of the robot.

| Signal | Arduino UNO pin |
|---|---:|
| TRIG | A5 |
| ECHO | A4 |

The code sets the maximum measurable distance to 200 cm. The `NewPing` library performs the ping measurement.

The function `readPing()` returns the measured distance in centimetres. If no echo is received and `ping_cm()` returns zero, the sketch treats the reading as the maximum distance (200 cm).

This fallback is a programming choice, not proof that the path is clear. A missed echo can also occur because of target shape, angle, material, sensor placement or environmental conditions. For safer operation, consider treating repeated invalid readings as an uncertainty or stop condition rather than automatically assuming 200 cm.

### 3.5 Servo motor

The servo rotates the ultrasonic sensor so the robot can inspect different directions without rotating the whole chassis.

| Servo position | Arduino pin | Purpose |
|---|---:|---|
| Signal | D3 | Servo control |
| Centre | 115° | Front-facing measurement |
| Right | 50° | Right-side scan |
| Left | 170° | Left-side scan |

The code first checks the right side, then the left side, and returns the servo to the centre position after each scan.

The angles are configured values. Actual left/right orientation depends on how the servo and sensor bracket are mounted. Confirm direction physically before testing.

## 4. Pin allocation summary

| Arduino UNO pin | Connected component | Signal |
|---|---|---|
| D3 | Servo motor | Servo signal |
| D5 | L298N ENA | Motor A PWM enable |
| D6 | L298N ENB | Motor B PWM enable |
| D8 | L298N IN4 | Right motor direction |
| D9 | L298N IN3 | Right motor direction |
| D10 | L298N IN1 | Left motor direction |
| D11 | L298N IN2 | Left motor direction |
| A4 | Ultrasonic sensor | Echo |
| A5 | Ultrasonic sensor | Trigger |

The supplied sketch does not assign pins to the gas sensor, airflow sensor, PM2.5 sensor, LED display or blower driver. Those pins must be selected after the exact modules and their electrical interfaces are known. Avoid pin conflicts with the existing assignments.

## 5. Obstacle-avoidance algorithm

### 5.1 Configured values

| Parameter | Value | Meaning |
|---|---:|---|
| `maximum_distance` | 200 cm | Maximum range passed to NewPing |
| `OBSTACLE_DISTANCE` | 40 cm | Obstacle decision threshold |
| `FORWARD_SPEED` | 220 / 255 | Forward PWM command |
| `BACKWARD_SPEED` | 180 / 255 | Reverse PWM command |
| `TURN_SPEED` | 230 / 255 | Turning PWM command |
| `TURN_TIME` | 300 ms | Timed turn duration |
| `SERVO_CENTER` | 115° | Forward scan position |
| `SERVO_RIGHT` | 50° | Right scan position |
| `SERVO_LEFT` | 170° | Left scan position |

PWM values are commands, not calibrated wheel speeds. Actual speed depends on battery voltage, motor characteristics, load, wheel size and driver voltage drop. A 300 ms turn is not a guaranteed fixed angle; calibrate it on the actual chassis.

### 5.2 Step-by-step operating sequence

1. **Power-up:** Arduino configures the L298N pins and stops the motors.
2. **Sensor setup:** Servo attaches to D3 and points to the configured centre angle.
3. **Initial measurement:** The robot takes several front distance readings.
4. **Front check:** The loop compares the most recent distance with the 40 cm threshold.
5. **Clear path:** If distance is greater than 40 cm, both motors move forward.
6. **Obstacle detected:** If distance is 40 cm or less, the robot stops.
7. **Reverse:** The robot moves backward for 200 ms.
8. **Pause:** Motors stop for 300 ms.
9. **Right scan:** Servo points to 50° and the ultrasonic sensor measures distance.
10. **Left scan:** Servo points to 170° and measures distance.
11. **Compare:** The code compares the two measurements.
12. **Choose direction:** If right distance is greater than or equal to left distance, turn right; otherwise turn left.
13. **Turn:** The motors counter-rotate for 300 ms at the configured turning PWM.
14. **Stop and resume:** The robot stops, returns to the main loop and checks the front again.

### 5.3 Decision flowchart

```text
              START
                |
                v
       Initialize UNO pins
       Servo and motor driver
                |
                v
        Read front distance
                |
                v
       Is distance <= 40 cm?
            /       \
          YES        NO
           |          |
           v          v
       Stop motors  Move forward
           |          |
           v          |
       Reverse 200 ms |
           |          |
           v          |
       Stop and wait  |
           |          |
           v          |
       Scan right     |
           |          |
           v          |
       Scan left      |
           |          |
           v          |
    Compare distances |
        /      \      |
 Right >= Left?       |
    /       \         |
  YES       NO        |
   |         |        |
   v         v        |
Turn right Turn left  |
   \         /        |
    v       v         |
     Stop motors      |
           |          |
           +----+-----+
                |
                v
        Read front again
```

## 6. Software architecture

### 6.1 Libraries

```cpp
#include <Servo.h>
#include <NewPing.h>
```

- `Servo.h` provides control of the servo motor.
- `NewPing.h` provides ultrasonic distance measurement.

Install the NewPing library in the Arduino IDE Library Manager or add it through the normal Arduino library installation process.

### 6.2 Main functions

| Function | Responsibility |
|---|---|
| `setup()` | Configures pins, attaches servo and takes initial readings |
| `loop()` | Runs the obstacle-avoidance decision cycle |
| `lookRight()` | Scans right and returns measured distance |
| `lookLeft()` | Scans left and returns measured distance |
| `readPing()` | Reads ultrasonic distance and handles zero echo |
| `moveStop()` | Stops both motors |
| `moveForward()` | Drives both motors forward |
| `moveBackward()` | Drives both motors backward |
| `turnRight()` | Counter-rotates motors to turn right |
| `turnLeft()` | Counter-rotates motors to turn left |

The variable `goesForward` is updated by movement functions but is not used in the supplied decision logic. It can be removed unless it is intended for future functionality.

## 7. Integration with the INK-A-BOT filtration subsystem

The mobile-navigation sketch is only one part of the full INK-A-BOT concept. The following is the proposed integration plan, not functionality already present in the supplied code.

### 7.1 Filtration air path

```text
SURROUNDING AIR
      |
      v
Inlet grille / optional coarse pre-filter
      |
      v
PM2.5-rated particulate filter
      |
      v
Sealed HEPA filter
      |
      v
Activated-carbon adsorption stage
      |
      v
Blower and exhaust
```

- The PM2.5-rated filter and HEPA filter capture airborne particles according to their specifications.
- Activated carbon adsorbs certain gas-phase compounds; it does not replace particulate filtration.
- A dedicated electronic PM sensor is needed if numerical PM2.5 readings are required.
- The blower must be selected to deliver the required airflow against the pressure drop of the complete filter assembly.
- The airflow sensor can help identify reduced flow, but it does not measure filter efficiency.

### 7.2 Proposed control integration

A future integrated program could coordinate:

1. Navigation and obstacle avoidance.
2. Blower switching through a correctly rated driver.
3. Airflow monitoring and low-flow shutdown.
4. Gas sensor readings for the gases supported by the selected sensor.
5. PM2.5 sensor readings, if fitted.
6. LED display status and fault messages.
7. Battery and system status, if suitable monitoring hardware is added.

The final pin map must be prepared after confirming every sensor module, display interface, motor driver and blower driver. The existing D3, D5, D6, D8–D11 and A4–A5 assignments are already occupied by the supplied navigation sketch.

## 8. Proposed integrated operating modes

| Mode | Intended operation | Current sketch status |
|---|---|---|
| Startup | Initialize controller and check basic hardware | Partially implemented |
| Navigation | Move and avoid obstacles | Implemented in supplied sketch |
| Air sampling | Run intake/blower during a sampling period | Not implemented |
| Filtration monitoring | Monitor airflow and sensor readings | Not implemented |
| Low-airflow fault | Stop blower and alert operator | Not implemented |
| Material service | Stop robot and allow safe filter servicing | Manual design requirement |
| Material evaluation | Laboratory characterization and suitability decision | Outside Arduino control |
| Eco-ink research | Controlled formulation testing if material is approved | Outside Arduino control |

A safety-oriented design should define whether the blower is allowed to operate while the robot is moving. If moving affects sample quality or causes unsafe cable/duct conditions, use a stationary sampling mode. The chosen behavior must be validated on the physical robot.

## 9. Electrical and mechanical integration considerations

1. **Separate motor and logic power appropriately.** Motors can draw high current and create electrical noise. Use a suitable motor supply and regulated logic supply.
2. **Common reference:** Where required by the driver and sensor interfaces, connect grounds correctly. Follow module datasheets.
3. **Power protection:** Use a fuse, correctly rated wiring, secure connectors and a suitable battery protection/charging arrangement.
4. **Blower driver:** Do not connect a blower directly to an Arduino pin. Use a driver rated for its voltage, startup current and operating current.
5. **Servo supply:** Check servo current requirements. A separate regulated supply may be needed; connect grounds appropriately.
6. **Filter sealing:** Prevent air from bypassing the filter media through gaps around the cartridge.
7. **Centre of gravity:** Mount the battery and filter assembly securely so the robot remains stable.
8. **Air intake placement:** Keep the intake away from wheel dust, exhaust recirculation and obstructions where practical.
9. **Service access:** Design a sealed, accessible filter compartment. Do not shake, brush or blow compressed air through loaded HEPA filters.
10. **Heat and ventilation:** Ensure motor driver, battery and electronics remain within their specified operating temperatures.

## 10. Testing and calibration plan

### Navigation tests

- Test each motor direction with wheels lifted before floor testing.
- Confirm that the robot's physical left and right correspond to the code's motor labels.
- Confirm servo right and left scan angles.
- Measure obstacle-distance accuracy at several distances.
- Test objects with different sizes, surfaces and angles.
- Calibrate reverse duration and turning duration on the actual chassis.
- Test low battery behavior and motor-driver temperature.
- Check what happens when the ultrasonic sensor receives no echo.

### Filtration tests

- Record filter model, grade, rated airflow and pressure drop.
- Check filter-housing seals and bypass leakage.
- Measure airflow with clean filters.
- Measure upstream and downstream particulate concentrations using a suitable PM instrument.
- Test activated carbon against a specified target gas using suitable measurement equipment.
- Record filter loading and airflow reduction over time.
- Validate any material-recovery process separately in a qualified laboratory.

Do not claim a removal percentage, safe exhaust, or safe ink without suitable repeatable test evidence.

## 11. Known limitations of the supplied sketch

1. It uses fixed delays (`delay()`), so sensor monitoring and other control tasks pause during those delays.
2. Turning is time-based rather than encoder- or IMU-controlled; turn angle can vary.
3. A zero ultrasonic reading is treated as 200 cm, which may incorrectly classify an uncertain reading as clear space.
4. It compares only right and left distance and does not verify the path after turning until the next loop.
5. It has no explicit emergency-stop input.
6. It does not check battery voltage or motor-driver faults.
7. It does not control the filtration blower or read the air-quality sensors.
8. The `goesForward` variable is not used to make decisions.
9. `BACKWARD_SPEED`, `FORWARD_SPEED` and `TURN_SPEED` need physical calibration.
10. The NewPing library and Servo library must be installed and compatible with the selected Arduino board.

## 12. Future development roadmap

### Phase 1 — Mobile base
- Assemble chassis, motors, L298N and battery.
- Upload and test the supplied obstacle-avoidance sketch.
- Calibrate motor direction, speed and turning.

### Phase 2 — Filtration assembly
- Build a sealed intake and filter housing.
- Install PM2.5-rated, HEPA and activated-carbon stages in the planned airflow path.
- Select a blower based on the complete filter pressure drop.

### Phase 3 — Environmental sensing
- Add a dedicated PM sensor if numerical PM2.5 readings are required.
- Add the selected gas sensor and airflow sensor.
- Add display and fault indications.

### Phase 4 — Integrated control
- Resolve pin allocation and power architecture.
- Combine navigation and filtration control.
- Implement low-airflow shutdown and clear fault states.
- Test whether sampling is performed while stationary or moving.

### Phase 5 — Material research
- Keep collected material contained.
- Arrange laboratory characterization.
- Evaluate suitability and validated processing options.
- Conduct experimental ink formulation only if safety and quality requirements are met.

## 13. Final architecture summary

INK-A-BOT is designed as an integrated environmental robotics concept with two principal engineering subsystems:

- **Mobility and navigation:** Arduino UNO, L298N motor driver, two DC motor channels, servo-mounted ultrasonic sensor and obstacle-avoidance software.
- **Air treatment and monitoring:** intake, PM2.5-rated filter, HEPA filter, activated-carbon stage, blower, airflow and gas sensing, optional PM2.5 measurement and status display.

A third, separate research pathway investigates whether captured carbon-rich particulate material can be safely characterized and potentially reused. This is not performed by the obstacle-avoidance code and requires controlled laboratory evaluation.

**Project vision:** From Pollution to Possibility — From Soot to Ink.

---

## Repository placement

Save this file at the root of the GitHub repository:

```text
INK-A-BOT/
├── README.md
├── workflow.md
├── project-architecture.md
├── research.md
├── Documentation/
│   └── filtration_and_purification_workflow.md
├── Images/
└── Code/
    └── obstacle_avoidance.ino
```

Suggested link from `README.md`:

```markdown
## Project Documentation

- [Project Architecture](project-architecture.md)
- [Research Background](research.md)
- [Filtration and Purification Workflow](Documentation/filtration_and_purification_workflow.md)
- [Complete Working Process](workflow.md)
```
