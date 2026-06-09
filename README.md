# flora-farms-deliverable-1
ICS 4111: Embedded Systems & IoT
Semester Project: Deliverable 1
Project: Flora Farms Remote Greenhouse Monitoring System
Assigned Flower: Daisy 
1. Project Overview
Flora Farms is a flower farm located in Naivasha, Kenya. The farm owner, Sheila, wants to remotely monitor conditions inside her greenhouses from her office in Nairobi, without having to be physically present at the farm. To solve this problem, our team is building an IoT (Internet of Things) monitoring system. This system uses small electronic devices equipped with sensors that measure key environmental conditions inside the greenhouses, such as temperature, humidity, and gas levels. The data collected by these sensors is then sent to the cloud so that Sheila can check it from anywhere at any time.
Our group has been assigned daisies as our flower type. Daisies have specific environmental requirements for healthy growth, and our IoT system is designed to monitor whether those conditions are being maintained inside the greenhouse.
2. Project Context: Flora Farms Setup
Parameter	Details
Location	Naivasha, Kenya (greenhouses) / Nairobi (farm office)
Power	200W solar panels with a 12V 100Ah battery per greenhouse
Irrigation	Stream sourced from a local river
Heating	LPG (Liquified Petroleum Gas) systems installed in each greenhouse
Connectivity	WiFi via routers installed in each greenhouse
Flower Groups	Roses, Daisies, Sunflowers, Carnations, Tulips (one assigned per group)


3. Flower Research
Assigned Flower: Daisy (Bellis perennis / Leucanthemum species)
Daisies are among the most cultivated flowers in greenhouse environments. They are relatively hardy but still require specific conditions to produce healthy, vibrant blooms. The following research outlines the optimal growing conditions for daisies that our monitoring system needs to track and maintain.
3.1 Environmental Requirements Table
Parameter	Optimal Range or Value	Notes
Temperature	15°C to 22°C (daytime)	Night temperatures can drop to 10°C without damaging the plant. Temperatures above 27°C can cause wilting and reduce bloom quality.
Relative Humidity	50% to 70%	Humidity above 80% increases the risk of fungal diseases like powdery mildew. Low humidity below 40% causes leaf stress and reduces flowering.
Soil Type	Well-draining loamy soil	Daisies do not tolerate waterlogged conditions. A mix of loam and organic compost is ideal for healthy root development.
Soil Moisture	40% to 60% volumetric water content	Soil should be consistently moist but never soggy. Daisies are moderately drought-tolerant but perform best with regular watering.
Soil pH	6.0 to 7.0 (slightly acidic to neutral)	A pH outside this range affects nutrient uptake. Iron and manganese deficiencies are common if the pH goes above 7.5.
Sunlight Exposure	6 to 8 hours of direct or bright indirect light per day	In a greenhouse setting, grow lights can supplement natural light during cloudy seasons. Insufficient light leads to leggy stems and reduced blooming.

