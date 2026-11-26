# INK-A-BOT — Research Background and Project Differentiation

## 1. Introduction

INK-A-BOT is a proposed mobile robotic system that combines air-quality monitoring, staged particulate filtration and research into the possible recovery of carbon-rich particulate material. Its concept is informed by three different areas:

1. Graviky Labs' pollution-derived ink work — an example of capturing combustion-derived particulate matter and developing pigments and inks from processed material.
2. World Health Organization (WHO) air-pollution research — scientific evidence explaining why particulate pollution, especially PM2.5, is a public-health concern.
3. Swachh Bharat Mission — India's broader cleanliness, sanitation and waste-management initiative.

These references provide context and inspiration. They do not mean that WHO or Swachh Bharat Mission developed or endorsed INK-A-BOT.

## 2. Graviky Labs — KAALINK and AIR-INK

### 2.1 Background

Graviky Labs is an Indian environmental technology company associated with the development of KAALINK and AIR-INK.

- **KAALINK** is a device developed to capture particulate matter from combustion-related exhaust.
- **AIR-INK** is a range of pigment and ink products made using processed pollution-derived carbon-rich particles.

The work is an important precedent for the broad idea that captured pollution-derived material may be processed into a useful pigment. It also demonstrates that collection alone is not enough: the recovered material needs further processing and quality evaluation before it can be used in an ink product.

### 2.2 General process described publicly

1. A capture device is installed in an exhaust stream.
2. Particulate matter is captured using the device's specialized collection technology.
3. Captured material is retained in a collection unit or cartridge.
4. The collected material is sent for controlled processing.
5. The material is assessed and treated to address unwanted contaminants.
6. Processed pigment is used in ink or paint formulations.

**Technical note:** Public descriptions of Graviky's technology discuss specialized electrostatic/plasma-based capture and subsequent processing. The exact proprietary process should not be represented as fully known or reproduced from public summaries. Do not claim that INK-A-BOT uses the same technology.

### 2.3 What INK-A-BOT learns from this research

- Pollution-derived particles may have potential as a secondary raw material.
- Safe collection and controlled handling are essential.
- Material characterization and contaminant testing are necessary.
- Ink production is a separate materials-processing task, not an automatic result of air filtration.

## 3. WHO — Air pollution and PM2.5

### 3.1 Why air pollution matters

The World Health Organization (WHO) publishes evidence and guidance on the health effects of ambient and household air pollution. Fine particulate matter is a major concern because small particles can penetrate deep into the respiratory system and are associated with adverse health effects.

### 3.2 PM2.5 explained

PM2.5 means particulate matter with an aerodynamic diameter of 2.5 micrometres or less.

Potential health impacts associated with exposure to particulate air pollution include:

- Respiratory effects.
- Cardiovascular effects.
- Increased risk of serious disease.
- Adverse effects from both short- and long-term exposure.

### 3.3 WHO statistics — use with dates

WHO's ambient air pollution fact sheet reports that, in 2019, 99% of the global population lived in places where WHO air-quality guideline levels were not met. It also estimates that ambient (outdoor) air pollution caused 4.2 million premature deaths worldwide in 2019. WHO reports a combined estimate of 6.7 million premature deaths annually associated with ambient and household air pollution.

These are WHO-reported global estimates for the stated periods; they should not be presented as measurements made by INK-A-BOT.

### 3.4 Connection to INK-A-BOT

WHO's research establishes the public-health importance of reducing exposure to air pollution. INK-A-BOT proposes an engineering response involving:

- Air intake from the surrounding environment.
- PM2.5-rated particulate filtration.
- HEPA filtration for high-efficiency particle capture.
- Activated-carbon adsorption for certain gas-phase compounds.
- Airflow monitoring and sensor-based system control.

The prototype must be tested before making claims about pollutant-removal efficiency or health benefits. WHO does not certify this project.

## 4. Swachh Bharat Mission — Cleanliness and waste management

### 4.1 Background

Swachh Bharat Mission was launched by the Government of India on 2 October 2014. It is a national programme focused on sanitation, cleanliness and improved waste management.

Its two broad components are:

- **Swachh Bharat Mission-Grameen:** Rural sanitation and solid/liquid waste management.
- **Swachh Bharat Mission-Urban:** Urban sanitation, cleanliness and municipal solid-waste management.

### 4.2 Connection to INK-A-BOT

