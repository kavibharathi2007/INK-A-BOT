# INK-A-BOT — Complete System Workflow

### Air-Pollution Collection, Particulate Recovery and Experimental Eco-Ink Development


**Controller:** Arduino UNO  
**Main subsystems:** Air intake · Air-quality monitoring · Filtration · Soot/particle collection · Material processing · Ink mixing and binding · Cartridge storage · Final output

---

## Project workflow reference image

The following image is the seven-stage workflow supplied for this project. It is the visual reference for the sequence explained in this document.

**Seven stages shown in the reference image**

1. Air intake
2. Filtration
3. Soot collection
4. Air-quality monitoring and Arduino UNO control
5. Mixing and binding
6. Ink cartridge storage
7. Final output

**Important interpretation:** The reference image is a concept workflow. It does not prove that every stage has already been built or tested. This document describes the intended system and identifies the additional hardware needed to implement the processing and ink-storage stages.

---

# Project purpose, system overview and operating sequence

## 1.1 Problem addressed

Air in traffic-dense and industrial environments can contain suspended particulate matter and gaseous pollutants. INK-A-BOT is proposed as a mobile system that draws a controlled sample of surrounding air through a filtration unit, captures particulate matter, and investigates the recovery of a suitable carbon-rich fraction for possible use as an ink pigment.

The project connects two activities:

- **Air treatment:** drawing air through staged filters to reduce the particulate content of the treated airflow and adsorb certain gaseous compounds.
- **Material recovery research:** safely collecting and characterizing captured material before any decision is made about whether it is suitable for an experimental ink formulation.

INK-A-BOT should not be described as removing all pollution from a street or as automatically converting every captured particle into safe ink. Its performance must be measured and validated.

## 1.2 Main system blocks

| Block | Main hardware | Main responsibility |
|---|---|---|
| Power | 12V rechargeable battery, power switches, fuse, regulators | Supply and distribute electrical power |
| Control | Arduino UNO | Read sensors and coordinate outputs |
| Gas monitoring | Gas sensor | Detect selected gases within the sensor's capability |
| Particle monitoring | PM2.5 sensor, if fitted | Measure airborne PM2.5 concentration |
| Airflow monitoring | Airflow sensor | Check that air is moving through the duct |
| Navigation | Ultrasonic sensor, motor driver and drive motors, if mobile | Detect obstacles and support movement control |
| Air intake | Intake grille, duct and blower/turbofan | Draw air into the filtration path |
| Filtration | Pre-filter/PM2.5 filter, HEPA filter, activated-carbon stage | Capture particles and adsorb certain gases |
| Collection | Sealed collection chamber or removable filter cassette | Retain captured material for controlled handling |
| Processing | Enclosed processing vessel and mixing equipment | Conduct controlled material preparation experiments |
| Storage/output | Compatible ink cartridge or sealed container and dispensing device | Store and demonstrate the tested formulation |
| User interface | LED display | Show readings, operating state and warnings |

## 1.3 End-to-end operating sequence

1. The operator checks the robot, filters, collection chamber, wiring and battery.
2. The main power switch is turned on.
3. The voltage-regulated supply powers the Arduino UNO and compatible sensors.
4. Arduino UNO starts the sensors and display and checks whether the readings are available.
5. The gas sensor monitors the gases it is designed to detect. A PM2.5 sensor is required if numerical PM2.5 measurements are to be displayed.
6. The ultrasonic sensor checks for nearby obstacles while the robot is moving.
7. When the operator or programmed control logic requests collection, the blower is switched on through a correctly rated driver.
8. Polluted air travels through the intake duct and staged filters.
9. Captured particles remain in the designated filter or collection stage. Airflow is monitored to identify reduced flow or a possible blockage.
10. The display reports operating status and warnings.
11. After shutdown, captured material is handled using a controlled, sealed recovery procedure.
12. Only a characterized and appropriately purified material may proceed to supervised ink-formulation experiments.
13. A tested formulation may be transferred to a compatible sealed cartridge and evaluated as a demonstration output.

---

#  Power, Arduino UNO and sensor-control workflow

## 12V rechargeable battery

**Activity:** Supplies portable electrical power to the robot.

**Working process:**