3.2 Summary
Based on the research above, the primary environmental parameters our IoT system must monitor for the daisy greenhouse are temperature (targeting 15 to 22 degrees Celsius), relative humidity (targeting 50 to 70 percent), and LPG gas levels (to detect any leaks from the heating system). The DHT22 sensor handles both temperature and humidity readings, while the MQ-5 sensor monitors LPG gas presence. This matches the hardware assigned to our project.
4. Hardware Components
4.1 Introduction
To monitor environmental conditions inside the daisy greenhouse, the IoT monitoring system requires a combination of sensors, processing units, display devices, communication modules, and supporting electronic components. These components work together to collect data, process it, display information locally, and transmit readings to the cloud for remote monitoring by the farm owner.
The hardware components were chosen based on their suitability for greenhouse monitoring, low power consumption, compatibility with the ESP32S microcontroller, and ease of integration within an IoT environment.
4.2 Hardware Components List
Component	Description	Purpose
ESP32S DevKit WiFi + BLE Module (30 Pin)	A powerful microcontroller with built-in WiFi and Bluetooth capabilities.	Acts as the main controller. Collects sensor data, processes readings, displays information, and transmits data to the cloud via WiFi.
DHT22 (AM2302) Temperature & Humidity Sensor	A digital sensor measuring temperature and relative humidity with high accuracy.	Monitors environmental conditions required for healthy daisy growth. Provides real-time temperature and humidity readings.
MQ-5 LPG/Natural Gas Sensor	A gas detection sensor designed to detect LPG, natural gas, and other combustible gases.	Detects LPG leaks from greenhouse heating systems, improving safety and preventing potential hazards.
1.3" OLED LCD Display (128x64 I2C)	A compact display module communicating using the I2C protocol.	Displays temperature, humidity, gas concentration, and system status locally within the greenhouse.
5V Single Channel Relay Module	An electrically operated switch controlled by a microcontroller.	Used in advanced circuit architectures to isolate or switch communication between devices.
Breadboard	A reusable prototyping board allowing circuits to be assembled without soldering.	Used for testing and developing the IoT monitoring system before creating a permanent circuit.
Jumper Wires	Flexible wires for making temporary electrical connections between components.	Connect sensors, displays, and microcontrollers during prototyping.
Power Supply (12V Battery + Solar)	Renewable energy system consists of a solar panel and rechargeable battery.	Provides continuous power to the monitoring system within the greenhouse environment.
Resistors	Passive electronic components that limit current flow and provide voltage control.	Used for pull-up resistors, voltage dividers, and sensor interface protection.
Capacitors	Passive components for energy storage and filtering.	Used for power stabilization, noise reduction, and improving circuit reliability.

4.3 Component Functions
ESP32S DevKit WiFi + BLE Module
The ESP32S serves as the brain of the monitoring system. It receives data from the sensors, processes the information, displays readings on the OLED screen, and transmits data through WiFi to cloud-based monitoring services. Its built-in wireless connectivity makes it ideal for IoT applications. The 30-pin form factor is breadboard-compatible, enabling straightforward prototyping without modification.
DHT22 Temperature and Humidity Sensor
The DHT22 sensor continuously measures temperature and relative humidity inside the greenhouse. Since daisies grow best between 15°C and 22°C and 50% to 70% relative humidity, this sensor provides critical environmental data needed for maintaining optimal growing conditions. It communicates via a single-wire digital protocol and requires a 10kΩ pull-up resistor on the data line.

