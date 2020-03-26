# rpi-screenbrightness-mqtt

This service can be used to control the backlight of a raspberrypi (touchscreen) e.g. the official 7" touchsceen via mqtt.   
The default config works with homeassistant if used with the config example for home assistant below. (You just have
to enter your mqtt broker info)  
The project uses the supervisord package, so it will run automatically on startup and restart upon error. The script publishes the current 
state of power and brightness every 10 seconds.

## How to install:

1. clone this repository to a folder (e.g. /opt/mqtt_backlight)
2. install service file into /etc/systemd/system/mqtt_backlight.service
3. make the mqtt_backlight file executable for the user running the service

## Trouble shooting
* to enable debug output set "debug" to True or 1 in `/etc/rpi_screenbrightness_mqtt.conf`  
* check journalctl 

### Home Assistant config example

to enable control of the backlight via a homeassistant light use the following configuration:

~~~~
light:
  - platform: mqtt
    name: "dashboard backlight"
    state_topic: "stat/rpi1/power"
    command_topic: "cmnd/rpi1/power"
    brightness_state_topic: "stat/rpi1/brightness"
    brightness_command_topic: "cmnd/rpi1/brightness"
    brightness_scale: 100
~~~~