1. The charged battery provides the system's 12V supply.
2. A protected power-distribution path separates the loads that require different voltages.
3. A suitable DC-DC regulator supplies the required regulated voltage to the Arduino UNO and compatible sensors.
4. The blower and any motors receive power through appropriately rated driver circuits.
5. The battery voltage should be monitored so that the system can warn the operator before the supply becomes too low.

**Hardware required:** 12V rechargeable battery, compatible charger, battery connector, fuse, master switch, DC-DC buck regulator, wiring and suitable protection.

**Design note:** Do not connect a 12V battery directly to the Arduino UNO 5V pin or to 5V-only sensors. Confirm the voltage and current requirements of every module.

## 2.2 Power switches

**Activity:** Provide controlled power isolation and operator control.

**Working process:**

1. The master switch connects or disconnects the system's protected power input.
2. A separate collection switch may be used to enable or disable the blower circuit.
3. If separate switches are used, their wiring must ensure that the Arduino can still report a fault where appropriate.
4. The operator switches off the collection load before opening or servicing the filter housing.
5. A fuse or suitable electronic protection device protects the circuit against overcurrent.

**Hardware required:** Rated DC switches, fuse and holder, connectors, and protected wiring.

## 2.3 Arduino UNO

**Activity:** Acts as the central controller.

**Working process:**

1. Receives sensor signals from the gas sensor, airflow sensor, ultrasonic sensor and optional PM2.5 measurement sensor.
2. Converts and processes the readings using the appropriate digital or analogue input.
3. Compares readings with configured thresholds and checks whether sensors are responding.
4. Controls the blower through a relay module or MOSFET driver selected for the blower's voltage and current.
5. Updates the LED display with readings and system state.
6. Activates warnings or stops collection when a configured fault condition is detected.

**Hardware required:** Arduino UNO, USB programming cable, suitable sensor interfaces, driver modules, regulated supply and connecting wires.

**Important:** Arduino UNO pins are signal/control pins. They must not directly power a blower, motor or other high-current load.

## 2.4 Gas sensor

**Activity:** Monitors selected gaseous pollutants.

**Working process:**

1. Air from the surrounding environment reaches the gas sensor's sensing element.
2. The sensing element changes its electrical response according to the gases it is designed to detect.
3. The sensor module provides an analogue or digital output.
4. Arduino UNO reads the output and displays a raw reading or a calibrated estimate, depending on the sensor and calibration.
5. If the reading exceeds a configured threshold, the controller can display a warning or request an operator response.

**Hardware required:** Gas sensor module compatible with the target gas, correct power supply, wiring and calibration reference.

**Limitation:** A general-purpose gas sensor does not identify every pollutant and does not automatically provide an accurate AQI value. The exact sensor model, target gases, warm-up time and calibration method must be documented.

## 2.5 PM2.5 measurement versus PM2.5 filtration

These are two different functions:

- A **PM2.5 filter** physically captures particles in the airflow.
- A **PM2.5 electronic sensor** measures the concentration of airborne particles in a sampled air stream.

If INK-A-BOT is expected to show a numerical PM2.5 value on its display, include a compatible PM sensor, such as a suitable optical particulate sensor. The filtration media alone cannot send a PM2.5 reading to Arduino UNO.

---

#  Air intake, blower, airflow detection and filtration

## 3.1 Air intake

**Activity:** Provides the entry path for polluted air.

**Working process:**

1. The intake opening faces the air region selected for sampling.
2. A protective grille prevents large debris from entering the duct.
3. The duct directs the incoming air towards the filtration assembly.
4. The intake should be sealed to prevent unfiltered air from bypassing the filter stages.
5. The air path should be designed so that the operator cannot touch moving fan parts or collected dust.

**Hardware required:** Intake grille, duct or flexible hose, seals, clamps and filter housing.

## 3.2 Turbofan / suction blower

**Activity:** Creates the pressure difference that moves air through the filters.

**Working process:**

1. The Arduino control logic requests an air-collection cycle.
2. A suitable relay or MOSFET driver switches the blower's power circuit.
3. The blower draws air through the intake and filter assembly.
4. Air passes through the filters at a flow rate determined by the blower and the resistance of the filter assembly.
5. The blower is switched off when the cycle ends or when a fault condition requires shutdown.

**Hardware required:** Correctly rated DC blower/turbofan, driver, power wiring, mounting bracket, protective grille and ducting.

**Selection note:** Select the blower using its airflow-versus-static-pressure performance, not only its free-air airflow rating. Filters become restrictive as they load with dust.

