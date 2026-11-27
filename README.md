# INK-A-BOT
### Turning Air Pollution into a Valuable Resource 

<p align="center">
  <strong>Turning Pollution into Possibility</strong>
  <strong>POLLUTION IN, INK OUT</strong>
</p>


<p align="center">
  <a href=https://www.instagram.com/reel/DfB2N8IPw9a/">
  </a>
</p>

# INK-A-BOT
![INK-A-BOT](./EXACT-IMAGE-PROJECTS%20MODEL.jpeg")

---

## 1. Overview

**INK-A-BOT** is an intelligent mobile robot designed to monitor and collect airborne particulate pollutants, particularly carbon-rich soot, from pollution-prone environments.

The system combines air-quality monitoring, automated mobility, suction-based particle collection, and multi-stage filtration to recover potentially reusable carbon-rich material.

The collected material can then undergo further processing and testing to explore its conversion into usable ink pigment.

Our mission is simple:

> **Don't just detect pollution. Collect it, recover valuable material, and give it a second life.**

## 2. Problem Statement

Air pollution caused by vehicle emissions and industrial activities releases harmful particulate matter into the atmosphere. These pollutants negatively affect environmental quality and human health.

At the same time, carbon-rich soot and other collected particles are often discarded as waste rather than investigated for potential resource recovery.

There is a need for an intelligent, cost-effective, and automated solution that can monitor particulate pollution, collect airborne particles, separate suitable carbon-rich material, and explore its conversion into reusable ink pigment.

## 3. Proposed Solution

INK-A-BOT introduces a mobile robotic system that:

- Monitors surrounding particulate pollution.
- Detects pollution levels using air-quality sensors.
- Moves through designated pollution-prone areas.
- Automatically activates its collection mechanism when required.
- Draws polluted air into a controlled filtration chamber.
- Separates and collects particulate matter.
- Identifies suitable recovered carbon-rich material for further processing.
- Explores the conversion of recovered carbon into ink pigment.

## 4. Project Objectives

1. Develop an intelligent mobile pollution-monitoring robot.
2. Implement autonomous and Wi-Fi-based manual movement.
3. Detect particulate pollution using suitable sensors.
4. Automate the air-suction and collection mechanism.
5. Develop an effective multi-stage filtration arrangement.
6. Investigate carbon-rich particle recovery.
7. Explore sustainable ink production from recovered material.
8. Promote environmental sustainability through waste-to-resource innovation.

## 5. System Architecture

```text
             START
               |
               ▼
       Power ON the Robot
               |
               ▼
      Initialize Controller
               |
               ▼
       Read Air Quality Data
               |
               ▼
       Evaluate Pollution Level
               |
          ┌────┴────┐
          |         |
       Normal    High Pollution
          |         |
          ▼         ▼
       Monitor   Activate Suction
                    |
                    ▼
              Collect Airborne
                Particles
                    |
                    ▼
              Multi-Stage
                Filtration
                    |
                    ▼
              Collect Suitable
               Carbon-Rich
                 Material
                    |
                    ▼
              Further Material
                Processing
                    |
                    ▼
              Ink Pigment
                Testing
                    |
                    ▼
                   END
```

## 6. Hardware Components

| Component | Purpose |
|---|---|
| Arduino Uno | Main control unit |
| ATmega328P | Microcontroller |
| 12V DC 300 RPM Motors | Robot movement |
| L298N Motor Driver | Motor speed and direction control |
| Air Quality / PM Sensor | Particulate pollution monitoring |
| Blower / Vacuum Pump | Air suction |
| HEPA Filter | Fine particle filtration |
| PM2.5 Filter | Particulate collection |
| Activated Carbon Filter | Additional air treatment |
| Wi-Fi Module | Wireless robot control |
| Battery | Power supply |
| Robot Chassis | Mechanical structure |

*Final component selection and electrical connections will be documented during hardware integration.*

##  7. Software & Technologies

- **Embedded Programming:** Arduino C/C++
- **Microcontroller Platform:** Arduino Nano
- **Wireless Communication:** Wi-Fi
- **Sensor Integration:** Air-quality and particulate sensors
- **Motor Control:** L298N motor driver
- **Development Environment:** Arduino IDE
- **Version Control:** Git & GitHub
- **Simulation:** Suitable circuit and logic simulation tools

## 8. Working Principle – Step by Step

### Step 1: System Initialization
The robot powers on and initializes the controller, sensors, motors, and wireless communication system.

### Step 2: Air Quality Monitoring
The particulate sensor continuously measures the surrounding air quality. The controller receives and evaluates the sensor readings.

### Step 3: Pollution Detection
The measured particulate concentration is compared against a configured collection threshold.

### Step 4: Robot Navigation
The robot can be operated through autonomous movement mode.

### Step 5: Automatic Particle Collection
When the configured pollution threshold is exceeded, the suction mechanism is activated.

### Step 6: Multi-Stage Filtration
Polluted air passes through the filtration chamber, where different filter stages capture particulate matter.

### Step 7: Material Recovery
Collected particles are carefully removed and evaluated. Suitable carbon-rich material is separated for further investigation.

### Step 8: Ink Production Experiment
The recovered material undergoes appropriate purification, characterization, and formulation experiments to investigate its suitability as an ink pigment.

### Step 9: Final Demonstration
The project demonstrates pollution monitoring, particle collection, filtration, and the potential transformation of recovered carbon-rich material into ink.

## 9. Key Features

-  Intelligent mobile robotic platform
-  Real-time particulate pollution monitoring
-  Automatic pollution-triggered collection
-  Suction-based particle collection
-  Multi-stage filtration system
-  Carbon-rich material recovery
-  Experimental waste-to-ink conversion
-  Environment-focused innovation

##  10. Innovation & Uniqueness

| Conventional Approach | INK-A-BOT Approach |
|---|---|
| Air pollution monitoring | Monitoring with active particle collection |
| Stationary monitoring systems | Mobile robotic platform |
| Pollutants treated as waste | Investigating material recovery |
| Separate monitoring and collection | Integrated monitoring and collection |
| Conventional ink pigment sourcing | Exploring recovered carbon-rich pigment |

**Our innovation:** Combining mobile pollution monitoring, automated particle collection, and potential carbon-based resource recovery in a single robotic platform.

##  11. Development Roadmap

- [x] Project concept and problem identification
- [x] Initial system planning
- [ ] GitHub repository development
- [ ] Embedded software development
- [ ] Sensor integration
- [ ] Motor control implementation
- [ ] Wi-Fi communication
- [ ] Pollution-triggered automation
- [ ] Suction and filtration integration
- [ ] Hardware prototype assembly
- [ ] Carbon recovery experiments
- [ ] Ink formulation and testing
- [ ] Complete system demonstration

##  12. Repository Structure

```text
INK-A-BOT/
│
├── README.md
│
├── Code/
│   ├── main.ino
│   ├── sensor_monitoring.ino
│   ├── motor_control.ino
│   └── pollution_detection.ino
│
├── Circuit_Diagrams/
│   ├── circuit_diagram.png
│   └── system_architecture.png
│
├── Documentation/
│   ├── project_overview.md
│   ├── working_principle.md
│   └── components.md
│
├── Simulation/
│   └── simulation_details.md
│
├── Images/
│   └── prototype_images/
│
└── LICENSE
```

##  13. Environmental Impact

INK-A-BOT aims to contribute to environmental sustainability by:

- Encouraging localized particulate collection.
- Exploring the recovery of carbon-rich waste materials.
- Reducing the disposal of potentially reusable material.
- Promoting resource efficiency and circular economy concepts.
- Raising awareness of air pollution through practical innovation.

**Important:** This prototype is intended for controlled testing. Filtration does not eliminate all pollution, and collected soot is not automatically safe or suitable for ink production. Material characterization, purification, and safety validation are essential before any reuse.

## 14. Future Enhancements

- GPS-enabled pollution mapping.
- IoT-based live monitoring dashboard.
- Cloud-based pollution data storage.
- AI-assisted pollution analysis.
- Improved autonomous navigation.
- Advanced particle separation technology.
- Automated collection chamber monitoring.
- Optimized carbon recovery and ink formulation.

##  15. Project Team

**Project Name:** INK-A-BOT

**Project Category:** Student Innovation – Hardware

**Domain:** Robotics | IoT | Environmental Sustainability

**Project Theme:** Clean and Green

**Institution:** Sri Ramakrishna Engineering College, Coimbatore

---

##  16. Our Vision

We believe technology should not only solve existing problems but also create opportunities from them.

INK-A-BOT represents an effort to transform environmental challenges into opportunities through robotics, automation, and sustainable engineering.

<p align="center">
  <strong>FROM POLLUTION TO POSSIBILITY.</strong>
  <br/>
  <strong>FROM SOOT TO INK. 🌍🖋️</strong>
</p>

---

⭐ If you find this project interesting, consider starring this repository and following its development!


 DESIGN AND DEVELOPMENT **INK A BOT TEAM** BY ROBOTICS CLUB OF SRI RAMAKRISHNA INSTITUTE TECHNOLOGY
