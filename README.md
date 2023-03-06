# Geozon-RG-01--E27-BK7231T-WB2L--SM2135
RGBCW Лампа, цоколь E27 Модуль WB2L ( чип BK7231 ) драйвер SM2135

OpenBeken:
![изображение](https://user-images.githubusercontent.com/64173457/223051331-79944bf3-02e1-4933-bbbd-02d2fcaf5c21.png)
![изображение](https://user-images.githubusercontent.com/64173457/223051525-6f7fe76d-109d-4f8c-9253-60bf13ec48db.png)
StartupCommand: SM2135_Current 0x07 0x02
![изображение](https://user-images.githubusercontent.com/64173457/223051713-d4bbab86-33d1-4c63-9a4f-c80fe730288f.png)


LibreTuya:
```
substitutions:
  board_name: rg01_1
esphome:
  name: $board_name
  project:
    name: "RG-01/Geozon.LibreTuya"
    version: "WB2L(BK7231T)"
  comment: "Geozon"

libretuya:
  board: wb2l
  framework:
    version: dev

external_components:
  - source:
      type: local
      path: my_components


preferences:
  flash_write_interval: 1min

api:
  encryption:
    key: !secret keyapi 
  reboot_timeout: 0s

ota:
  password: !secret passwordota


logger:
  baud_rate: 0

captive_portal:
wifi:
  ssid: !secret wifi1
  password: !secret password1

  ap:
    ssid: "$board_name Hotspot"
    password: !secret password1


web_server:
  port: 80  


button:
  - platform: restart
    name: Reset.$board_name

sm2135:
  data_pin: P8
  clock_pin: P7

output:
  - platform: sm2135
    id: output_red
    channel: 2
    max_power: 0.8
  - platform: sm2135
    id: output_green
    channel: 0
    max_power: 0.8
  - platform: sm2135
    id: output_blue
    channel: 1
    max_power: 0.8
  - platform: sm2135
    id: output_cold_white
    channel: 3
    max_power: 1
  - platform: sm2135
    id: output_warm_white
    channel: 4
    max_power: 1

light:
  - platform: rgbww
    name:  $board_name
    id: light1
    red: output_red
    green: output_green
    blue: output_blue
    cold_white: output_cold_white
    warm_white: output_warm_white
    cold_white_color_temperature: 6500 K
    warm_white_color_temperature: 2700 K
    color_interlock: true
    constant_brightness: true
    restore_mode: RESTORE_AND_ON
    gamma_correct: false
sensor:
  - platform: wifi_signal
    name: WiFi_Signal.$board_name
  - platform: uptime
    name: uptime_sensor.$board_name
```
