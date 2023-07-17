### Common Commands
| Command | Description |
| --- | --- |
| ; | Text after semicolon makes no effect (for comments and explanations) |
| G0 & G1 | To initiate movement (G0 for non-extrusion movement and G1 for extrusion movement) |
| F | Feed rate (speed) in mm/min |
| X Y Z | Coordinates in mm |
| E | Extrusion amount in mm |

G-code is a common language for CNC (Computer Numerical Control) machine that includes a list of operations. In the case of 3D FDM printers, this includes operations on how to move, how much filament to extrude, what temperature to set, and more. G-code comes in different "flavors" which indicates what commands are accepted and how they are interpreted by the printer. In this lesson, we will focus on the Marlin flavor, although other flavors only have small differences. For a full list of G-code commands, please refer to the resources here: [marlinfw.org/meta/gcode](http://marlinfw.org/meta/gcode) and [reprap.org/wiki/G-code](http://reprap.org/wiki/G-code) 

G-code is a common language for CNC (Computer Numerical Control) machine that includes a list of operations. In the case of 3D FDM printers, this includes operations on how to move, how much filament to extrude, what temperature to set, and more. G-code comes in different "flavors" which indicates what commands are accepted and how they are interpreted by the printer. In this lesson, we will focus on the Marlin flavor, although other flavors only have small differences. For a full list of G-code commands, please refer to the resources here: [marlinfw.org/meta/gcode](http://marlinfw.org/meta/gcode) and [reprap.org/wiki/G-code](http://reprap.org/wiki/G-code)

```nasm

M104 S0 ;extruder heater off
M140 S0 ;heated bed heater off (if you have it)

G91 ;relative positioning

G1 E-1 F300 ;retract the filament a bit 
before lifting the nozzle, to release some
of the pressure

G1 Z+0.5 E-5 X-20 Y-20 F9000 ;move Z up a
bit and retract filament even more

G28 X0 Y0 ;move X/Y to min endstops, so
the head is out of the way

M84 ;steppers off
G90 ;absolute positioning

```



































