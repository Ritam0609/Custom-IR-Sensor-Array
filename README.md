# Custom-IR-Sensor-Array
Open-source custom infrared sensor array featuring custom PCB design, IR sensing circuitry, firmware, schematics, and hardware documentation.
# Custom-IR-Sensor-Array

A custom-designed infrared sensor array based on the **TCRT5000 reflective IR sensor**, developed for short-range object detection and proximity sensing.

<img width="500" height="400" alt="image" src="https://github.com/user-attachments/assets/c908cd8f-5c19-419d-84af-f16e7cfc7c10" />

Fig 1: Prototype of Custom IR Array Sensor
## Components Used

| Component | Value / Type | Purpose |
|---|---|---|
| TCRT5000 | Reflective IR Sensor | IR emission and reflected IR detection |
| Resistor | 220 Ω | IR LED current limiting |
| Resistor | 10 kΩ | Phototransistor pull-up |
| Capacitor | 100 nF | Noise filtering and supply decoupling |
| Microcontroller | ESP32 | Sensor signal processing |

---

## Why TCRT5000?

The **TCRT5000** was selected because it integrates an infrared emitter and phototransistor in a compact package, making it suitable for short-range reflective sensing and custom sensor-array applications.

### Key Features

- Integrated IR emitter and phototransistor
- Infrared wavelength: approximately **950 nm**
- Compact and low-cost
- Simple interface with microcontrollers
- Suitable for short-range reflective detection
- Easy to integrate into a custom PCB
- Suitable for multiple sensors arranged in an array

---

## Working Principle

The IR LED inside the TCRT5000 emits infrared light toward the target object. When an object is present within the sensing region, a portion of the emitted IR light is reflected back toward the phototransistor.

The reflected infrared light changes the phototransistor's conduction, producing a change in the output voltage. This voltage variation is then read and processed by the ESP32.

```text
        TCRT5000
      ┌─────────────┐
      │   IR LED    │ ───────► IR Light
      │             │              │
      │ Phototrans. │ ◄──── Reflected IR
      └──────┬──────┘
             │
             ▼
            ESP32
```

---

## Resistors

Two resistors are used in each TCRT5000 sensor channel.

### 220 Ω Resistor — IR LED Current Limiting

The **220 Ω resistor** is connected in series with the internal IR LED of the TCRT5000.

Its primary purpose is to limit the current flowing through the IR LED and protect it from excessive current.

The approximate LED current can be calculated using:

**I = (VCC - VF) / R**

For a 5 V supply and a typical IR LED forward voltage of approximately 1.2 V:

**I = (5 - 1.2) / 220**

**I ≈ 17.3 mA**

This provides a suitable operating current for the IR emitter.

### 10 kΩ Resistor — Phototransistor Pull-Up

The **10 kΩ resistor** is used as a pull-up resistor for the phototransistor output.

It converts the phototransistor's current variation into a voltage signal that can be read by the ESP32.

```text
        3.3V
         │
       10 kΩ
         │
         ├──────► ESP32 ADC
         │
   Phototransistor
         │
        GND
```

When the amount of reflected IR increases, the phototransistor conducts more current, causing the output voltage to change. The ESP32 measures this voltage variation to determine the presence or proximity of an object.

---

## Capacitor

A **100 nF ceramic capacitor** is used for noise suppression and supply decoupling.

It helps reduce high-frequency electrical noise and provides a more stable supply for the sensor circuitry.

The capacitor should preferably be placed close to the sensor or the corresponding supply connections on the PCB.

---

## Sensor Array

Multiple TCRT5000 sensors are arranged on a custom PCB to create the IR sensor array.

The number and spacing of sensors can be adjusted according to the required detection area and application.

```text
        IR SENSOR ARRAY

     ┌────┐  ┌────┐  ┌────┐  ┌────┐
     │ S1 │  │ S2 │  │ S3 │  │ S4 │
     └────┘  └────┘  └────┘  └────┘
        │       │       │       │
        └───────┴───────┴───────┘
                    │
                  ESP32
```

Each sensor provides an individual detection signal that can be processed by the microcontroller.

---

## Schematic 

<img width="800" height="304" alt="schematic" src="https://github.com/user-attachments/assets/5667c077-cd5a-4402-aabc-28192e992fbb" />

Fig 2: Schematic Design of the Custom Line Follower IR Array Sensor


## Working Distance

The effective sensing distance of the TCRT5000 depends on several factors:

- Target surface reflectivity
- Object color
- Sensor orientation
- Distance between the sensor and target
- Ambient lighting
- Sensor alignment
- PCB and sensor geometry

### Measured Working Distance

**Working distance:** `5 mm`

**Maximum reliable detection distance:** `7-8 mm`

> The final values should be replaced with the experimentally measured values from the completed sensor array.

---

## Testing and Results

The sensor array was tested at different distances to evaluate its object-detection capability.

<img width="700" height="400" alt="Sensor_Working" src="https://github.com/user-attachments/assets/8f76da0c-c3c9-48be-9ee6-a5c46dc04045" />

Fig 3: Sensors active under the voltage of 3.3 V to 5 V

<img width="427" height="310" alt="result" src="https://github.com/user-attachments/assets/2b75795b-fc08-490a-9051-fd7befa498f0" />

Fig 4: Sensor giving Result while detecting a white surface


| Distance | Detection Result |
|---:|---|
| 5 mm | Detected |
| 10 mm | Detected |
| 15 mm | Not Detected |
| 20 mm | Not Detected |
| 25 mm | Not Detected |
| 30 mm | Not Detected |
| 35 mm | Not Detected |

### Result

The custom IR sensor array successfully detects nearby objects using the reflected infrared signal from the TCRT5000 sensors.

The measured detection range depends on the physical properties of the target and the environmental conditions.

**Maximum reliable detection distance:** `5 - 6 mm`

---


The sensor positions can be customized according to the required detection geometry.

---

## Applications

The custom IR sensor array can be used for:

- Short-range object detection
- Proximity sensing
- Robotics
- Autonomous systems
- Obstacle detection
- Line and surface detection
- Custom embedded sensing applications

---

## Project Status

**Status:** Testing / Development

### Completed

- [x] TCRT5000 sensor selection
- [x] Sensor circuit design
- [x] Resistor selection
- [x] Custom PCB design
- [x] ESP32 interface
- [x] Initial sensor testing

### Ongoing

- [ ] Final distance calibration
- [ ] Full array testing
- [ ] Performance optimization
- [ ] Final documentation

---

## Repository Structure

```text
Custom-IR-Sensor-Array/
│
├── README.md
│
├── Hardware/
│   ├── Schematic/
│   ├── PCB/
│   ├── Gerber/
│   └── 3D_Model/
│
├── Firmware/
│   └── ESP32/
│
├── Datasheets/
│
├── Images/
│
└── Documentation/
    ├── Testing/
    └── Calibration/
```

---

## Author

**Ritam Das**

Custom IR Sensor Array  
Electronics & Embedded Systems Project

---

---

## Contact

For questions, collaboration, or technical discussion regarding this project:

**Ritam Das**  
B.Tech – Electronics & Communication Engineering  
University of Engineering and Management, Kolkata

📧 **Email:** dasritam0609@gmail.com   
💻 **GitHub:** [yourusername](https://github.com/yourusername)  
🔗 **LinkedIn:** [Ritam Das](https://www.linkedin.com/in/yourusername/)

---

## License

This project is intended for educational, research, and development purposes.
