# Smart EV Cable Tamper Detection System

## Overview
The Smart EV Cable Tamper Detection System is an IoT-based embedded security solution designed to monitor EV charging cables for tampering and wire-cut events in real time. The system uses dual-loop detection logic to classify intrusion stages and automatically isolates power during abnormal conditions.

The project integrates ESP32, INA219 current sensing, relay-based protection, cloud monitoring, and LCD-based real-time status visualization.

---

## Features

- Real-time cable tamper detection
- Multi-layer intrusion classification
- Automatic motor/power cutoff using relay
- Current and voltage monitoring using INA219
- WiFi-enabled cloud monitoring with ThingSpeak
- LCD display for live system status
- Buzzer-based alert mechanism
- Low-cost and scalable architecture

---

## Intrusion Classification Logic

| Loop 1 | Loop 2 | Condition |
|--------|--------|-----------|
| LOW | LOW | NORMAL |
| HIGH | LOW | LAYER TAMPER |
| LOW | HIGH | WIRE CUT |
| HIGH | HIGH | SEVERE CUT |

---

## Components Used

- ESP32
- INA219 Current Sensor
- 16x2 I2C LCD Display
- 5V Relay Module
- 5V DC Motor
- Buzzer
- Jumper Wires
- Breadboard
- Lithium Battery / 5V Supply

---

## System Architecture

```text
Battery (+)
   ↓
INA219 VIN+
   ↓
INA219 VIN-
   ↓
Relay COM
   ↓
Relay NO
   ↓
Motor (+)
   ↓
Motor (-)
   ↓
Battery (-)
```

ESP32 handles:
- Loop wire monitoring
- Relay control
- LCD updates
- WiFi communication
- ThingSpeak cloud upload

---

## Connections

### Relay Module
| Relay Pin | ESP32 |
|-----------|-------|
| S | GPIO 33 |
| + | 5V |
| - | GND |

### INA219
| INA219 Pin | ESP32 |
|------------|-------|
| VCC | 5V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

### LCD I2C
| LCD Pin | ESP32 |
|----------|-------|
| VCC | 5V |
| GND | GND |
| SDA | GPIO 21 |
| SCL | GPIO 22 |

### Buzzer
| Buzzer | ESP32 |
|---------|-------|
| + | GPIO 26 |
| - | GND |

### Loop Wires
| Loop | ESP32 |
|------|-------|
| Loop 1 | GPIO 14 |
| Loop 2 | GPIO 27 |

---

## Working Principle

1. ESP32 continuously monitors Loop 1 and Loop 2 using INPUT_PULLUP logic.
2. The system classifies the cable condition based on loop continuity.
3. During normal operation, the relay keeps the motor active.
4. If tampering or wire cuts are detected:
   - Relay disconnects motor power
   - Buzzer alert activates
   - LCD updates system state
5. INA219 measures live current and voltage values.
6. Electrical parameters are uploaded to ThingSpeak using WiFi.

---

## Cloud Monitoring

The system uploads:
- Voltage data
- Current data
- System operating conditions

to the ThingSpeak IoT cloud platform for remote monitoring and visualization.

---

## Applications

- EV Charging Stations
- Smart Grid Protection
- Industrial Cable Monitoring
- Critical Infrastructure Security
- Defense Cable Protection Systems

---

## Future Enhancements

- Mobile notification alerts
- AI-based anomaly detection
- GPS tracking integration
- Cloud analytics dashboard
- Battery backup optimization

---

## Technologies Used

- Embedded C
- ESP32
- Arduino IDE
- WiFi Communication
- ThingSpeak IoT
- I2C Communication Protocol

---

## Author

Prasannaa K

---
