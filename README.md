# Smart Thermostat Prototype

## Overview

This project is a smart thermostat prototype built on a Raspberry Pi. It demonstrates how an embedded system can read sensor data, respond to user input, control outputs, and communicate system status.

The thermostat reads the current room temperature, compares it to a user-defined set point, and determines whether heating or cooling is needed. It then displays this information and sends updates through serial communication.

---

## Features

* **Three Operating Modes**

  * OFF
  * HEAT
  * COOL

* **Temperature Control**

  * Default set point: 72°F
  * Increase set point with button
  * Decrease set point with button

* **Sensor Input**

  * Reads temperature using AHT20 sensor via I2C

* **Visual Output (LEDs)**

  * Red LED = Heating
  * Blue LED = Cooling
  * Fading = system actively heating/cooling
  * Solid = target temperature reached

* **LCD Display**

  * Line 1: Current date and time
  * Line 2: Alternates between:

    * Current temperature
    * Current mode and set point

* **UART Communication**

  * Sends system status every 30 seconds
  * Format:

    ```
    state,current_temperature,set_point
    ```

---

## Hardware Used

* Raspberry Pi
* AHT20 Temperature Sensor (I2C)
* 16x2 LCD Display
* 3 Push Buttons
* Red LED (heating indicator)
* Blue LED (cooling indicator)
* Breadboard and wiring

---

## How It Works

1. The system continuously reads the current temperature from the sensor.
2. The user selects a mode using the mode button:

   * OFF → HEAT → COOL → OFF
3. The system compares the current temperature to the set point:

   * In HEAT mode:

     * If temperature is below set point → heating (red LED fades)
     * Otherwise → red LED stays solid
   * In COOL mode:

     * If temperature is above set point → cooling (blue LED fades)
     * Otherwise → blue LED stays solid
4. The LCD updates with current system information.
5. Every 30 seconds, the system sends a status update over UART.

---

## Controls

* **Green Button** → Change mode (OFF / HEAT / COOL)
* **Red Button** → Increase set point (+1°F)
* **Blue Button** → Decrease set point (-1°F)

---

## File Structure

* `Thermostat.py`
  Main program that runs the thermostat system

* `ThermostatServer-Simulator.py`
  Simulates a server by receiving and displaying UART data

---

## How to Run

1. Connect all hardware components to the Raspberry Pi.
2. Open terminal on the Pi.
3. Navigate to the project folder:

   ```
   cd ~/your-project-folder
   ```
4. Run the thermostat:

   ```
   python3 Thermostat.py
   ```

(Optional) Run the server simulator in another terminal:

```
python3 ThermostatServer-Simulator.py
```

---

## Learning Objectives

This project demonstrates:

* GPIO (buttons and LEDs)
* I2C communication (temperature sensor)
* UART communication (data output)
* LCD interfacing
* State machine design
* Embedded systems programming

---

## Future Improvements

* Add Wi-Fi connectivity for cloud communication
* Store historical temperature data
* Add mobile or web interface
* Improve user interface and display

---

## Summary

This project shows how a basic embedded system can function as a thermostat by combining sensor input, user controls, system logic, and multiple output methods. It serves as a foundation for building a fully connected smart thermostat system.