INK-A-BOT is not an official Swachh Bharat Mission project, and the mission is not a soot-to-ink technology programme. However, the project's broader environmental goals can be discussed in relation to:

- Environmental awareness.
- Resource recovery.
- Responsible handling of collected material.
- Exploring ways to turn a waste-derived material into a useful product, where safety and feasibility are demonstrated.

Use the phrase **“aligned with the broader objectives of cleanliness and resource recovery”**, rather than claiming official partnership or endorsement.

## 5. Comparison — Graviky Labs and INK-A-BOT

| Feature | Graviky Labs / KAALINK and AIR-INK | INK-A-BOT proposed design |
|---|---|---|
| Main focus | Capturing exhaust particulate matter and developing pollution-derived ink | Mobile environmental air sampling, staged filtration and investigation of material recovery |
| Deployment concept | Capture device associated with combustion exhaust systems | Mobile robotic platform intended for selected outdoor environments |
| Capture approach | Specialized capture technology publicly described as electrostatic/plasma-based | PM2.5-rated filter and HEPA filter media |
| Gas treatment | Proprietary technology and downstream processing; do not assume identical stages | Activated-carbon cartridge intended to adsorb selected gas-phase compounds |
| Control and monitoring | Device-specific capture arrangement | Arduino UNO-based monitoring and control concept |
| Airflow monitoring | Depends on the device design | Airflow sensor planned to detect normal or reduced flow |
| Particle collection | Dedicated collection unit/cartridge | Particles retained in filter media or a separately designed sealed collection cassette |
| Material processing | Graviky's own controlled processing and formulation | Proposed laboratory characterization, suitability assessment and validated processing |
| Final output | Commercial AIR-INK products | Experimental eco-ink is a future research goal, not yet a demonstrated output |

### Main difference

Graviky Labs has demonstrated a pollution-derived ink pathway using a specialized exhaust-particle capture approach. INK-A-BOT proposes a mobile platform that combines ambient-air sampling, staged physical filtration, sensor monitoring and a separate research pathway for safe material evaluation.

The broad pollution-to-ink concept is not new. INK-A-BOT's proposed distinction is its system integration and implementation approach. This distinction must be supported by a working prototype, test data and a review of existing patents and products before claiming novelty.

## 6. Proposed innovation areas for INK-A-BOT

### 6.1 Mobile air sampling

A mobile platform could be used to sample air at selected locations rather than being restricted to one fixed installation. The actual mobility and sampling performance depend on the completed robot design.

### 6.2 Multi-stage filtration

The proposed filtration train includes:

1. Protective intake grille and optional coarse pre-filter.
2. PM2.5-rated particulate filter.
3. Sealed HEPA filter.
4. Activated-carbon adsorption stage.
5. Blower and exhaust.

The PM2.5 filter and HEPA filter are particulate-capture stages. Activated carbon primarily adsorbs certain gases and odours; it does not replace particle filtration.

### 6.3 Sensor-based monitoring

The Arduino UNO can coordinate sensor readings and control outputs. Depending on the selected sensor models, the system may monitor:

- Airflow.
- Selected gases.
- PM2.5 concentration, if a dedicated PM sensor is installed.
- Obstacle distance, if an ultrasonic sensor is used for robot navigation.
- System status through an LED display.

A gas sensor is specific to the gases it is designed to detect. An airflow sensor does not measure filter efficiency. A filter cartridge is not a PM2.5 measuring sensor.

### 6.4 Controlled material-recovery research

Captured soot or dust is not automatically pure carbon or safe pigment. Roadside particulate matter may contain metals and harmful organic compounds. Material recovery must therefore be designed as a separate, contained operation.

A responsible research pathway is:

1. Keep used filters and collected material sealed.
2. Record the source, collection date and filter stage.
3. Arrange laboratory characterization for composition and hazardous contaminants.
4. Decide whether the sample is suitable for further work.
5. Use a qualified laboratory to select and validate any purification process.
6. Re-test the treated material.
7. Only if it meets relevant safety and quality requirements, conduct controlled experimental ink-formulation tests.

Do not scrape, shake, brush or blow compressed air through loaded HEPA filters to recover soot. Do not use unknown roadside soot in consumer ink, skin-contact products or ordinary printers.

## 7. Research gap and project positioning

The research reviewed here points to three different contributions:

- WHO documents the air-pollution health problem.
- Graviky Labs demonstrates an existing route for capturing combustion-derived particles and developing pollution-derived inks.
- Swachh Bharat Mission provides a national context for cleanliness and waste-management objectives.

