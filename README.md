# Konnected Pro Ethernet Alarm Panel Configuration

This ESPHome configuration implements a local alarm system for the Konnected Pro Alarm Panel Pro (Ethernet) using Esphome. This config includes support for a Wiegand Hardwired Keypad to Arm/Disarm

## Overview

This alarm panel provides a configurable state machine-based security system with keypad control, zone monitoring, and Home Assistant integration.

## Features

### Alarm States
- **Disarmed**: System is inactive
- **Arming**: System is arming with countdown
- **Armed Away**: System is armed for away mode
- **Armed Home**: System is armed for home mode
- **Pending**: Motion detected while armed (triggers transition after timeout)
- **Triggered**: Alarm is active

### Keypad Controls
- **\*** key: Arms the system in Home mode
- **#** key: Arms the system in Away mode
- **4-digit PIN code**: Disarms the system (code required)
- Keypad includes LED indicator and beeper for user feedback

### Zone Monitoring
Supports up to 8 monitored zones (zones 5-12) for doors, windows, and motion sensors. When armed, zone triggers transition to pending state and then trigger alarm state.

### Configurable Settings
- **Arming Timeout**: Delay before system fully arms (default: 10 seconds)
- **Pending Timeout**: Delay after zone trigger before alarm activates (default: 60 seconds)
- **Trigger Timeout**: Duration alarm remains active (default: 5 minutes)

### Connectivity & Interface
- Ethernet connectivity (LAN8720)
- Built-in web server for local monitoring and control
- Home Assistant API integration
- Local PIN code validation

### Outputs
- Siren output (alarm1) can be triggered manually or automatically on alarm state
- Keypad LED and beeper outputs

## Hardware

- Konnected Pro Alarm Panel ESP32
- LAN8720 Ethernet interface
- Wiegand keypad
- Door/window/motion sensors on zones 5-12
- Optional siren output

## Configuration

Key settings are defined as substitutions at the top of the config file:
- `alarm_code`: Master PIN code(s) for disarming
- Zone names and GPIO assignments
- Timeout durations
- Device name and friendly name

## Home Assistant Integration

The system exposes:
- Alarm state sensor
- Arm/Disarm services
- Incorrect code counter
- Individual zone binary sensors
- LED and beeper controls
