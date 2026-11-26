# INK-A-BOT — Filtration and Material-Purification Workflow

### Detailed engineering guide for PM2.5 filtration, HEPA filtration, activated-carbon treatment, airflow monitoring, particle collection and safe material evaluation

**Controller:** Arduino UNO  
**Purpose:** Draw a controlled air sample through a sealed filter train, capture particulate matter, treat certain gas-phase contaminants, monitor operation, and safely evaluate whether any recovered carbon-rich material is suitable for further research.

> **Scope:** This is a proposed prototype design, not a claim that the robot removes every pollutant or automatically converts roadside soot into safe ink. Performance and safety must be validated by testing.

## 1. Understand the three different jobs

| Stage | Main job | Important limitation |
|---|---|---|
| PM2.5-rated particulate filter | Captures particles according to its media rating | It is not an electronic PM2.5 measuring sensor |
| HEPA filter | High-efficiency capture of airborne particles | It does not remove all gases or vapours |
| Activated-carbon stage | Adsorbs certain gas-phase compounds and odours | It is not a substitute for a particle filter |

A separate electronic PM sensor is required to measure numerical PM2.5 concentration. A gas sensor detects only the gases it is designed and calibrated to detect. Neither sensor replaces physical filters.

## 2. Recommended air path

![INK-A-BOT filtration and purification flow](Images/filtration_and_purification_flow.png)

```text
SURROUNDING AIR
     |
     v
[Inlet grille / coarse protective screen]
     |
     v
[Optional coarse pre-filter]
     |
     v
[PM2.5-rated particulate filter]
     |
     v
[Sealed HEPA filter]
     |
     v
[Activated-carbon adsorber]
     |
     v
[Airflow measurement point, as appropriate]
     |
     v
[Blower / turbofan]
     |
     v
[Exhaust outlet]
```

A draw-through arrangement, with the blower downstream of the filters, can keep much of the filter housing under negative pressure during operation and help reduce outward leakage if the enclosure is properly sealed. The blower must be selected to overcome the pressure drop of the complete filter train.

**Sensor placement matters:** Install the airflow sensor in a suitable straight duct section according to its datasheet. Avoid sharp bends, fan turbulence and abrupt transitions unless the manufacturer permits them.

### Why this order?

1. The inlet screen prevents large debris from entering.
2. The optional pre-filter catches larger dust and protects downstream media.
3. The PM2.5-rated filter provides an upstream particulate-capture stage.
4. The HEPA stage provides high-efficiency fine-particle capture.
5. Activated carbon is placed after particle filtration so dust does not prematurely foul the carbon bed.
6. The blower moves air through the resistance of the complete filter train.

The PM2.5-rated stage and HEPA stage may overlap in the particle sizes they capture. Their actual performance depends on media specification, sealing, face velocity, loading and test conditions. Do not claim a removal percentage without suitable testing.

---

# PAGE 1 — Air intake and pre-filtration

## 3. Air intake assembly

**Purpose:** Bring the selected surrounding-air sample into the robot in a controlled direction.

**Hardware:** Intake grille, duct or flexible hose, sealed filter housing, gaskets, clamps, optional coarse pre-filter and protective fan guard.

**Working steps:**

1. Position the intake to sample the intended surrounding air. Do not place it directly against an exhaust pipe or concentrated emission source.
2. Fit a protective grille to stop leaves, insects and large debris entering the duct.
3. Route the duct to the filter housing with as few sharp bends as practical.
4. Seal joints so air cannot bypass the filter stages.
5. Fit an optional coarse pre-filter if the environment contains larger dust or debris.
6. Make the pre-filter accessible for inspection and replacement.
7. Ensure the intake cannot draw in clothing, fingers or loose objects.

**Arduino UNO role:** The UNO does not draw air. It can switch the blower through a correctly rated driver and read the airflow sensor.

## 4. Coarse pre-filter

**Purpose:** Capture larger debris and reduce loading on finer filters.

**Working steps:**

1. Incoming air passes through the coarse screen or pre-filter.
2. Larger particles and debris are retained.
3. Partially pre-filtered air moves to the PM2.5-rated stage.
4. Inspect the pre-filter regularly.
5. Replace or service it according to its design and manufacturer instructions.

Do not wash a filter unless it is explicitly designed to be washable. Never clean a loaded filter by blowing compressed air through it.

---

# PAGE 2 — PM2.5 particulate filtration

## 5. PM2.5-rated filter stage

**Purpose:** Capture airborne particles using filter media selected for the intended particle range and airflow.

**Hardware:** PM2.5-rated filter cartridge or media, rigid frame, perimeter gasket, sealed access cover and optional upstream/downstream sample ports.