**INK-A-BOT's proposed focus:** integrate mobile environmental sampling, staged particulate filtration, selected gas treatment, Arduino-based monitoring and a safe, separately validated material-recovery research pathway.

This is a proposed engineering direction, not proof that the system is more efficient than existing products. A defensible claim of innovation requires a literature and patent review, a working prototype and repeatable performance testing.

## 8. Presentation-ready speech

Our project, INK-A-BOT, is inspired by research and initiatives related to air pollution and sustainable resource recovery.

The World Health Organization highlights the health risks associated with air pollution, particularly fine particulate matter such as PM2.5. This establishes the need for effective air-quality management.

We also studied Graviky Labs, an Indian environmental technology company associated with KAALINK and AIR-INK. Their work demonstrates that captured combustion-derived particulate matter can be processed into pigments and inks under controlled conditions.

In addition, the Swachh Bharat Mission promotes cleanliness, sanitation and improved waste management across India.

Based on these research foundations, we propose INK-A-BOT: a mobile robotic system integrating PM2.5 filtration, HEPA filtration, activated-carbon treatment, Arduino UNO control, gas sensing and airflow monitoring.

Unlike the exhaust-associated capture approach demonstrated by Graviky Labs, our proposed design focuses on mobile environmental air sampling and a multi-stage filtration arrangement. We also propose a separate, safety-focused research pathway to evaluate whether captured carbon-rich material can be recovered and reused.

Our aim is not to claim that pollution-to-ink technology is entirely new, but to develop and test a different integrated robotic approach to particulate collection and potential resource recovery.

## 9. Possible questions from judges

### Q1. Hasn't Graviky Labs already converted air pollution into ink?

Yes. Graviky Labs has demonstrated pollution-derived ink products. INK-A-BOT's proposed distinction is its mobile air-sampling platform, staged filtration and sensor-based monitoring, with a separate material-recovery research pathway.

### Q2. Why use both a PM2.5 filter and a HEPA filter?

They are separate particulate-filtration stages with potentially overlapping capture ranges. Their selection should be justified using their datasheets, pressure-drop characteristics and measured performance.

### Q3. Does activated carbon remove PM2.5?

No. Activated carbon is mainly used to adsorb certain gas-phase compounds. PM2.5 particles are captured by the particulate-filter stages.

### Q4. Does the HEPA filter give us reusable soot?

Not directly. It traps particles within its media. A separate sealed collection design and controlled handling procedure would be needed to investigate material recovery safely.

### Q5. Does Arduino purify the collected material?

No. Arduino UNO controls and monitors electronic components. Material characterization, purification and ink formulation require separate laboratory processes.

### Q6. What is the main limitation?

Filter loading and airflow resistance, battery runtime, sensor accuracy, particle-collection efficiency and the safety of recovered material are key challenges requiring testing.

### Q7. What is the project's main contribution?

The proposed integration of a mobile robotic platform, multi-stage filtration, sensor-based monitoring and a research pathway for safe material recovery.

## 10. References and further reading

Use these sources in the presentation bibliography. Check the original publication for exact figures and context before presenting them.

1. **World Health Organization — Ambient (Outdoor) Air Pollution:**  
   https://www.who.int/news-room/fact-sheets/detail/ambient-(outdoor)-air-quality-and-health

2. **World Health Organization — WHO Global Air Quality Guidelines:**  
   https://www.who.int/publications/i/item/9789240034228

3. **Government of India — Swachh Bharat Mission-Grameen:**  
   https://swachhbharatmission.ddws.gov.in/

4. **Government of India — Swachh Bharat Mission-Urban:**  
   https://sbmurban.org/

5. **MIT News — Graviky Labs / AIR-INK background:**  
   https://news.mit.edu/2017/air-ink-captures-pollution-art-1025

6. **Graviky Labs — AIR-INK:**  
   https://www.air-ink.com/

---

## Final project statement

**INK-A-BOT explores a mobile, sensor-integrated approach to air-pollution particulate collection through staged filtration, while investigating the safe recovery and potential reuse of captured carbon-rich material.**

**Presentation reminder:** Clearly label the robot as a proposed or developing prototype wherever testing is incomplete. Do not claim measured removal efficiency, safe ink production, WHO approval, Swachh Bharat endorsement or a first-ever pollution-to-ink invention without evidence.
