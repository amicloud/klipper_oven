# Klipper Oven Macro

A custom G-code macro for Klipper that allows you to use your 3D printer's heated bed as a makeshift oven. Perfect for curing silicone parts or any application requiring controlled heating over a period of time.

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
  - [Starting the Oven](#starting-the-oven)
  - [Canceling the Oven](#canceling-the-oven)
- [Parameters](#parameters)
- [Examples](#examples)
- [Recommendations](#recommendations)
- [Safety Precautions](#safety-precautions)
- [License](#license)

---

## Features

- **Customizable Temperature and Time:** Set your desired temperature (°C) and duration (minutes).
- **Adjustable Check Interval:** Define how frequently the macro checks the remaining time during the holding phase.
- **Non-Blocking Operation:** The macro remains responsive and can be canceled at any time.
- **Prevents Heater Idle Timeout:** Reissues the heater command periodically to prevent the heater from turning off automatically.
- **User Feedback:** Provides real-time updates via `M117` messages and console responses.
- **Safety-Oriented:** Designed to prevent conflicts and ensure safe operation.

---

## Installation


### Fast One-Liner 
#### This will download the .cfg to the default Klipper config directory, add the [include] line to your printer.cfg, and restart Klipper.
1. ```curl https://raw.githubusercontent.com/amicloud/klipper_oven/main/oven.cfg -o ~/printer_data/config/oven.cfg && sed -i '2i\[include oven.cfg]' ~/printer_data/config/printer.cfg && systemctl restart klipper```

### Manual Installation
  1. **Download the `oven.cfg` File:**
  
     - Download the [`oven.cfg`](oven.cfg) file from this repository.
  
  2. **Include `oven.cfg` in Your Configuration:**
  
     - Add the following line to your `printer.cfg` file:
  
       ```
       [include oven.cfg]
       ```
  
     - Ensure that `oven.cfg` is placed in the same directory as your `printer.cfg` file. If it's in a different directory, adjust the path accordingly.
  

3. **Save and Restart Klipper:**

   - Save the `printer.cfg` file and restart Klipper to apply the changes.
     - You can restart Klipper by issuing the `RESTART` command in your terminal or through your printer's interface.

---

## Usage

### Starting the Oven

Use the `OVEN` macro to start the oven operation.

**Syntax:**

OVEN [TIME=<minutes>] [TEMP=<degrees Celsius>] [CHECK_INTERVAL=<seconds>]

- **TIME:** Duration in minutes (default: `60` minutes).
- **TEMP:** Target temperature in degrees Celsius (default: `60°C`).
- **CHECK_INTERVAL:** Time between status checks in seconds during the holding phase (default: `60` seconds).

**Example:**

- Start the oven at default settings (60°C for 60 minutes):

OVEN

- Start the oven at 70°C for 90 minutes, checking every 30 seconds:

OVEN TIME=90 TEMP=70 CHECK_INTERVAL=30


### Canceling the Oven

Use the `CANCEL_OVEN` macro to cancel the oven operation at any time.

**Syntax:**

CANCEL_OVEN

---

## Parameters

- **TEMP (float):**

  Target temperature in degrees Celsius for the heated bed.

- **TIME (float):**

  Duration in minutes for which the bed should hold the target temperature.

- **CHECK_INTERVAL (float):**

  Time in seconds between each status check during the holding phase. Adjusting this can balance between processor load and update frequency.

---

## Examples

1. **Default Operation:**

  Start the oven at 60°C for 60 minutes, checking every 60 seconds.
  OVEN

2. **Custom Temperature and Time:**

  Start the oven at 65°C for 120 minutes.
  OVEN TEMP=65 TIME=120

3. **Custom Check Interval:**

  Start the oven at 55°C for 45 minutes, checking every 15 seconds.
  OVEN TEMP=55 TIME=45 CHECK_INTERVAL=15

4. **Cancel the Oven Operation:**
   CANCEL_OVEN


---

## Recommendations

- **Use a Heat-Resistant Cover:**

To improve heat retention and even distribution, it's recommended to place a heat-resistant cover over your build plate. Materials like **ASA** (Acrylonitrile Styrene Acrylate) are suitable for this purpose due to their thermal stability.

- **Example Setup:**

 - Use an FDM-printed ASA lid to cover the build plate.
 - Keep the printer in an enclosure to maintain consistent ambient temperatures.

- **Benefits:**

 - Enhances heat retention, leading to more efficient curing.
 - Provides a controlled environment, reducing temperature fluctuations.

- **Ensure Material Compatibility:**

- Verify that all materials used (molds, platters, covers, etc.) can safely withstand the target temperatures.
- Avoid materials that may deform, melt, or release harmful fumes at your operating temperatures.

- **Avoid Obstructing Sensors:**

- Ensure that the cover does not block any airflow or thermal runaway sensors.
- Proper sensor operation is crucial for safety mechanisms.

---

## Safety Precautions

- **Supervision Required:**

Always monitor your printer while it's operating as an oven to prevent any hazards.

- **Fire Safety:**

Keep a fire extinguisher nearby and ensure smoke detectors are operational.

- **Ventilation:**

Operate in a well-ventilated area if curing materials that may emit fumes.

- **Temperature Limits:**

Do not exceed the maximum safe operating temperatures for your printer's components.

- **Heater Stability:**

The macro periodically reissues the heater command to prevent the heater from turning off due to idle timeout. Ensure this aligns with your printer's safety protocols.

---

## License

This project is licensed under the MIT License.










