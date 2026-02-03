# Ultrasonic Distance Sensor with `Arduino Uno R4 WiFi`

## Overview
This project reads distance measurements from an ultrasonic sensor (e.g. HC-SR04) using an `Arduino Uno R4 WiFi` board and PlatformIO. The measured distance is printed to the serial console at `9600` baud.

## Files
- `main.cpp` — application code: triggers the ultrasonic sensor, measures echo pulse, computes distance (cm) and writes results to Serial at 9600 baud.
- `platformio.ini` — build configuration (environment `uno_r4_wifi`, platform `renesas-ra`, framework `arduino`, `monitor_speed = 9600`).

## Hardware
- `Arduino Uno R4 WiFi`
- Ultrasonic sensor (e.g. HC-SR04)
- Jumper wires
- Optional: resistor divider or level shifter for the sensor echo pin if required by your board

Wiring (example):
- Ultrasonic VCC -> `5V` (or `3.3V` if using a 3.3V sensor)
- Ultrasonic GND -> `GND`
- Ultrasonic Trigger -> digital pin `D2`
- Ultrasonic Echo -> digital pin `D3` (use level shifting if needed)

Note: Verify the voltage and I/O tolerance of your sensor and board before connecting. If the board's I/O is not 5V tolerant, use a voltage divider or level shifter on the Echo line.

## Build & Upload (PlatformIO)
From the project root:
- Build: `pio run -e uno_r4_wifi`
- Upload: `pio run -e uno_r4_wifi -t upload`
- Open serial monitor: `pio device monitor -e uno_r4_wifi`  
  or `pio run -e uno_r4_wifi -t monitor`  
Serial monitor baud is set by `monitor_speed = 9600` in `platformio.ini`.

## Behavior (what `main.cpp` does)
- Sends a short trigger pulse to the ultrasonic sensor.
- Measures the duration of the echo pulse.
- Converts pulse duration to distance in centimeters using the speed of sound.
- Prints distance values to Serial every loop (baud `9600`).

## Troubleshooting
- No serial output: confirm correct COM/USB port and that `monitor_speed` matches the `Serial.begin()` baud rate in `main.cpp`.
- Incorrect distances: check wiring, sensor orientation, and whether an appropriate constant for the speed of sound is used in calculations.
- Floating or noisy readings: add averaging or filtering in code, ensure stable power to the sensor.

## License
MIT

## Author
Project by `Aditya Singh`
