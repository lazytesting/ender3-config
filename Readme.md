# Mods and guides

## Mods
Printer is an Ender 3 Pro with the following mods:
- 4.2.7 silent mainboard
- Orange springs
- Glass plate
- Swiss clips
- Capricorn filament tube
- OctoPrint on a Pi
- BlTouch sensor
- Lack enclosure: https://www.lets-talk-about.tech/2020/02/3d-printing-famous-ikea-lack-enclosure.html
- Filament roller: https://www.thingiverse.com/thing:3052488
- Spool holder: https://www.thingiverse.com/thing:3646853
- Hotend fix: https://www.youtube.com/watch?v=Fb4XMbZ0iA4

## Guides:
- Calibrate bed level sensor: https://letsprint3d.net/guide-how-to-calibrate-an-auto-bed-leveling-sensor/

## Cura profile

### Start GCode
```
; Ender 3 Custom Start G-code
M117 Pre-heat for leveling; lcd
M140 S{material_bed_temperature_layer_0} ; Set Heat Bed temperature
M190 S{material_bed_temperature_layer_0} ; Wait for Heat Bed temperature
M104 S160; start warming extruder to 160
G28 ; Home all axes
M155 S30 ; reduce temperature reporting rate to reduce output pollution
M117 Bed leveling ; lcd
@BEDLEVELVISUALIZER	; tell the plugin to watch for reported mesh
G29 ; Auto bed-level (BL-Touch)
M155 S3  ; reset temperature reporting
G92 E0 ; Reset Extruder
M117 Pre-heat for printing; lcd
M104 S{material_print_temperature_layer_0} ; Set Extruder temperature
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
M109 S{material_print_temperature_layer_0} ; Wait for Extruder temperature
; G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
; End of custom start GCode
```

### End Gcode
```
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-20 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positionning

G1 X0 Y{machine_depth} ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

M84 X Y E ;Disable all steppers but Z
```
