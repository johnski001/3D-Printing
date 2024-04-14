# Ender 3V2 machine settings
## Printer
### Printer settings

* X: 235mm
* Y: 235mm
* Z: 250mm
* Build plate shape: Rectangular
* Origin at center: N
* Heated bed: Y
* Heated build volume: N
* G-code flavor: Marlin

### Printhead settings
* X min: -26
* Y min: -32
* X max: 32
* Y max: 34
* Gantry height: 25mm
* Number of extruders: 1
* Apply extruder offsets to GCODE: Y

## Start G-code
````
M201 X500.00 Y500.00 Z100.00 E5000.00 ;Setup machine max acceleration
M203 X500.00 Y500.00 Z20.00 E50.00 ;Setup machine max feedrate
M204 P500.00 R1000.00 T500.00 ;Setup Print/Retract/Travel acceleration
M205 X8.00 Y8.00 Z0.40 E5.00 ;Setup Jerk
M220 S100 ;Reset Feedrate
M221 S100 ;Reset Flowrate

G92 E0 ; Reset Extruder
G29 P1 ; Home automatically and run mesh leveling on every print
G29 A ; Activate UBL
C108 ; Close the mesh viewer (optional)
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
````

## End G-code
````
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positioning

G1 X0 Y200 ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed
M84 ;Disable steppers
````