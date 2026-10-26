# Non-Invasive Detection of Chronic Kidney Disease (CKD)

An Arduino-based biomedical instrumentation project exploring non-invasive measurement of breath ammonia and optical estimation of hemoglobin levels for preliminary Chronic Kidney Disease (CKD) screening research.

## Table of Contents

- [Project Overview](#project-overview)
- [Background](#background)
- [Objectives](#objectives)
- [Key Features](#key-features)
- [System Architecture](#system-architecture)
- [Hardware Components](#hardware-components)
- [Working Principle](#working-principle)
- [Hardware Interfacing](#hardware-interfacing)
- [Software Implementation](#software-implementation)
- [Measurement Parameters](#measurement-parameters)
- [Results and Observations](#results-and-observations)
- [Applications](#applications)
- [Limitations](#limitations)
- [Future Improvements](#future-improvements)
- [Technologies Used](#technologies-used)
- [Project Structure](#project-structure)
- [Disclaimer](#disclaimer)

## Project Overview

Chronic Kidney Disease (CKD) is a long-term condition in which kidney function gradually deteriorates. Early identification and continuous monitoring are important for managing kidney health.

This project presents a low-cost embedded system that investigates two measurable parameters associated with CKD:

1. **Breath ammonia concentration:** Measured using an MQ137 ammonia gas sensor.
2. **Hemoglobin estimation:** Explored using an OPT101 photodetector and red and infrared LEDs.

An Arduino UNO acts as the main controller, acquiring sensor readings and processing the measurements. An LCD is used to display the resulting values.

The project combines embedded systems, gas sensing, optical measurement, and biomedical instrumentation to explore an alternative approach to preliminary health screening.

## Background

The kidneys filter waste products and excess fluids from the blood. When kidney function declines, waste products may accumulate in the body.

Two parameters explored in this project are:

- **Breath ammonia:** Changes in exhaled ammonia concentration have been investigated as a potential indicator associated with impaired kidney function.
- **Hemoglobin:** Anemia is a common complication of CKD and may be associated with reduced erythropoietin production and impaired red blood cell formation.

By investigating these parameters together, the project explores whether a simple embedded platform can support preliminary monitoring research without requiring a blood sample for every measurement.

These parameters are indirect indicators and cannot independently confirm CKD or determine its stage.

## Objectives

- Develop an Arduino-based system for measuring ammonia concentration in exhaled breath.
- Investigate optical estimation of hemoglobin concentration using transmitted light through a finger.
- Interface gas and optical sensors with a microcontroller.
- Process sensor signals into readable measurement values.
- Display the measured values using an LCD.
- Explore a low-cost approach to biomedical measurement and preliminary CKD screening research.

## Key Features

- Breath ammonia sensing using the MQ137 sensor.
- Optical measurement using the OPT101 photodetector.
- Red and infrared LED illumination for the finger probe.
- Arduino-based sensor acquisition and processing.
- LCD output for measurement display.
- Two measurement subsystems integrated into a single embedded platform.
- A low-cost prototype using commonly available electronic components.

## System Architecture

The system consists of two primary measurement subsystems controlled by an Arduino UNO.

### 1. Breath Ammonia Measurement

The breath analyzer uses a mouthpiece, tubing, a one-way valve, a collection bag, and the MQ137 sensor. Exhaled air is collected and exposed to the sensor. The sensor output is read by the Arduino and processed to estimate ammonia concentration.

### 2. Optical Hemoglobin Estimation

A finger probe uses red and infrared LEDs to illuminate the finger. Light transmitted through the finger is detected by the OPT101 photodetector. The resulting electrical signal is read by the Arduino and used by the implemented algorithm to estimate hemoglobin concentration.

### 3. Display Unit

The Arduino processes the readings from both subsystems and sends the corresponding measurement values to the LCD.

**System flow:**

Breath sample → MQ137 sensor → Arduino UNO

Finger illumination → Red/infrared LEDs → Finger tissue → OPT101 photodetector → Arduino UNO

Arduino UNO → Measurement processing → LCD display

## Hardware Components

| Component | Purpose |
|---|---|
| Arduino UNO | Main microcontroller for sensor acquisition and processing |
| MQ137 ammonia sensor | Detects ammonia in the collected breath sample |
| OPT101 photodetector | Detects transmitted optical intensity and converts it into an electrical signal |
| Red LED | Provides red-wavelength illumination for optical measurement |
| Infrared LED | Provides infrared illumination for optical measurement |
| LCD display | Displays the processed measurements |
| Finger probe | Holds the finger in position for optical measurement |
| Breath collection bag | Collects exhaled air for ammonia sensing |
| Mouthpiece and tubing | Directs the breath sample into the collection setup |
| One-way valve | Helps control the direction of airflow |
| Connecting wires and supporting circuitry | Provide electrical connections between system components |
<img width="810" height="568" alt="image" src="https://github.com/user-attachments/assets/cb7b69df-0936-4465-b091-60d4e673d1f2" />

## Working Principle

### 1. Breath Ammonia Measurement Using MQ137

The MQ137 is a gas sensor sensitive to ammonia (NH₃). Its electrical characteristics change in response to the concentration of ammonia in the surrounding gas.
<img width="678" height="411" alt="image" src="https://github.com/user-attachments/assets/338de51e-164a-4ed4-8079-b531e3b78489" />

**Working steps:**

1. Exhaled air is collected using the breath collection arrangement.
2. The collected sample is exposed to the MQ137 sensor.
3. The sensor produces an electrical output related to the gas concentration.
4. The Arduino reads the analog output through an analog input.
5. The software processes the sensor reading to estimate ammonia concentration in parts per million (ppm).
6. The calculated value is displayed on the LCD.

The project report discusses a breath ammonia range of approximately 0.3–1.2 ppm as a reference range in its design discussion. This should not be treated as a universal clinical threshold because breath measurements can vary with sampling conditions, calibration, and individual factors.

### 2. Optical Hemoglobin Estimation Using OPT101

The optical subsystem investigates estimating hemoglobin concentration by measuring light transmitted through a finger.

Hemoglobin absorbs light differently at different wavelengths. The project uses red and infrared illumination to investigate the relationship between transmitted light and hemoglobin-related optical properties.
<img width="690" height="431" alt="image" src="https://github.com/user-attachments/assets/63f41adf-1be0-4beb-bb92-5acab549f1c5" />
<img width="726" height="466" alt="image" src="https://github.com/user-attachments/assets/99149d28-e537-4dc3-bd2e-42ddc0d31032" />
<img width="700" height="502" alt="image" src="https://github.com/user-attachments/assets/dbb09bdc-c0cd-4fd7-8b91-73a5659de472" />

**Working steps:**

1. The finger is placed inside the optical probe.
2. Red and infrared LEDs illuminate the finger under microcontroller control.
3. Light passes through the finger tissue.
4. The OPT101 detects the transmitted light.
5. The photodetector converts the detected optical intensity into an electrical voltage.
6. The Arduino reads the voltage and processes it using the implemented calculation method.
7. The estimated hemoglobin value is displayed on the LCD.

The report discusses comparison with reference hemoglobin ranges. However, optical transmission alone does not establish an accurate hemoglobin measurement without appropriate calibration and validation against a reference method.

## Hardware Interfacing

The following connections are described in the project report. Verify the final circuit against the actual hardware and firmware before reproducing it.

### MQ137 to Arduino UNO

| MQ137 connection | Arduino UNO connection |
|---|---|
| VCC | 5V |
| GND | GND |
| Analog output (AO) | A0 |
| Digital output (DO) | Optional digital input, if used |

The analog output is used to obtain sensor readings for ammonia estimation. Converting the raw output into ppm requires a suitable calibration procedure.

### OPT101 to Arduino UNO

The optical sensor module provides an analog voltage corresponding to detected light intensity.

| OPT101 connection/function | Connection described in report |
|---|---|
| Supply voltage | 5V |
| Ground | GND |
| Output | Arduino analog input |
| Feedback connection | As specified by the sensor/module circuit |

The report describes the output and feedback connections using the analog input A2 and a 1 MΩ feedback resistor. Check the specific OPT101 module pinout and circuit before wiring, since module designs can differ.

### LED Control

The red and infrared LEDs are controlled by the Arduino so that illumination can be applied in sequence. The report discusses wavelengths around 660 nm for red light and 940 nm for infrared light; the hardware description also references slightly different nominal wavelengths in places.

Use the actual LED specifications when documenting or reproducing the circuit.

### LCD Display

The LCD is connected to the Arduino to display the processed sensor measurements. The exact pin assignments depend on the circuit used in the project.

## Software Implementation

The embedded software is developed using the Arduino IDE.

The main software responsibilities are:

- Initialize the microcontroller pins and peripherals.
- Read the analog output from the MQ137 sensor.
- Process gas sensor readings into an ammonia concentration estimate.
- Control the red and infrared LEDs in the optical measurement subsystem.
- Acquire the OPT101 photodetector output.
- Process the optical measurements using the implemented hemoglobin estimation algorithm.
- Display the resulting values on the LCD.

### General Processing Flow

1. Initialize the Arduino and connected peripherals.
2. Acquire the breath ammonia sensor reading.
3. Convert the sensor output using the implemented calibration method.
4. Control the optical LEDs and read the photodetector output.
5. Calculate the hemoglobin estimate using the implemented algorithm.
6. Display the measurement values.
7. Repeat the measurement cycle as defined by the firmware.

The exact calibration equations, filtering settings, and decision logic should be documented alongside the corresponding source code.

## Measurement Parameters

| Parameter | Sensor or method | Output |
|---|---|---|
| Breath ammonia | MQ137 gas sensor | Estimated ammonia concentration in ppm |
| Transmitted light intensity | OPT101 photodetector | Analog voltage or ADC reading |
| Hemoglobin | Optical estimation algorithm | Estimated concentration in g/dL |
| Display output | LCD | Readable measurement values |

## Results and Observations

The project report includes separate experimental sections for the MQ137 breath ammonia subsystem and the OPT101 optical subsystem.

The intended outputs are:

- Ammonia concentration estimates from the collected breath sample.
- Photodetector readings corresponding to transmitted light through the finger.
- Hemoglobin estimates generated by the implemented optical algorithm.
- Measurement values displayed through the LCD interface.

The reliability of these outputs depends on sensor calibration, sample handling, ambient conditions, optical alignment, signal quality, and the accuracy of the conversion algorithms.

For a reproducible evaluation, record the raw sensor readings, converted values, reference measurements, and measurement conditions. The project should not be described as clinically validated unless supported by appropriate validation data.

## Applications

Potential research and educational applications include:

- Biomedical instrumentation prototyping.
- Embedded sensor acquisition and signal processing.
- Breath-based biomarker research.
- Optical sensing and photodetector interfacing.
- Low-cost health-monitoring system development.
- Learning applications involving Arduino and biomedical sensors.

## Limitations

- The MQ137 response can be influenced by calibration, humidity, temperature, and other environmental or gas-related factors.
- Reliable ammonia concentration estimation requires a documented calibration procedure.
- Optical hemoglobin estimation requires validation against an appropriate reference method.
- Finger movement, probe alignment, ambient light, and differences in tissue properties can affect optical measurements.
- Breath ammonia and hemoglobin are indirect indicators and are not sufficient to diagnose CKD.
- CKD diagnosis and staging require appropriate clinical assessment and validated tests.
- The prototype should not be used to make medical decisions.

## Future Improvements

- Develop a repeatable calibration process for the MQ137 sensor using known ammonia concentrations.
- Investigate temperature and humidity compensation for gas measurements.
- Improve breath sample collection and control the measurement conditions.
- Improve optical probe design to reduce movement and ambient-light interference.
- Validate hemoglobin estimates against laboratory reference measurements.
- Add signal filtering and repeat-measurement averaging.
- Log measurement data for later analysis.
- Integrate wireless communication for transferring readings to a computer or mobile application.
- Conduct a larger validation study before considering clinical use.

## Technologies Used

**Embedded Systems**
- Arduino UNO
- Arduino IDE
- Embedded C/C++

**Biomedical Instrumentation**
- MQ137 ammonia gas sensor
- OPT101 photodetector
- Red and infrared LEDs
- Optical transmission measurement

**Hardware Integration**
- Analog sensor interfacing
- LED control
- LCD interfacing
- Sensor signal acquisition

## Project Structure

A suggested repository organization is shown below. Adjust the filenames to match the files actually included in your repository.

```text
Non-Invasive-CKD-Detection/
├── README.md
├── code/
│   └── ckd_detection.ino
├── circuit/
│   └── circuit_diagram.png
├── images/
│   ├── prototype.jpg
│   └── system_block_diagram.png
└── docs/
    └── project_report.pdf
```

## Disclaimer

This project is an academic prototype developed for educational and research purposes. It is **not a clinically validated diagnostic device**. Its measurements must not be used to diagnose CKD, determine CKD stage, or replace laboratory investigations and professional medical assessment.

## Project Information

- **Project Title:** Non-Invasive Detection of Chronic Kidney Disease
- **Domain:** Biomedical Engineering and Embedded Systems
- **Controller:** Arduino UNO
- **Primary Sensors:** MQ137 and OPT101
- **Project Type:** Academic Mini Project