## 3.3 Airflow detection sensor

**Activity:** Checks whether air is moving through the system.

**Working process:**

1. The sensor is installed in a suitable duct location.
2. During a collection cycle, it measures airflow or air velocity according to its sensing method.
3. It sends a signal to Arduino UNO.
4. Arduino compares the reading with a configured minimum operating range.
5. If airflow is too low, the system can warn the operator and stop the blower to avoid continued operation under a suspected blockage or failure.

**Hardware required:** Compatible airflow sensor, suitable duct adapter and signal wiring.

**Limitation:** An airflow sensor confirms air movement; it does not prove that the filters are capturing particles efficiently. Filter condition should also be checked through inspection and, where appropriate, differential-pressure measurement.

## 3.4 PM2.5 filtration stage

**Activity:** Captures fine particulate matter in the incoming air.

**Working process:**

1. Air enters the particulate pre-filter or PM2.5-rated filtration stage.
2. The filter media captures a portion of the suspended particles.
3. Captured dust remains on or within the filter media.
4. The partially filtered air proceeds to the next stage.
5. The filter is inspected and replaced or serviced according to its loading and manufacturer guidance.

**Hardware required:** Properly rated particulate filter, sealed frame, filter holder and safe access cover.

**Design note:** State the filter's actual grade and efficiency only when supported by its specification sheet or test results.

## 3.5 HEPA filter

**Activity:** Provides high-efficiency capture of fine airborne particles.

**Working process:**

1. Air leaving the upstream particulate stage enters the HEPA filter.
2. The filter media captures particles through a combination of filtration mechanisms.
3. Captured particles remain in the filter.
4. Filtered air moves to the next treatment stage.
5. The HEPA filter is replaced or serviced safely when its condition or airflow indicates that it is loaded.

**Hardware required:** Correctly specified HEPA filter, sealed filter frame, gasket and access cover.

**Important:** The HEPA filter must be installed without gaps around its edges. Air bypassing the filter can carry untreated particles to the outlet.

## 3.6 Activated-carbon filter

**Activity:** Adsorbs certain gaseous compounds and odors.

**Working process:**

1. Air leaving the particulate filtration stages reaches the activated-carbon media.
2. Certain gas molecules interact with and are adsorbed onto the carbon surface.
3. The treated air proceeds to the exhaust.
4. The media is replaced when exhausted, according to its rated service life or testing.

**Hardware required:** Activated-carbon filter cartridge or bed, sealed housing and retaining mesh.

**Important technical distinction:** Activated carbon is primarily a gas/odor adsorption stage. It should not be described as the main HEPA-like soot or PM2.5 particle filter. A suitable particulate filter should capture soot particles before the carbon stage.

## 3.7 Recommended airflow order

**Air intake → coarse pre-filter (if used) → PM2.5-rated particulate stage → HEPA filter → activated-carbon stage → blower/exhaust**

The blower may be positioned before or after the filter bank depending on the mechanical design. The selected arrangement must keep the filter housing sealed and prevent leakage of contaminated air. Confirm the blower's pressure capability for the chosen arrangement.

---

#  Particle collection and air-quality display

## 4.1 Soot / particulate collection chamber

**Activity:** Retains captured material for controlled recovery.

**Working process:**

1. Particles are captured by the designated removable filter, collection cassette or collection chamber.
2. The operator stops the blower and isolates the power before accessing the collection section.
3. The collection unit is removed or opened only using a controlled procedure that prevents dust release.
4. The recovered material is placed in a sealed, labelled container.
5. The material is sent for characterization before any reuse is considered.

**Hardware required:** Sealed collection chamber or filter cassette, gasket, secure lid, removable tray where appropriate, labelled sample container and safe handling equipment.

**Important design clarification:** A HEPA filter commonly retains particles within its media. It does not automatically deposit all captured soot into a separate chamber. If the project needs a recoverable soot sample, design a dedicated collection cassette or removable collection stage and validate how material can be recovered without releasing dust.

## 4.2 LED display

**Activity:** Gives the operator a visible indication of system operation.

**Working process:**

1. Arduino UNO sends display data to the LED display module.
2. The display shows the system state, such as standby, monitoring, collection active or fault.
3. If a PM2.5 sensor is installed, the measured concentration can be shown.
4. Gas sensor readings can be displayed with the sensor name and units or as a clearly labelled relative reading.
5. Airflow status can be shown as normal, low or fault based on the configured limits.
6. Obstacle distance can be displayed while the robot is moving, if useful.

