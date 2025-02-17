# Changelog

## v0.0.6
* Changed: Allow to use customized JSON property names by @hoone123

## v0.0.5
* Added: MQTT message can now also be only a float number
* Added: New temperature types room, outdoor, waterheater and freezer
* Changed: Broker port missing on reconnect
* Changed: Fixed service not starting sometimes

## v0.0.4
* Changed: Add VRM ID to MQTT client name
* Changed: Fix registration to dbus https://github.com/victronenergy/velib_python/commit/494f9aef38f46d6cfcddd8b1242336a0a3a79563

## v0.0.3
* Changed: Fixed problems when timeout was set to `0`.

## v0.0.2
* Added: Timeout on driver startup. Prevents problems, if the MQTT broker is not reachable on driver startup

## v0.0.1
Initial release
