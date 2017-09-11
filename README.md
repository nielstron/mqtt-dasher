# MQTT Dasher
***Emits events to MQTT when an Amazon Dash button is pressed.***

[![GitHub tag](https://img.shields.io/github/tag/stjohnjohnson/mqtt-dasher.svg)](https://github.com/stjohnjohnson/mqtt-dasher/releases)

# Configuration

The dash bridge has one yaml file for configuration:

```
---
mqtt:
    # Specify your MQTT Broker's hostname or IP address here
    host: mqtt
    # Preface for the topics $PREFACE/$TOPIC
    preface: dash

buttons:
    44:65:0d:dc:51:50: nerf_supplies

```

# Usage

_note: follow [this setup](https://github.com/hortinstein/node-dash-button#installation-instructions) first

1. Install the Node module globally

    ```
    $ npm install -g mqtt-dasher
    ```

2. Configure your buttons

    ```
    $ vi /opt/mqtt-dasher/config.yml
    ```

3. Run the server

    ```
    $ CONFIG_DIR=/opt/mqtt-dasher mqtt-dasher
    ```

4. Configured dash events now feed into MQTT


## Possible Home Assistant setup

I configured the dash button as [binary sensor](https://home-assistant.io/components/binary_sensor/) in [Home Assistant](https://home-assistant.io/). This is an example piece of text for `configuration.yaml`.

    ```
     binary_sensor:
      - platform: mqtt
        name: "Nerf supply is out"
        state_topic: "dash/nerf_supply"
        payload_on: 'active'
        payload_off: 'inactive'
        device_class: 'occupancy'
    ```