**Working steps:**

1. Air leaving the pre-filter enters the PM2.5-rated filter.
2. Particles are captured according to the media design and rated performance.
3. Retained particles accumulate on or within the media.
4. Air continues towards the HEPA stage.
5. Inspect for damage, poor seating and visible loading.
6. Replace the filter when its manufacturer service criteria or measured pressure-drop limit is reached.

**Design requirements:**
- Obtain the filter datasheet and record its stated efficiency, test method, airflow range and pressure drop.
- Seal the full perimeter; bypass air defeats the purpose of the stage.
- Do not claim “PM2.5 removed” as a measured result unless upstream/downstream measurements support it.

### Measurement is separate from filtration

If the project must show a numerical PM2.5 reading:
- Add an electronic PM2.5 sensor with a suitable sampling arrangement.
- Record its exact model and measurement range.
- Show measured concentration and units on the display.
- For performance testing, compare upstream and downstream readings under repeatable conditions.

A PM2.5 filter is a passive capture component; it does not send a concentration reading to Arduino UNO.

---

# PAGE 3 — HEPA filtration

## 6. HEPA filter stage

**Purpose:** Capture a high proportion of airborne particles reaching the HEPA media, subject to the filter's certified grade and operating conditions.

**Hardware:** HEPA cartridge with documented grade and test standard, rigid frame, continuous perimeter gasket, retaining clips and sealed housing.

**Working steps:**

1. Air from the upstream particulate stage enters the HEPA filter.
2. Air is drawn through the filter media.
3. Fine particles are captured within the media.
4. Filtered air proceeds to the activated-carbon stage.
5. Keep the cartridge installed as a sealed unit; do not shake or brush it to recover dust.
6. Inspect for tears, gaps, deformation and excessive loading.
7. Replace according to manufacturer instructions and prototype service criteria.

### Critical installation points

- Support the filter so airflow does not deform it.
- Use a continuous gasket around the filter perimeter.
- Select a blower that can deliver the required airflow at the filter train's operating pressure drop.
- Do not claim “100% filtration.”
- Record the filter grade and certification from the supplier's datasheet.

### Important for soot recovery

A HEPA filter captures particles within its fibrous media. It does not normally deliver a clean pile of soot into a separate chamber. Scraping or blowing captured soot out can release hazardous dust and damage the filter.

If recoverable material is a project requirement, treat this as a separate design problem. Investigate a purpose-designed, sealed and removable collection stage that can be handled and evaluated safely. Do not assume a HEPA cartridge is a safe or practical pigment-harvesting device.

---

# PAGE 4 — Activated-carbon filtration

## 7. Activated-carbon adsorption stage

**Purpose:** Adsorb certain gas-phase compounds and odours from air after particulate filtration.

**Hardware:** Activated-carbon cartridge or bed, sealed housing, retaining screens/media supports, gaskets and optional sample ports before and after the carbon stage.

**Working steps:**

1. Air leaving the particle filters enters the activated-carbon stage.
2. Compatible gas molecules may be adsorbed onto the porous carbon surface.
3. Treated air leaves the carbon housing and moves towards the blower/exhaust.
4. The carbon media gradually becomes loaded.
5. Replace it according to its rated service life, target contaminant, operating conditions or suitable breakthrough testing.

### Why carbon comes after particle filters

Dust can coat or block the carbon surface and reduce useful adsorption capacity. Upstream particulate filtration helps protect the carbon stage.

### Limitations

- Activated carbon does not remove every gas.
- Performance depends on gas species, humidity, carbon type, contact time, bed depth and airflow.
- A general gas sensor cannot prove all gases have been removed.
- Select carbon media for the intended target compounds.
- Do not describe exhaust air as safe to breathe solely because it passed through activated carbon.

---

# PAGE 5 — Blower, airflow monitoring and Arduino control

## 8. Blower / turbofan

**Purpose:** Create the pressure difference needed to pull air through the filter train.

**Hardware:** DC blower/turbofan, correctly rated MOSFET driver or relay module, fuse, protected wiring, mounting bracket and duct connections.

**Working steps:**

1. Operator starts a collection cycle or valid control logic requests one.
2. Arduino UNO checks required sensor and safety states.
3. Arduino sends a low-current control signal to the driver.
4. The driver switches the blower's separate power circuit.
5. The blower draws air through the intake and filters.
6. The airflow sensor reports whether air is moving.
7. If airflow falls below the configured limit, the UNO stops the blower and displays a warning.
8. At the end of the cycle, the blower is switched off.

**Selection rule:** Choose the blower using its airflow-versus-static-pressure curve at the expected filter resistance. Its free-air rating is not the airflow it will deliver through several filters.

