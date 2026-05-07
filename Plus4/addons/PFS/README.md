# Qidi Plus4 Proportional Sync Feedback sensor

> [!NOTE]
> Not yet tested!

The Qidi Plus4 features an encoder, while the Q2 and Max4 get hubs equipped with a tension sensor.
Both have their advantages and disadvantages.

The Plus4 however does also have a tension sensor at point where the PTFE tube enters the heated chamber. This simple switch sensor, meant for detecting filament tangles, can be replaced with a cheap PSF if the tension sensor fails or if you want to have the additional information.

This folder contains the 3D files for the sensor that fit the Plus4 easily, as well as the configuration files.

Credit for the CAD files goes to [@fxwoody](https://www.youtube.com/@frankthebum)! ❤️

## Installation

### Hardware

1. Order the Aliexpress kit (or source the components yourself).
2. Print the case and mounting plate in [`./3D Files`](./3D%20files/).
3. Put it together
4. Take the back panel of the Plus4 off to expose the tangle sensor.
5. Replace the tangle sensor with the PSF sensor. 
6. *TBD - does the cable need rework?*
7. From printer.cfg, remove the following section (or any other sensor section using the PC3 pin)
```diff
-[filament_switch_sensor fila]
-pause_on_runout: True
-runout_gcode:
-    M118 Filament tangle detected
-event_delay: 3.0
-pause_delay: 0.5
-switch_pin:U_1:PC3
```

8. In mmu_hardware.cfg `SENSORS` section, add (*TBD - YOU NEED TO FIGURE THIS OUT YOURSELF, THIS IS A TEMP PLACEHOLDER*):
```
sync_feedback_analog_pin: PC3 			# The ADC pin where the proportional filament pressure sensor is installed
sync_feedback_analog_max_compression: 1		# Raw sensor reading at max filament compression (buffer squeezed)
sync_feedback_analog_max_tension: 0		# Raw sensor reading at max filament tension (buffer expanded)
sync_feedback_analog_neutral_point: 0.50	# Biasing of neutral point (sensor value 0). Normally close to 0.5
```

9. [Calibrate if needed](https://github.com/moggieuk/Happy-Hare/wiki/Synchronized-Gear-Extruder#-analogproportional-types-p).

### Configs


For more details on the PSF, see:
[Original PSF repo](https://github.com/kashine6/Proportional-Sync-Feedback-Sensor?tab=readme-ov-file)
[PSF kit on AliExpress (easiest way to get the non-3D-printed components)](https://pl.aliexpress.com/item/1005010470743517.html?gatewayAdapt=glo2pol)
[Happy Hare documentation on sync sensors](https://github.com/moggieuk/Happy-Hare/wiki/Synchronized-Gear-Extruder#-analogproportional-types-p)
