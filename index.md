# LightHub — Developer Documentation

**LightHub** is a flexible open-source smart-home controller firmware for
Arduino Mega 2560, Arduino Due, ESP8266, ESP32 / ESP32-C3, STM32, NRF52840 and M5Stack.

Links:
- [Source code](https://github.com/anklimov/lighthub)
- [User documentation (RU)](https://github.com/anklimov/lighthub/tree/master/documentation)
- [Wiki (RU)](https://www.lazyhome.ru/dokuwiki/doku.php?id=start)
- [Releases](https://github.com/anklimov/lighthub/releases)

## What is LightHub?

A microcontroller-based smart-home hub that exposes every physical channel as an
MQTT-addressable "item" (virtual channel):

```
myhome/in/<device>/<item>[/subitem]/<suffix>   <- commands
myhome/s_out/<device>/<item>[/subitem]/<suffix> <- status
```

- **24 channel types** (`CH_*`, 0..23): DMX dimmers, PWM, relays, groups, thermostats,
  PID, Modbus (dimmer + universal master), Haier AC, NeoPixel strips, motorized gates,
  UART bridges, relay-PWM, multizone ventilation (`VENTS`), elevator, counters,
  humidifier, Mercury energy meters, sprinkler controller.
- **Inputs**: buttons with single/double/triple/long-press detection, analog inputs with
  `map` transformations, rotary encoders with profiles, DHT22, CCS811, HDC1080, 1-Wire.
- **Buses**: Modbus RTU, CAN (50 kbit/s, non-IP "lightspot" controllers), IP-Modbus gateway,
  UART bridges, 1-Wire (DS2482).
- **Integrations**: Home Assistant, OpenHAB, Node-Red, HomeRemote; Homie discovery topics;
  OTA updates; JSON config from server or via web/CLI.

## Doxygen API reference

The complete API reference for the firmware source is published under
[doxygen/](doxygen/index.html).

Highlights:
- [`item.h`](doxygen/item_8h.html) — items (virtual channels), channel types, suffixes
- [`itemCmd.h`](doxygen/itemCmd_8h.html) — command set and command codes
- [`inputs.h`](doxygen/inputs_8h.html) — input types (buttons, sensors, rotary encoder)
- [`candriver.h`](doxygen/candriver_8h.html) — CAN protocol (datagram format, payload types)
- [`config.h`](doxygen/config_8h.html) — config load/save, ETag, MAC
- [`modules/out_*.h`](doxygen/modules_2out_ac_8h.html) — one driver class per channel type
  (JSON config format, handled commands, published status topics)

## Building

```bash
git clone https://github.com/anklimov/lighthub
cd lighthub
pio run -e <target>          # due | mega2560 | esp32-wifi | esp32c3-wifi |
                             # lighthub21 | nrf52840 | stm32 | ... (16 targets)
```

Precompiled binaries for all targets are attached to the
[GitHub releases](https://github.com/anklimov/lighthub/releases).