**Hardware required:** Compatible LED display module, interface wiring and regulated power.

**Suggested display information:**

| Display field | Information |
|---|---|
| System | ON / OFF / STANDBY |
| Gas | Sensor reading and target gas |
| PM2.5 | Concentration, only if a PM sensor is fitted |
| Airflow | Normal / Low / No flow |
| Collection | Active / Stopped |
| Obstacle | Distance or obstacle warning |
| Filter service | Inspection / replacement reminder |

Do not label a raw gas-sensor voltage or arbitrary sensor value as AQI. AQI requires the appropriate pollutant measurements and a defined calculation method.

## 4.3 Ultrasonic sensor

**Activity:** Detects obstacles in front of the mobile robot.

**Working process:**

1. Arduino UNO sends a trigger pulse to the ultrasonic sensor.
2. The sensor emits an ultrasonic burst.
3. The sensor receives the reflected echo from a nearby object.
4. Arduino calculates the distance from the echo travel time.
5. If the measured distance is below the configured safety threshold, the movement controller stops or changes the robot's direction.

**Hardware required:** Ultrasonic module, suitable mounting bracket and wiring.

**Important:** The ultrasonic sensor does not move the robot by itself. A mobile implementation also requires drive motors, a motor driver, a suitable chassis and movement-control code. The sensor is for obstacle detection, not pollution detection.

---

#  Arduino control logic and complete operating cycle

## 5.1 Start-up sequence

1. Operator inspects the intake, filter seals, collection chamber, battery and wiring.
2. Operator turns on the master power switch.
3. The regulated supply powers Arduino UNO and the sensors.
4. Arduino initializes the display and sensor interfaces.
5. Arduino checks that sensor signals are within plausible operating ranges.
6. The display shows READY or a fault message.
7. The blower remains off until a collection cycle is requested and safety checks pass.

## 5.2 Monitoring sequence

1. Read the gas sensor.
2. Read the airflow sensor.
3. Read the ultrasonic sensor.
4. Read the PM2.5 sensor if one is installed.
5. Update the display.
6. Check sensor faults and configured thresholds.
7. Continue monitoring while the system is in standby.

## 5.3 Collection sequence

1. The operator or programmed control rule requests collection.
2. Arduino checks that the power system and required sensors are ready.
3. If the robot is mobile, the navigation logic checks for obstacles.
4. Arduino activates the blower through its driver.
5. Air is drawn through the intake and filtration stages.
6. The airflow sensor confirms whether air is moving.
7. If airflow is below the safe configured limit, Arduino switches off the blower and displays a warning.
8. If airflow is acceptable, the collection cycle continues.
9. The display indicates COLLECTION ACTIVE.
10. At the end of the cycle, the blower is switched off and the system returns to monitoring or standby.

## 5.4 Example control logic

```text
START
  |
  v
MASTER POWER ON
  |
  v
INITIALIZE ARDUINO AND DISPLAY
  |
  v
CHECK SENSOR STATUS
  |
  +---- Sensor fault? ---- YES ---> DISPLAY FAULT / KEEP BLOWER OFF
  |                                  |
  NO                                 v
  |                                WAIT
  v
READ GAS / PM (IF FITTED) / AIRFLOW / DISTANCE
  |
  v
UPDATE DISPLAY
  |
  v
COLLECTION REQUESTED?
  |
  +---- NO ------------------------> CONTINUE MONITORING
  |
 YES
  |
  v
SAFETY CHECKS PASS?
  |
  +---- NO ------------------------> DISPLAY WARNING / DO NOT START
  |
 YES
  |
  v
ACTIVATE BLOWER THROUGH DRIVER
  |
  v
CHECK AIRFLOW
  |
  +---- LOW / NO FLOW ------------> STOP BLOWER / DISPLAY FAULT
  |
 NORMAL
  |
  v
CONTINUE FILTERING
  |
  v
CYCLE COMPLETE?
  |
  +---- NO ------------------------> CONTINUE AIRFLOW CHECK
  |
 YES
  |
  v
STOP BLOWER
  |
  v
DISPLAY CYCLE COMPLETE
  |
  v
RETURN TO MONITORING
```

## 5.5 Example Arduino control pseudocode

