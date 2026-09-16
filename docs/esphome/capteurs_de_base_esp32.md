To expose the Wi-Fi signal strength (RSSI) as a sensor entity in Home Assistant, you need to explicitly add the wifi_signal component to your ESPHome YAML configuration file.
Here is the exact code snippet to add to your YAML file:

sensor:
  - platform: wifi_signal
    name: "WiFi Signal"
    update_interval: 60s

## Where to add this code

   1. Open your ESPHome Dashboard in Home Assistant.
   2. Click Edit on your device's card.
   3. Paste the snippet above into your YAML configuration. (If you already have a sensor: section, just add the - platform: wifi_signal block right beneath it, ensuring proper indentation).
   4. Click Save and then Install to flash the updated firmware to your device over-the-air (OTA).

## Optional: Expose Signal Strength as a Percentage
If you prefer to see the Wi-Fi health as a percentage (0% to 100%) instead of a negative dBm number, you can use a template sensor directly in your ESPHome code.
Add this block under your sensor: section instead:

sensor:
  - platform: wifi_signal
    name: "WiFi Signal"
    id: my_wifi_signal
    update_interval: 60s

  - platform: template
    name: "WiFi Signal Percentage"
    unit_of_measurement: "%"
    device_class: "signal_strength"
    accuracy_decimals: 0
    lambda: |-
      return min(max(2 * (id(my_wifi_signal).state + 100), 0.0), 100.0);

Once installed, Home Assistant will automatically discover the new sensor.wifi_signal entity (and the percentage entity, if you added it) under your ESPHome device.



Here are the other built-in hardware and diagnostic sensors available for an ESP32 in ESPHome that you can expose to Home Assistant without needing external chips or wiring.
## 1. Internal Hardware Sensors
The ESP32 has a few built-in internal sensors you can access directly.

* Internal Temperature Sensor: Measures the temperature of the ESP32 die itself (useful for detecting overheating).

sensor:
  - platform: internal_temperature
    name: "ESP32 Internal Temperature"

* Hall Effect Sensor: Detects strong magnetic fields placed directly against the chip casing.

sensor:
  - platform: esp32_hall
    name: "ESP32 Hall Sensor"


## 2. Network & System Diagnostics
These sensors help you monitor the device's stability and network performance alongside your RSSI sensor.

* Uptime Sensor: Tracks how long the device has been running since its last reboot.

sensor:
  - platform: uptime
    name: "ESP32 Uptime"

* IP Address (Text Sensor): Exposes the current local IP address of the device to Home Assistant.

text_sensor:
  - platform: wifi_info
    ip_address:
      name: "ESP32 IP Address"

* ESPHome Version (Text Sensor): Shows the version of ESPHome currently compiled onto the chip.

text_sensor:
  - platform: version
    name: "ESPHome Version"


## 3. Power & Memory Health
Great for debugging custom code or checking if your power supply is stable.

* Free Memory (Heap): Monitors how much RAM is left on the ESP32 to prevent crashes.

sensor:
  - platform: heap
    name: "ESP32 Free Memory"

Here are the official documentation links for the base sensors and components mentioned, where you can find advanced configuration options and implementation details:
## Hardware Sensors

* 
* Internal Temperature Sensor: Look at the [ESPHome Internal Temperature Sensor Documentation](https://esphome.io/components/sensor/internal_temperature/) to see how it tracks the internal die temperature.
* Hall Effect Sensor: Review the ESPHome ESP32 Hall Sensor Documentation for notes on measuring magnetic fields and pin exclusions. [1, 2] 
* 

## Network & Diagnostics

* 
* Wi-Fi Signal Strength: Check the [ESPHome Wi-Fi Signal Sensor Documentation](https://esphome.io/components/sensor/wifi_signal/) for standard dBm tracking guidelines and alternative filtering methods. [3] 
* Wi-Fi Information (IP Address): Visit the [ESPHome Wi-Fi Info Text Sensor Documentation](https://esphome.io/components/text_sensor/wifi_info/) to see how to expose additional details like SSID, BSSID, and MAC addresses. [4] 
* Uptime Tracking: Refer to the [ESPHome Uptime Sensor Documentation](https://esphome.io/components/sensor/uptime/) to customize your device boot tracking. [5] 
* 

Would you like assistance building a single YAML file that packages all these diagnostic metrics together, or are you ready to configure Home Assistant dashboards or alerts around them?

[1] [https://esphome.io](https://esphome.io/components/sensor/internal_temperature/)
[2] [https://esphome-docs.pages.dev](https://esphome-docs.pages.dev/components/sensor/esp32_hall/)
[3] [https://esphome.io](https://esphome.io/components/sensor/wifi_signal/)
[4] [https://esphome.io](https://esphome.io/components/text_sensor/wifi_info/)
[5] [https://esphome.io](https://esphome.io/components/sensor/uptime/)

