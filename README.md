# dbus-mqtt-temperature - Emulates a temperature sensor from MQTT data

<small>GitHub repository: [mr-manuel/venus-os_dbus-mqtt-temperature](https://github.com/mr-manuel/venus-os_dbus-mqtt-temperature)</small>

## Index

1. [Disclaimer](#disclaimer)
1. [Supporting/Sponsoring this project](#supportingsponsoring-this-project)
1. [Purpose](#purpose)
1. [Config](#config)
1. [JSON structure](#json-structure)
1. [Install / Update](#install--update)
1. [Uninstall](#uninstall)
1. [Restart](#restart)
1. [Debugging](#debugging)
1. [Compatibility](#compatibility)
1. [Screenshots](#screenshots)


## Disclaimer

I wrote this script for myself. I'm not responsible, if you damage something using my script.


## Supporting/Sponsoring this project

You like the project and you want to support me?

[<img src="https://github.md0.eu/uploads/donate-button.svg" height="50">](https://www.paypal.com/donate/?hosted_button_id=3NEVZBDM5KABW)


## Purpose

The script emulates a temperature sensor in Venus OS. It gets the MQTT data from a subscribed topic and publishes the information on the dbus as the service `com.victronenergy.temperature.mqtt_temperature` with the VRM instance `100`.


## Config

Copy or rename the `config.sample.ini` to `config.ini` in the `dbus-mqtt-temperature` folder and change it as you need it.


## JSON structure

<details><summary>Minimum required</summary>

```json
{
    "temperature": 22.0
}
```

OR

```json
{
    "value": 22.0
}
```

OR

```json
22.0
```


</details>

<details><summary>Full</summary>

```json
{
    "temperature": 22.0,
    "humidity": 62.927,
    "pressure": 102.104
}
```
</details>


## Install / Update

1. Login to your Venus OS device via SSH. See [Venus OS:Root Access](https://www.victronenergy.com/live/ccgx:root_access#root_access) for more details.

2. Execute this commands to download and copy the files:

    ```bash
    wget -O /tmp/download_dbus-mqtt-temperature.sh https://raw.githubusercontent.com/mr-manuel/venus-os_dbus-mqtt-temperature/master/download.sh

    bash /tmp/download_dbus-mqtt-temperature.sh
    ```

3. Select the version you want to install.

4. Press enter for a single instance. For multiple instances, enter a number and press enter.

    Example:

    - Pressing enter or entering `1` will install the driver to `/data/etc/dbus-mqtt-temperature`.
    - Entering `2` will install the driver to `/data/etc/dbus-mqtt-temperature-2`.

### Extra steps for your first installation

5. Edit the config file to fit your needs. The correct command for your installation is shown after the installation.

    - If you pressed enter or entered `1` during installation:
    ```bash
    nano /data/etc/dbus-mqtt-temperature/config.ini
    ```

    - If you entered `2` during installation:
    ```bash
    nano /data/etc/dbus-mqtt-temperature-2/config.ini
    ```

6. Install the driver as a service. The correct command for your installation is shown after the installation.

    - If you pressed enter or entered `1` during installation:
    ```bash
    bash /data/etc/dbus-mqtt-temperature/install.sh
    ```

    - If you entered `2` during installation:
    ```bash
    bash /data/etc/dbus-mqtt-temperature-2/install.sh
    ```

    The daemon-tools should start this service automatically within seconds.

## Uninstall

⚠️ If you have multiple instances, ensure you choose the correct one. For example:

- To uninstall the default instance:
    ```bash
    bash /data/etc/dbus-mqtt-temperature/uninstall.sh
    ```

- To uninstall the second instance:
    ```bash
    bash /data/etc/dbus-mqtt-temperature-2/uninstall.sh
    ```

## Restart

⚠️ If you have multiple instances, ensure you choose the correct one. For example:

- To restart the default instance:
    ```bash
    bash /data/etc/dbus-mqtt-temperature/restart.sh
    ```

- To restart the second instance:
    ```bash
    bash /data/etc/dbus-mqtt-temperature-2/restart.sh
    ```

## Debugging

⚠️ If you have multiple instances, ensure you choose the correct one.

- To check the logs of the default instance:
    ```bash
    tail -n 100 -F /data/log/dbus-mqtt-temperature/current | tai64nlocal
    ```

- To check the logs of the second instance:
    ```bash
    tail -n 100 -F /data/log/dbus-mqtt-temperature-2/current | tai64nlocal
    ```

The service status can be checked with svstat `svstat /service/dbus-mqtt-temperature`

This will output somethink like `/service/dbus-mqtt-temperature: up (pid 5845) 185 seconds`

If the seconds are under 5 then the service crashes and gets restarted all the time. If you do not see anything in the logs you can increase the log level in `/data/etc/dbus-mqtt-temperature/dbus-mqtt-temperature.py` by changing `level=logging.WARNING` to `level=logging.INFO` or `level=logging.DEBUG`

If the script stops with the message `dbus.exceptions.NameExistsException: Bus name already exists: com.victronenergy.temperatureinverter.mqtt_temperature"` it means that the service is still running or another service is using that bus name.

## Compatibility

This software supports the latest three stable versions of Venus OS. It may also work on older versions, but this is not guaranteed.

## Screenshots

<details><summary>MQTT Temperature</summary>

![Temperature - device list](/screenshots/temperature_device-list.png)
![Temperature - device list - mqtt temperature 1](/screenshots/temperature_device-list_mqtt-temperature-1.png)
![Temperature - device list - mqtt temperature 2](/screenshots/temperature_device-list_mqtt-temperature-2.png)

## GuiMods

![Temperature - pages](/screenshots/temperature_pages_guimods.png)

</details>