This is a logic outline, not a ready-to-upload sketch. Pin numbers, sensor libraries, calibration and thresholds must be filled in after the exact module models are selected.

```cpp
setup:
    initialize Arduino pins
    initialize gas sensor input
    initialize airflow sensor input
    initialize ultrasonic sensor
    initialize optional PM sensor
    initialize LED display
    set blower control OFF
    show system ready

loop:
    read gas sensor
    read airflow sensor
    read ultrasonic distance
    read PM sensor if installed

    update LED display

    if sensor fault:
        turn blower OFF
        show sensor fault

    else if collection requested:
        if safety checks pass:
            turn blower ON through driver
            read airflow

            if airflow is below safe limit:
                turn blower OFF
                show airflow warning
            else:
                continue collection
        else:
            show safety warning

    else:
        keep blower OFF
        continue monitoring
```

## 5.6 Fault conditions to handle

| Condition | Expected response |
|---|---|
| Battery voltage too low | Warn and stop collection safely |
| Gas sensor not responding | Show sensor fault; do not report a valid gas result |
| PM sensor absent or faulty | Do not display a fabricated PM2.5 value |
| Airflow too low | Stop blower and request filter/duct inspection |
| Ultrasonic obstacle detected | Stop or avoid movement, if drive hardware is fitted |
| Blower driver fault | Stop collection and show fault |
| Filter service due | Show inspection/replacement reminder |

---

#  Material processing, ink conversion, cartridge storage and final output

> **This is a separate research and processing stage.** The Arduino-controlled air-filtration robot does not automatically make ink. Material characterization, purification and formulation require additional equipment and supervised testing.

## 6.1 Stage 1: Controlled recovery of collected material

**Activity:** Obtain a sample from the collection stage without releasing dust.

**Working process:**

1. Complete the collection cycle.
2. Switch off the blower and isolate the relevant power.
3. Allow the filter assembly to settle before servicing.
4. Use a sealed removable cassette or controlled collection chamber.
5. Transfer the sample into a sealed, labelled container.
6. Record the sample source, date, collection conditions and filter stage.

**Hardware/equipment:** Sealed collection cassette, sealed sample containers, labels, suitable laboratory handling enclosure and appropriate protective equipment.

**Safety:** Roadside soot may contain toxic metals, organic compounds and other contaminants. Do not brush, blow, dry-sweep or handle it in an open room. Do not use uncharacterized roadside soot in consumer ink, markers, printers or paint.

## 6.2 Stage 2: Material characterization and suitability decision

**Activity:** Determine whether the recovered material contains a suitable carbon-rich pigment fraction and whether contaminants make it unsuitable.

**Working process:**

1. Send representative samples for suitable laboratory characterization.
2. Assess composition and possible hazardous contaminants.
3. Evaluate particle characteristics and consistency.
4. Decide whether the sample can proceed to further purification research.
5. Reject material that cannot be demonstrated to meet the intended safety and quality requirements.

**Additional equipment may include:** Analytical balance, sample containers, laboratory characterization instruments and access to an appropriately equipped testing laboratory.

The project should not assume that black appearance means the sample is pure carbon or safe pigment.

## 6.3 Stage 3: Purification and preparation research

**Activity:** Investigate a validated method to prepare a suitable pigment fraction.

**Working process:**

1. Select a purification method based on laboratory characterization.
2. Conduct the work in a suitable controlled laboratory.
3. Keep the sample contained to prevent airborne dust.
4. Verify the treated material against the required quality and safety criteria.
5. Document the method and test results.

**Additional equipment:** Depends on the validated laboratory method. Do not specify or use a purification recipe until the material composition and hazards are known.

## 6.4 Stage 4: Mixing and binding

**Activity:** Combine a validated pigment with a compatible binder and other formulation ingredients to investigate an ink.

**Working process:**

1. Select a compatible binder and formulation system for the intended output.
2. Use only a characterized, approved pigment sample.
3. Measure ingredients using suitable laboratory equipment.
4. Mix in a closed or controlled vessel using suitable mixing equipment.
5. Assess dispersion, settling, viscosity, adhesion, drying and flow.
6. Record the formulation and test results.
7. Reject formulations that fail safety, stability or performance tests.

**Additional hardware/equipment:** Enclosed mixing vessel, laboratory mixer or stirrer, analytical balance, suitable measuring tools, compatible binder and formulation materials, and testing surfaces.

