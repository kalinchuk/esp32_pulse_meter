# ESP32 Pulse Water Meter

The following schematic and YAML are for building and configuring a pulse water meter reader using an ESP32 board and ESPHome.

## Schematic
The schematic is using the ESP32-WROOM DevKitC board since it contains an external antenna connection.

![Schematic_New Project_2023-06-02 (2)](https://github.com/kalinchuk/esp32_pulse_meter/assets/1035984/85db671c-8e7c-491f-ad05-b385638cae6d)

## YAML Configuration

Create a new ESP32 device in ESPHome and use the following YAML configuration underneath the default configuration that is created in the device YAML file.

Note that this configuration is using pin GPIO26 to read one water meter and that `pullup` is enabled.

```
sensor:
  - platform: pulse_counter
    update_interval: 6s
    name: "Water Meter Pulse Counter"
    id: water_meter_pulse_counter
    pin:
      number: GPIO26
      mode:
        input: true
        pullup: true
  - platform: pulse_meter
    name: "Water Meter"
    unit_of_measurement: "gal/min"
    icon: "mdi:water"
    pin:
      number: GPIO26
      mode:
        input: true
        pullup: true
    total:
      name: "Water Meter Total"
      unit_of_measurement: "gal"
      id: water_meter_total
      accuracy_decimals: 1
      device_class: water
      state_class: total_increasing
```