MQ-5 LPG Gas Sensor
The greenhouse uses LPG heating systems, creating a potential risk of gas leakage. The MQ-5 sensor detects LPG and other combustible gases using a tin dioxide (SnO2) sensing layer, whose conductivity increases with gas concentration. This allows the system to issue alerts when dangerous gas concentrations are detected. The sensor outputs an analog voltage that the ESP32S ADC reads and interprets. A warm-up period of approximately 20 seconds is required before readings stabilize.
1.3" OLED LCD Display
The OLED display provides immediate visual feedback to greenhouse workers. Temperature, humidity, gas levels, and system status can be viewed without needing to access the cloud dashboard. The I2C interface means only two data lines (SDA and SCL) are required, conserving GPIO pins on the ESP32S.
5V Single Channel Relay Module
The relay module acts as an electrically controlled switch. In the more advanced circuit architectures (Designs B and C), it allows one ESP32S board to activate, isolate, or signal another subsystem. The low-level trigger design means the relay is activated when the signal line is pulled LOW, the default-safe configuration suitable for GPIO control.
Breadboard and Jumper Wires
These components are used during the prototyping stage to connect devices and test circuit functionality before implementing a permanent design. The full-size 830-point breadboard supports simultaneous connections across all components.
Resistors and Capacitors
Resistors regulate electrical current and protect sensitive components. Key uses include 10kΩ pull-up resistor on the DHT22 data line (required for signal integrity) and voltage divider network for level-shifting between the 5V MQ-5 output and the 3.3V ESP32S ADC input. Capacitors stabilize voltage fluctuations and reduce electrical noise. A 100nF decoupling capacitor between VDD and GND near each sensor is recommended per component datasheets.
4.4 Summary
The proposed IoT monitoring system uses the ESP32S microcontroller as the central processing unit, together with the DHT22 temperature and humidity sensor, MQ-5 LPG gas sensor, OLED display, and relay module. Supporting components such as breadboards, jumper wires, resistors, and capacitors facilitate circuit construction and reliable operation. These hardware components provide an effective solution for monitoring environmental conditions and gas safety within the daisy greenhouse at Flora Farms.
5. Datasheets & Documentation
The following are the official datasheets and product documentation pages for the five components specified in the project brief. These serve as the primary technical references for schematic design, pin assignments, electrical characteristics, and programming considerations.
5.1 1.3" White IIC 128x64 OLED LCD (SH1106 Driver)
The 1.3-inch OLED module uses the SH1106 driver IC and communicates over I2C. It operates on 3.3V–5V, features 128x64 pixel resolution, and has a wide viewing angle (>160°). It draws approximately 29mA when fully on at 3.3V, making it suitable for low-power deployments.
Reference	Link
SH1106 OLED Module Datasheet (Waveshare PDF)	waveshare.com - 1.3inch-SH1106-OLED.pdf

SH1106 Driver IC Datasheet	lcd-module.de - SH1106_2014-03-11.pdf

Waveshare Product & Resource Page	waveshare.com/wiki/1.3inch_OLED_(B)


Key specs: Driver IC: SH1106, Interface: I2C / SPI, Resolution: 128x64 px, Supply: 3.3V-5V, Temp: -30°C to 70°C, I2C Address: 0x3C
5.2 ESP32S DevKIT WiFi + BLE Module (30 Pin)
The ESP32S DevKit is built around the ESP32-WROOM-32 module by Espressif Systems. It integrates a dual-core Xtensa LX6 processor, 2.4 GHz WiFi (802.11 b/g/n), Bluetooth 4.2 (BR/EDR + BLE), and 34 programmable GPIO pins. The 30-pin variant is breadboard-compatible for prototyping.
Reference	Link
ESP32-WROOM-32D Official Datasheet (Espressif)	espressif.com - esp32-wroom-32d_datasheet_en.pdf

ESP32 Series Chip Datasheet (Espressif)	espressif.com esp32_datasheet_en.pdf

ESP32-DevKitC Official Documentation	docs.espressif.com - esp32-devkitc


Key specs: CPU: Dual-core Xtensa LX6 @ 240 MHz, Flash: 4 MB, WiFi: 802.11 b/g/n, BLE 4.2, GPIO: 25 exposed, ADC: 12-bit, Temp: -40°C to 85°C
5.3 DHT22 AM2302 Temperature and Humidity Sensor
DHT22 (also known as AM2302) is a calibrated digital sensor from Aosong Electronics. It uses a capacitive humidity sensing element and a thermistor, outputting 40-bit serial data over a single data wire. A 10kΩ pull-up resistor is required on the data line, and readings can only be requested once every 2 seconds.
Reference	Link
AM2302 / DHT22 Official Datasheet (Adafruit CDN - Aosong)	cdn-shop.adafruit.com - AM2302.pdf

DHT22 Datasheet (SparkFun CDN)	cdn.sparkfun.com - DHT22.pdf


Key specs: Temp: -40°C to +80°C (±0.5°C), Humidity: 0–100% RH (±2–5%), Supply: 3.3V–5V, Interface: Single-wire digital, Sampling: ≥2 seconds, Pull-up: 10kΩ
5.4 MQ-5 LPG, Natural Gas, Coal Gas Sensor
The MQ-5 is a Winsen Electronics combustible gas sensor using a tin dioxide (SnO2) sensing layer. Its electrical resistance changes in proportion to the concentration of target gases. The sensor requires a warm-up/preheat period of approximately 20 seconds before readings stabilize.