**Important:** The binder and formulation depend on whether the intended product is marker ink, printing ink or paint. One formula should not be assumed to work for all three.

## 6.5 Stage 5: Ink cartridge storage

**Activity:** Store a validated experimental ink formulation.

**Working process:**

1. Check that the formulation is compatible with the intended cartridge and seals.
2. Transfer the formulation using a suitable filling method.
3. Close and label the cartridge.
4. Record the formulation ID, date and test status.
5. Check for leakage, settling and storage stability.

**Additional hardware:** Compatible ink cartridge or sealed storage bottle, filling syringe or transfer tool, caps, seals and labels.

## 6.6 Stage 6: Final output and demonstration

**Activity:** Demonstrate the performance of the experimental ink in its intended application.

**Working process:**

1. Select the correct output device for the formulation.
2. Load the cartridge or sample container.
3. Test flow, line consistency, drying and adhesion on an appropriate test surface.
4. Record the results and limitations.
5. Present the output as an experimental demonstration only if it passes the required safety and performance checks.

**Additional hardware:** Compatible marker body, controlled dispensing tip, test substrate or suitable printer/paint test equipment depending on the formulation.

## 6.7 Processing-stage summary

| Stage | Activity | Additional equipment |
|---|---|---|
| Recovery | Remove captured sample safely | Sealed cassette and sample container |
| Characterization | Check composition and hazards | Appropriate laboratory analysis |
| Purification | Prepare a suitable pigment fraction | Equipment selected for validated method |
| Mixing and binding | Formulate experimental ink | Enclosed vessel, mixer, balance and binder |
| Cartridge storage | Store validated formulation | Compatible cartridge, seals and filling tool |
| Final output | Test intended use | Compatible marker, dispenser or test apparatus |

---

#  Integrated hardware list, validation, safety and project limitations

## 7.1 Hardware list based on the current project design

### A. Components already specified for INK-A-BOT

| No. | Component | Function |
|---:|---|---|
| 1 | Arduino UNO | Central controller |
| 2 | HEPA filter | Fine-particle capture |
| 3 | Activated-carbon filter | Adsorption of certain gases and odors |
| 4 | PM2.5 filtration media | Particulate capture |
| 5 | Gas sensor | Detection of selected gases |
| 6 | LED display | System status and readings |
| 7 | 12V rechargeable battery | Main power source |
| 8 | Airflow detection sensor | Airflow monitoring |
| 9 | Ultrasonic sensor | Obstacle detection |
| 10 | Power switches | Power isolation and control |

### B. Additional hardware required to complete the air-collection robot

| No. | Additional component | Why it is required |
|---:|---|---|
| 11 | DC turbofan / suction blower | Moves air through the filter system |
| 12 | Blower driver (rated relay or MOSFET circuit) | Allows Arduino to control the blower safely |
| 13 | PM2.5 electronic sensor, if numerical PM readings are required | Measures PM2.5 concentration |
| 14 | Air intake grille and duct | Guides air into the unit |
| 15 | Filter housing and seals | Prevents air bypass around filters |
| 16 | Collection cassette/chamber | Retains material for controlled recovery |
| 17 | DC-DC voltage regulator | Supplies the required logic voltage |
| 18 | Fuse and holder | Overcurrent protection |
| 19 | Battery connector and wiring | Power distribution |
| 20 | Protective fan grille | Prevents contact with moving fan parts |

### C. Additional hardware required if the robot is mobile

| No. | Component | Why it is required |
|---:|---|---|
| 21 | Robot chassis | Mechanical base |
| 22 | DC geared motors | Drive the robot |
| 23 | Motor driver | Controls motor speed and direction |
| 24 | Wheels and supports | Mobility |
| 25 | Motor brackets and fasteners | Mechanical mounting |

The ultrasonic sensor alone does not make the robot mobile. Drive motors, a motor driver and a chassis are also necessary.

### D. Additional equipment required for ink research

| No. | Equipment | Why it is required |
|---:|---|---|
| 26 | Sealed sample containers | Safe sample storage |
| 27 | Enclosed laboratory handling equipment | Controls exposure to collected dust |
| 28 | Characterization/testing access | Checks material composition and hazards |
| 29 | Enclosed mixing vessel | Contains formulation during mixing |
| 30 | Laboratory mixer or stirrer | Disperses the approved pigment |
| 31 | Analytical balance and measuring tools | Controls formulation measurements |
| 32 | Compatible binder and formulation materials | Forms the ink system |
| 33 | Compatible cartridge or sealed bottle | Stores the tested ink |
| 34 | Filling and dispensing tools | Transfers and demonstrates the formulation |

