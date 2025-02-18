# Pychonet

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]](LICENSE)
![Project Maintenance][maintenance-shield]
[![BuyMeCoffee][buymecoffeebadge]][buymecoffee]


A library for interfacing with the ECHONETlite protocol as commonly used in Japan.
Useful for interfacing to many interesting devices such as HVACs,
electric car chargers, rice cookers (not joking), and solar systems
that support ECHONETLite.

The current functionality is limited to a few ECHONETLite classes, notably HVAC
but it can easily be extended to any ECHONETlite classes required.

The basic boilerplate EchoNetInstance class can be used to provide
raw connectivity to any compatible device but it is up to the developer
to create useful classes. Any ECHONETlite class additions to the library are welcome.

It is designed to work with Python 3.9.5+

## Instructions

Simplest way to install is to use pip:

```
pip install pychonet
```

## Basic usage
### Discover a list of ECHONETlite instances using:
```python
import pychonet as echonet
echonet_instances = echonet.discover()
print(echonet_instances)
[{'netaddr': '192.168.1.6', 'eojgc': 1, 'eojcc': 48, 'eojci': 1, 'group': 'Air conditioner-related device group', 'code': 'Home air conditioner'}]
```

### Create a HVAC ECHONETlite instance
```python
aircon = echonet.HomeAirConditioner("192.168.1.6")

### Turn HVAC on or off:
```python
aircon.on()
aircon.off()
aircon.getOperationalStatus()
{'status': 'off'}
```

### Set or Get a HVACs target temperature
```python
aircon.setOperationalTemperature(25)
aircon.getOperationalTemperature()
{'set_temperature': 25}
```

### Set or Get a HVACs mode of operation:
```python
supported modes =  'auto', 'cool', 'heat', 'dry', 'fan_only', 'other'

aircon.setMode('cool')
aircon.getMode()
{'mode': 'cool'}
```
### Set or Get a HVACs fan speed:

Note - your HVAC may not support all fan speeds.
```python
supported modes = 'auto', 'minimum', 'low', 'medium-Low', 'medium', 'medium-high', 'high', 'very high', 'max'

aircon.setFanSpeed('medium-high')
aircon.getFanSpeed()
{'fan_speed': 'medium-high'}
```
### Get HVAC attributes at once:
```python
aircon.update()
{'status': 'On', 'set_temperature': 25, 'fan_speed': 'medium-high', 'room_temperature': 25, 'mode': 'cooling'}
```
## Using this library with Home Assistant

NOTE: For Home Assistant users there is now a dedicated repo for the related Home Assistant 'Mitsubishi' custom component that makes use of this Python library:
(https://github.com/scottyphillips/mitsubishi_hass)

'example_hvac.py' gives you an idea how to drive a HVAC directly from Python using this library.

## Hall of Fame
Thanks to khcnz (Karl Chaffey) and gvs for helping refector the old code
and contributing to testing.

Thanks to Dick Swart, Masaki Tagawa, Paul, khcnz,  Kolodnerd, and Alfie Gerner
for each contributing code updates to to the original 'mitsubishi_echonet'
and therefore this library

Thanks to Jeffro Carr who inspired me to write my own native Python ECHONET
library for Home Assistant.
Some ideas in his own repo got implemented in my own code.
(https://github.com/jethrocarr/echonetlite-hvac-mqtt-service.git)

Also big thanks to Futomi Hatano for open sourcing a well-documented ECHONET Lite
library in Node JS that formed
the basis of my reverse engineering efforts.
(https://github.com/futomi/node-echonet-lite)

## License

This application is licensed under an MIT license, refer to LICENSE for details.

***
[pychonet]: https://github.com/scottyphillips/pychonet
[releases-shield]: https://img.shields.io/github/release/scottyphillips/pychonet.svg?style=for-the-badge
[releases]: https://github.com/scottyphillips/pychonet/releases
[license-shield]:https://img.shields.io/github/license/scottyphillips/pychonet?style=for-the-badge
[buymecoffee]: https://www.buymeacoffee.com/RgKWqyt?style=for-the-badge
[buymecoffeebadge]: https://img.shields.io/badge/buy%20me%20a%20coffee-donate-yellow.svg?style=for-the-badge
[maintenance-shield]: https://img.shields.io/badge/Maintainer-Scott%20Phillips-blue?style=for-the-badge