Reference	Link
MQ-5 Datasheet - Winsen Electronics (Manufacturer)	winsen-sensor.com - MQ-5.pdf

MQ-5 Datasheet - Seeed Studio / Hanwei	files.seeedstudio.com - MQ-5.pdf


Key specs: Target gases: LPG, methane, propane, butane, town gas, Supply: 5V DC, Output: Analog, Heater: 31Ω ± 3Ω, Preheat: ≥20 s, Temp: -10°C to 50°C
5.5 5V 1-Channel Low Level Trigger Relay Module
This module provides optocoupler-isolated relay switching. It is triggered by a LOW logic signal (0–1.5V) on the IN pin, making it compatible with the ESP32S GPIO outputs. The onboard SPDT relay can switch loads up to 10A at 250V AC, and LEDs indicate power and relay status.
Reference	Link
1-Channel 5V Low-Level Trigger Relay Module Datasheet (HandsOnTec)	handsontec.com - 1Ch-relay.pdf

Relay Module Technical Specification (Rajguru Electronics)	rajguruelectronics.com - relay_board.pdf


Key specs: Supply: 5V DC, Trigger: LOW (0–1.5V), Trigger current: 5 mA, Max load: 10A @ 250V AC, Isolation: Optocoupler, Contacts: SPDT (COM, NO, NC)
Datasheet Summary
	Component	Primary Datasheet / Documentation
1	1.3" IIC 128x64 OLED LCD (SH1106)	Waveshare SH1106 OLED Datasheet PDF

2	ESP32S DevKIT WiFi + BLE (30 Pin)	Espressif ESP32-WROOM-32D Datasheet PDF

3	DHT22 AM2302 Temp & Humidity Sensor	AM2302 Datasheet PDF (Adafruit / Aosong)

4	MQ-5 LPG / Natural Gas Sensor	MQ-5 Datasheet PDF (Winsen Electronics)

5	5V 1-Channel Low Level Trigger Relay	1-Channel Relay Module Datasheet PDF (HandsOnTec)





















6. Circuit Diagrams
6.1 CIRCUIT DIAGRAM A
Architecture A: Single ESP32S Monitoring System
This architecture uses a single ESP32S microcontroller to interface with the DHT22 temperature and humidity sensor, MQ-5 LPG gas sensor, and OLED display. The ESP32S collects environmental data from the sensors, processes the readings, and displays real-time information on the OLED screen. A pull-up resistor is included for the DHT22 data line, while a decoupling capacitor improves power stability and noise filtering.
 


6.2 CIRCUIT DIAGRAM B
Architecture B: Dual ESP32S Direct Communication System
This architecture consists of two ESP32S microcontrollers connected directly to each other. The first ESP32S interfaces with the MQ-5 gas sensor, while the second ESP32S interfaces with the DHT22 temperature and humidity sensor. The two microcontrollers communicate through direct serial connections, allowing environmental data collected by one subsystem to be shared with the other. This design demonstrates distributed sensing using multiple embedded devices.
 


















6.3 CIRCUIT DIAGRAM C
Architecture C: Relay-Based Dual ESP32S System
This architecture incorporates two ESP32S microcontrollers connected through a relay-controlled interface. One ESP32S is connected to the DHT22 sensor while the second ESP32S is connected to the MQ-5 gas sensor. The relay module provides electrical isolation and controlled switching between the two subsystems. Additional components such as resistors, capacitors, a transistor driver, and a flyback diode are included to ensure reliable relay operation and circuit protection.
 








 EVIDENCE OF GROUP WORK
Virtual team meeting held during the planning and development of Deliverable 1, including discussion of hardware selection, datasheet review, and circuit schematic design.

 