## 9. Airflow detection sensor

**Purpose:** Detect normal, reduced or absent airflow.

**Working steps:**

1. Mount the sensor in a suitable duct section according to its datasheet.
2. Read its output with the blower off to establish a baseline.
3. Start the blower and record normal operation with clean filters.
4. Set a conservative low-flow warning threshold from measured tests.
5. During operation, compare readings with the expected range.
6. If airflow is too low, stop collection and request inspection of intake, duct, filters, seals and blower.

An airflow sensor is not a filter-efficiency meter. It can indicate a flow problem but cannot independently identify which filter is clogged.

## 10. Arduino UNO and display logic

**Arduino UNO tasks:**
- Read the gas sensor.
- Read the airflow sensor.
- Read the ultrasonic sensor if the robot is mobile.
- Read a PM2.5 sensor if fitted.
- Update the LED display.
- Switch the blower through a correctly rated driver.
- Stop the blower during a defined fault condition.

**Suggested display states:**
- `SYSTEM: READY`
- `MONITORING`
- `COLLECTION: ON`
- `AIRFLOW: NORMAL`
- `AIRFLOW: LOW — CHECK FILTER`
- `SENSOR: FAULT`
- `COLLECTION: STOPPED`

Do not display a fabricated AQI or PM2.5 number. Label raw sensor values accurately and use calibrated units only where calibration supports them.

---

# PAGE 6 — Particle collection, purification research and ink suitability

## 11. What happens to particles after filtration?

Particles captured by a PM filter or HEPA filter remain on or inside the filter media. The activated-carbon stage primarily retains adsorbed gas molecules. These are different mechanisms.

**Prototype handling sequence:**

1. Complete the collection run.
2. Switch off the blower.
3. Isolate power before opening a service panel.
4. Keep loaded filters sealed.
5. Record which filter stage contains the sample.
6. If a sample is needed for research, use a purpose-designed sealed collection cassette and an approved controlled handling procedure.
7. Do not shake, brush, use an ordinary vacuum cleaner or blow compressed air through loaded filters.
8. Store any recovered sample in a sealed, labelled container and arrange suitable laboratory evaluation.

## 12. Purification is not the same as filtration

The robot's air filters treat the airflow. They do **not** automatically purify collected soot into safe pigment.

Before considering ink production:

1. **Traceable sampling:** Record source, date, collection stage and handling history.
2. **Material characterization:** Determine composition and check for hazardous contaminants using a suitably equipped laboratory.
3. **Suitability decision:** Decide whether the sample is appropriate for further research. Reject material that cannot meet intended safety requirements.
4. **Validated purification research:** Qualified personnel select a method based on analytical results and perform it with suitable containment and waste controls.
5. **Post-treatment verification:** Test the treated material again; do not assume treatment removed contaminants.
6. **Formulation testing:** Only material that passes relevant safety and quality checks may be considered for a controlled experimental formulation.

Roadside and combustion-derived particulate matter can contain carbonaceous particles, metals, organic compounds and other contaminants. Black colour does not prove purity. HEPA capture does not make dust non-toxic.

**This guide intentionally does not provide a do-it-yourself chemical washing, heating, solvent extraction or purification recipe for unknown roadside soot.** Such treatment can expose people to hazardous material, create contaminated waste or fail to remove contaminants. Use a qualified laboratory and validated method.

## 13. Ink formulation is a separate subsystem

If a characterized pigment is approved for research:

1. Select the intended ink type first (for example, demonstrator marker ink or a paint-like formulation).
2. Select a compatible binder and formulation system.
3. Use a contained mixing vessel and appropriate measuring equipment.
4. Evaluate dispersion, settling, viscosity, drying, adhesion and dispensing performance.
5. Check material safety and cartridge compatibility.
6. Store the experimental formulation in a sealed, labelled container.
7. Do not use it on skin, in consumer products or in a printer unless it has passed relevant safety and compatibility tests.

The Arduino UNO does not perform chemical purification or ink formulation. Those tasks require a separate controlled processing and testing setup.

---

# PAGE 7 — Testing, maintenance and final checklist

## 14. Validation plan

| Test | What to verify | Evidence to record |
|---|---|---|
| Housing leakage | Seals and filter bypass | Defects and corrective action |
| Airflow baseline | Flow with clean filters | Flow and operating condition |
| Filter pressure drop | Pressure across stages/train | Pressure drop and filter condition |
| PM performance | Upstream/downstream PM readings | Values, units and test conditions |
| HEPA integrity | Supplier certification and suitable integrity test | Grade and test evidence |
| Carbon performance | Target-specific gas test | Gas, conditions and results |
| Fault response | Low airflow or sensor fault response | Whether blower stops and warning appears |
| Display operation | Correct status and units | Display photographs |
| Battery runtime | Runtime under intended load | Runtime and battery voltage |
| Collection containment | Sealed cassette and handling | Inspection record |
| Material safety | Laboratory characterization | Laboratory report and suitability decision |

