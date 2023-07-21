# dbus-mqtt-temperature - Emulates a temperature sensor from MQTT data

<small>GitHub repository: [mr-manuel/venus-os_dbus-mqtt-temperature](https://github.com/mr-manuel/venus-os_dbus-mqtt-temperature)</small>

### Disclaimer

I wrote this script for myself. I'm not responsible, if you damage something using my script.


### Purpose

The script emulates a temperature sensor in Venus OS. It gets the MQTT data from a subscribed topic and publishes the information on the dbus as the service `com.victronenergy.temperature.mqtt_temperature` with the VRM instance `100`.


### Config

Copy or rename the `config.sample.ini` to `config.ini` in the `dbus-mqtt-temperature` folder and change it as you need it.


### JSON structure

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


### Install

1. Copy the `dbus-mqtt-temperature` folder to `/data/etc` on your Venus OS device

2. Run `bash /data/etc/dbus-mqtt-temperature/install.sh` as root

   The daemon-tools should start this service automatically within seconds.

### Uninstall

Run `/data/etc/dbus-mqtt-temperature/uninstall.sh`

### Restart

Run `/data/etc/dbus-mqtt-temperature/restart.sh`

### Debugging

The logs can be checked with `tail -n 100 -f /data/log/dbus-mqtt-temperature/current | tai64nlocal`

The service status can be checked with svstat `svstat /service/dbus-mqtt-temperature`

This will output somethink like `/service/dbus-mqtt-temperature: up (pid 5845) 185 seconds`

If the seconds are under 5 then the service crashes and gets restarted all the time. If you do not see anything in the logs you can increase the log level in `/data/etc/dbus-mqtt-temperature/dbus-mqtt-temperature.py` by changing `level=logging.WARNING` to `level=logging.INFO` or `level=logging.DEBUG`

If the script stops with the message `dbus.exceptions.NameExistsException: Bus name already exists: com.victronenergy.temperatureinverter.mqtt_temperature"` it means that the service is still running or another service is using that bus name.

### Multiple instances

It's possible to have multiple instances, but it's not automated. Follow these steps to achieve this:

1. Save the new name to a variable `driverclone=dbus-mqtt-temperature-2`

2. Copy current folder `cp -r /data/etc/dbus-mqtt-temperature/ /data/etc/$driverclone/`

3. Rename the main script `mv /data/etc/$driverclone/dbus-mqtt-temperature.py /data/etc/$driverclone/$driverclone.py`

4. Fix the script references for service and log
    ```
    sed -i 's:dbus-mqtt-temperature:'$driverclone':g' /data/etc/$driverclone/service/run
    sed -i 's:dbus-mqtt-temperature:'$driverclone':g' /data/etc/$driverclone/service/log/run
    ```

5. Change the `device_name` and increase the `device_instance` in the `config.ini`

Now you can install and run the cloned driver. Should you need another instance just increase the number in step 1 and repeat all steps.

### Compatibility

It was tested on Venus OS Large `v2.92` on the following devices:

* RaspberryPi 4b
* MultiPlus II (GX Version)

### Screenshots

<details><summary>MQTT Temperature</summary>

![Temperature - device list](/screenshots/temperature_device-list.png)
![Temperature - device list - mqtt temperature 1](/screenshots/temperature_device-list_mqtt-temperature-1.png)
![Temperature - device list - mqtt temperature 2](/screenshots/temperature_device-list_mqtt-temperature-2.png)

### GuiMods

![Temperature - pages](/screenshots/temperature_pages_guimods.png)

</details>


## Supporting/Sponsoring this project

You like the project and you want to support me?

[<img src="https://github.md0.eu/uploads/donate-button.svg" height="50">](https://www.paypal.com/donate/?hosted_button_id=3NEVZBDM5KABW)
