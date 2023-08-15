# Regenfass - Debugging

On development you often point to bugs and errors. To make it easier for us to find and fix them, we have integrated a debug mode into the Regenfass. This mode can be activated in the config file. The debug mode is only active if the Regenfass is started with the parameter `--debug` or `-d`. The debug mode is deactivated by default.

## Pinout

![Pinout](https://resource.heltec.cn/download/WiFi_LoRa32_V3/HTIT-WB32LA(F)_V3.png)

## Common errors

### Error: 'heltec.h' file not found

```shell
src/main.cpp:2:10: fatal error: heltec.h: No such file or directory
```

Add `heltec.h` as dependency to your `platformio.ini` file:

```ini
[env:heltec_wifi_lora_32_V2]
platform = espressif32
board = heltec_wifi_lora_32_V2
framework = arduino
lib_deps = heltec/ESP32_LoRaWAN@^1.1.1
```

### Error: 'XXX' was not declared in this scope

```shell
'LoRaWAN_DEBUG_LEVEL' was not declared in this scope
'ACTIVE_REGION' was not declared in this scope
'RST_LoRa' was not declared in this scope
'DIO0' was not declared in this scope
'DIO1' was not declared in this scope
'WIFI_LED' was not declared in this scope
'LoRa_LED' was not declared in this scope
```

More information [here](http://community.heltec.cn/t/example-for-esp32-lora-node-to-a-lora-gateway-via-lorawan-protocol-does-not-work/1051)

#### Solution 1

```c++
#define LoRaWAN_DEBUG_LEVEL 1
#define ACTIVE_REGION LORAWAN_REGION_EU868
#define RST_LoRa 14
#define DIO0 26
#define DIO1 33
#define WIFI_LED 25
#define LoRa_LED 18
```

#### Solution 2

Custom board definition:
```json
{
  "build": {
    "core": "esp32",
    "extra_flags": "-DLoRaWAN_DEBUG_LEVEL=1 -DACTIVE_REGION=LORAWAN_REGION_EU868 -DRST_LoRa=14 -DDIO0=26 -DDIO1=33 -DWIFI_LED=25 -DLoRa_LED=18",
    "f_cpu": "240000000L",
    "mcu": "esp32",
    "variant": "heltec_wifi_lora_32_V2"
  },
  "frameworks": [
    "arduino"
  ],
  "name": "Heltec WiFi LoRa 32",
  "upload": {
    "maximum_ram_size": 327680,
    "maximum_size": 1310720,
    "protocol": "espota",
    "require_upload_port": true,
    "speed": 921600
  },
  "url": "https://heltec.org/project/wifi-lora-32/",
  "vendor": "Heltec Automation",
  "version": "1.0.0"
}
```

More information see [here](https://docs.platformio.org/en/latest/platforms/creating_board.html)

### Error: error: 'class McuClass' has no member named 'begin'

```shell
error: 'class McuClass' has no member named 'begin'
````

#### Solution



```c++



