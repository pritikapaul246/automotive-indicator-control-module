# automotive-indicator-control-module
# Automotive Indicator Control Module (Embedded ECU Simulation)

This project implements an automotive-style Indicator Control Module using an ESP8266 microcontroller with a cooperative time-triggered scheduler architecture. The system simulates real vehicle turn indicator and hazard light control logic similar to a Body Control Module (BCM).

## Features

- Left indicator toggle (1-second hold)
- Right indicator toggle (1-second hold)
- Hazard mode activation (dual-button hold)
- Hazard mode exit arbitration
- Mutual exclusion between indicators
- Deterministic scheduler-based firmware
- Non-blocking execution using millis()
- UART debug logging support

## Hardware Components

| Component | Quantity |
|----------|----------|
| ESP8266 NodeMCU | 1 |
| Push buttons | 2 |
| LEDs | 2 |
| 220Ω resistors | 2 |
| Breadboard | 1 |

## Hardware Setup

Below is the experimental setup of the Indicator Control Module using ESP8266 NodeMCU, push-button module, and indicator LEDs.

![Hardware Setup](images/hardware_setup.jpg)

---

## Pin Configuration

| Signal | GPIO |
|-------|------|
| Left Button | D1 |
| Right Button | D2 |
| Left Indicator LED | D5 |
| Right Indicator LED | D6 |

---

## Firmware Architecture

The system follows a cooperative time-triggered scheduler similar to automotive Body Control Module firmware.

Two periodic software tasks are implemented:

| Task | Period | Function |
|------|--------|----------|
| Task_100ms | 100 ms | Button sampling and state-machine transitions |
| Task_300ms | 300 ms | Indicator LED blinking control |

This ensures deterministic execution without blocking delays.

---

## State Machine Design

The indicator control logic is implemented as a finite state machine with four operating modes:

- IDLE
- LEFT_INDICATOR_ACTIVE
- RIGHT_INDICATOR_ACTIVE
- HAZARD_MODE_ACTIVE

Transitions occur based on long-press button detection and hazard arbitration logic.

---

## Hazard Arbitration Logic

Hazard mode has priority over individual indicators.

If both buttons are pressed for 1 second:

- hazard mode activates
- individual indicators deactivate

Pressing either button during hazard mode exits hazard mode.

---

## Scheduler Implementation

Instead of using blocking delay() calls, periodic execution is implemented using millis():

```cpp
if(currentTime - last100msTick >= 100)