## 7.2 Validation and testing plan

| Test | What to verify | Evidence to record |
|---|---|---|
| Power test | Stable, correct voltage under load | Voltage readings |
| Controller test | UNO starts and reads connected modules | Serial log or test record |
| Gas sensor test | Sensor responds to its target gas and calibration method | Sensor model, calibration and readings |
| PM2.5 test | PM sensor reports plausible concentration, if installed | Reference comparison and readings |
| Airflow test | Air moves through the assembled filter path | Airflow readings |
| Filter sealing test | No obvious bypass around filter frames | Inspection/test record |
| Filtration test | Particle reduction across the system | Upstream/downstream measurements |
| Obstacle test | Ultrasonic sensor detects test objects | Distance readings |
| Display test | Correct status and units are shown | Display photographs |
| Collection test | Captured material remains contained | Inspection and sample log |
| Ink test | Formulation meets intended performance and safety criteria | Test results and limitations |

## 7.3 Safety requirements

- Do not intentionally expose people to vehicle exhaust or concentrated soot to test the robot.
- Use controlled, appropriately assessed test environments.
- Do not open or clean loaded filters in an ordinary room.
- Do not use compressed air or dry brushing to clean soot from filters.
- Treat recovered roadside particulate matter as potentially hazardous.
- Use a suitable contained handling and laboratory process for sample recovery and characterization.
- Do not claim that activated carbon removes all gases or that HEPA removes all pollutants.
- Keep the battery, wiring, blower and electronics protected from dust and accidental short circuits.
- Use a fuse, correctly rated drivers and suitable voltage regulation.
- Stop the blower if airflow indicates a blockage or if the filter housing is damaged.
- Do not use experimental recovered material in products intended for human use until the relevant safety and performance requirements have been independently met.

## 7.4 Project scope and honest claims

**What the robot is designed to demonstrate:**

- Sensor-based environmental monitoring.
- Controlled air intake using a blower.
- Staged particulate filtration.
- Activated-carbon treatment for certain gaseous compounds.
- Airflow and obstacle monitoring.
- Controlled collection and documentation of captured particulate matter.

**What requires additional development and validation:**

- Numerical PM2.5 monitoring, unless a PM sensor is fitted.
- Reliable soot recovery from the filter media.
- Purification and characterization of recovered material.
- Safe and stable ink formulation.
- Cartridge compatibility and final dispensing performance.

## 7.5 Final project workflow

```text
POWER ON
   |
   v
ARDUINO UNO INITIALIZATION
   |
   v
GAS / PM (IF FITTED) / AIRFLOW / OBSTACLE MONITORING
   |
   v
COLLECTION REQUEST AND SAFETY CHECK
   |
   v
BLOWER ACTIVATION
   |
   v
POLLUTED AIR INTAKE
   |
   v
PARTICULATE PRE-FILTER / PM2.5 STAGE
   |
   v
HEPA FILTRATION
   |
   v
ACTIVATED-CARBON TREATMENT
   |
   v
SEALED PARTICLE COLLECTION / FILTER CASSETTE
   |
   v
CONTROLLED SAMPLE RECOVERY
   |
   v
MATERIAL CHARACTERIZATION
   |
   v
VALIDATED PURIFICATION RESEARCH
   |
   v
MIXING AND BINDING EXPERIMENT
   |
   v
INK QUALITY AND SAFETY TESTING
   |
   v
COMPATIBLE CARTRIDGE STORAGE
   |
   v
FINAL EXPERIMENTAL OUTPUT
```

## 7.6 Project vision

**INK-A-BOT connects environmental monitoring, robotic air filtration and material-recovery research in one project.** Its purpose is not only to collect airborne particles, but also to investigate whether a carefully characterized recovered material can become a useful resource.

> **FROM POLLUTION TO POSSIBILITY — FROM SOOT TO INK.**

---

### Repository note

This document describes the proposed design and workflow. Update the hardware list, photographs, circuit diagram, code links and test results as the prototype is actually assembled and validated. Do not mark a feature as completed until it has been demonstrated.
