<p align="center">
  <img src="assets/V2_mug_banner.png" alt="TempO banner" width="100%">
</p>

<p align="center">
  <img alt="Status" src="https://img.shields.io/badge/status-in%20development-orange">
  <img alt="Platform" src="https://img.shields.io/badge/platform-ESP32-blue">
  <img alt="Integration" src="https://img.shields.io/badge/integration-Home%20Assistant-41BDF5">
</p>

# TempO

**A homemade, open-source temperature, humidity and pressure station for Home Assistant, built on the ESP32.**

## Contents

- [Prelude](#prelude)
- [System requirements](#system-requirements)
- [Planned hardware and software](#planned-hardware-and-software)
- [Prototyping in the Wokwi simulator](#prototyping-in-the-wokwi-simulator)
- [Project status](#project-status)
- [Contributing](#contributing)

## Prelude

The name TempO comes from two very simple ideas: **Temp**erature and **O**pen-source. TempO is what it says it is, and it does not pretend to do anything else: it is a homemade temperature, humidity and pressure station for Home Assistant. How you deploy it or scale it is up to you.

The project was born from the need to learn the ESP32 platform and embedded systems. The best way I found to learn about them was to build something myself, from start to end, especially now that we all have the internet and AI on our side.

I run a small homelab at home and recently deployed Home Assistant, partly out of curiosity and partly to replace the SmartLife app I used to switch my server's outlet. From there, going further into home automation and developing a small environmental sensor from scratch felt like a natural next step.

In terms of technical difficulty, this project is roughly the equivalent of a high-school side project, and I am aware of that. Even so, it covers topics I had no previous idea about: programming in C++, dealing with I2C, handling analog and digital inputs, circuit design and CAD assembly.

I will try to provide all the materials and files needed to build this yourself, together with proper documentation, to the best of my abilities and availability.

> [!WARNING]
> **Disclaimer:** Given my limited prior experience in this field, some design and technical decisions were made with an AI-assisted workflow, which means parts of this project were done **with the help of AI**. If that conflicts with your views on LLM usage, please read no further.

## System requirements

The finished product has to comply with the following requirements:

1. **Reliable measurements.** The system must reliably gather temperature, humidity and pressure data and push those values to the Home Assistant server.
2. **Timekeeping.** The system must pull the date and time from the Home Assistant server every given number of hours and keep that value with an RTC, so the time stays valid if the connection to the server is lost.
3. **Secure connection.** The system must be able to establish, keep and recover a secure connection with the Home Assistant server, in such a way that it cannot be used as an entry point for malicious access to the LAN.
4. **Battery life.** The final unit must be rechargeable and hold its charge for at least 15 days, so keeping it running does not become a chore. Low-power components and code must be considered throughout the design.
5. **Home-buildable.** With the exception of the PCB and the electronic components on it, the product must be entirely manufacturable at home using basic DIY tools (soldering iron, 3D printer, screwdrivers, etc.).
6. **Simple integration.** Integration with Home Assistant must be as simple and intuitive as with any other ESP32-based device.

## Planned hardware and software

These are the current plans and may change as the project moves forward.

| Block | Choice | Notes |
| --- | --- | --- |
| Microcontroller | ESP32 | Wi-Fi and deep sleep support for battery operation |
| Sensor | BME280 (I2C) | Temperature, humidity and pressure in a single chip |
| Display | E-ink panel (SPI) | Refreshed periodically; keeps the image without power |
| Power | Rechargeable LiPo or Li-ion cell with a charging circuit | Whichever turns out cheaper and more stable for the purpose |
| Timekeeping | RTC (internal or external, to be decided) | Synchronised from Home Assistant |
| Firmware | ESPHome | Native Home Assistant integration |
| PCB design | KiCad | Simple two-layer board |
| Enclosure | CAD design, 3D printed | Printable at home |

## Prototyping in the Wokwi simulator

The first prototyping stage runs in the [Wokwi](https://wokwi.com) simulator, so the firmware logic can be developed before the physical ESP32 and sensors are available.

Wokwi does not include a BME280 model, so three other sensors stand in for it during simulation:

| Simulated sensor | Provides | Interface |
| --- | --- | --- |
| DS18B20 | Temperature | 1-Wire (with a 4.7 kΩ pull-up) |
| DHT22 | Temperature and humidity | Single-wire, own protocol |
| BMP180 | Temperature and pressure | I2C |

The physical build replaces all three with the BME280, which is also an I2C device.

## Project status

- [x] Requirements defined
- [x] Sensor reading simulated in Wokwi (DS18B20, DHT22, BMP180)
- [ ] Breadboard prototype with real hardware (ESP32 and BME280)
- [ ] ESPHome firmware and Home Assistant integration
- [ ] E-ink display
- [ ] Deep sleep and power optimisation (15-day target)
- [ ] Secure connection (encrypted API, network isolation)
- [ ] Schematic and PCB design in KiCad
- [ ] Enclosure design and 3D printing
- [ ] Assembly guide and final documentation

## Contributing

This project is a learning exercise, so corrections, suggestions and feedback are welcome. Feel free to open an issue.

<!-- TODO: add a license section once a license has been chosen. -->