Do not use smell as a reliable gas-removal test. A single low-cost sensor is not proof of certified filtration efficiency.

## 15. Filter maintenance workflow

1. Stop the collection cycle.
2. Switch off and isolate blower and robot power.
3. Follow the filter manufacturer's service instructions.
4. Inspect the intake screen and pre-filter.
5. Check PM2.5-stage media for loading or damage.
6. Check the HEPA cartridge and gasket without disturbing the media.
7. Check the activated-carbon cartridge and service life.
8. Inspect housing seals, duct joints and retaining clips.
9. Replace damaged or exhausted media with the specified replacement.
10. Close and seal the housing before restarting.
11. Record service date, filter identification and reason for replacement.
12. Recheck airflow after maintenance.

Loaded filters and recovered dust must be handled and disposed of according to their hazard assessment and applicable local requirements.

## 16. Complete filtration hardware checklist

### Air intake and movement
- [ ] Intake grille
- [ ] Duct or flexible hose
- [ ] Optional coarse pre-filter
- [ ] DC blower / turbofan
- [ ] Blower driver
- [ ] Fan guard
- [ ] Sealed filter housing and gaskets

### Particulate filtration
- [ ] PM2.5-rated filter with datasheet
- [ ] HEPA filter with documented grade
- [ ] Secure filter frames and retaining clips
- [ ] Optional pressure measurement ports/instrumentation

### Gas treatment
- [ ] Activated-carbon cartridge suitable for target gases
- [ ] Sealed carbon housing
- [ ] Replacement carbon media

### Monitoring and control
- [ ] Arduino UNO
- [ ] Gas sensor matched to target gas
- [ ] Airflow sensor
- [ ] PM2.5 electronic sensor, if numerical PM readings are required
- [ ] LED display
- [ ] Ultrasonic sensor, if mobile navigation is required
- [ ] Driver circuit and protected wiring

### Power and protection
- [ ] 12V rechargeable battery
- [ ] Compatible charger
- [ ] Master and collection switches
- [ ] DC-DC voltage regulator
- [ ] Fuse and holder
- [ ] Suitable connectors and cable protection

### Collection and research
- [ ] Sealed collection cassette or chamber
- [ ] Sealed sample containers
- [ ] Laboratory characterization access
- [ ] Approved contained processing equipment
- [ ] Compatible mixing and storage equipment, only after material approval

## 17. Final process summary

```text
AIR INTAKE
   |
   v
PROTECTIVE GRILLE
   |
   v
OPTIONAL COARSE PRE-FILTER
   |
   v
PM2.5-RATED PARTICULATE FILTER
   |
   v
SEALED HEPA FILTER
   |
   v
ACTIVATED-CARBON ADSORPTION STAGE
   |
   v
BLOWER / EXHAUST
   |
   +---- AIRFLOW MONITORING AND FAULT CONTROL
   |
   v
SEALED PARTICLE COLLECTION / FILTER SERVICE
   |
   v
CONTROLLED SAMPLE HANDLING
   |
   v
LABORATORY CHARACTERIZATION
   |
   v
SUITABILITY DECISION AND VALIDATED PURIFICATION
   |
   v
SUPERVISED INK FORMULATION TESTS
   |
   v
CARTRIDGE COMPATIBILITY AND FINAL TESTING
```

## 18. INK-A-BOT engineering principle

**The filtration train treats the air. The controlled recovery and laboratory process evaluates the captured material. These are separate operations.**

INK-A-BOT's strongest and most defensible technical contribution is the integration of sensor-monitored air intake, staged particulate filtration, activated-carbon gas treatment, airflow fault detection and a documented pathway for safe material-recovery research.

> **FROM POLLUTION TO POSSIBILITY — FROM SOOT TO INK.**

---

## Repository placement

Save this file as:

`Documentation/filtration_and_purification_workflow.md`

Suggested repository structure:

```text
INK-A-BOT/
├── README.md
├── workflow.md
├── Documentation/
│   └── filtration_and_purification_workflow.md
└── Images/
    └── filtration_and_purification_flow.png
```

Add the diagram in this document using:

```markdown
![INK-A-BOT filtration and purification flow](../Images/filtration_and_purification_flow.png)
```

**Document status:** Proposed engineering workflow. Replace assumptions with selected component datasheets, circuit details, measured airflow, filter test results and laboratory findings as the prototype develops.
