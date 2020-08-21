# Ender3-Better-Start-and-End-GCode
I created this custom g-code to make my prints start more reliably and quicker, while wasting as little filament as possible, while adding some quality-of-life improvements to the end g-code as well.

This code was tuned using a 0.4mm nozzle, ergo the roughly 0.4mm line width as notated in the Start G-code section, and is based on a 0.28mm layer height.
However, I have used this profile just fine with a 0.3 and 0.6mm nozzle, however, the result will vary based on your filament type, nozzle temperature, nozzle size, and other factors.

<h2>Overall Functions of this G-code</h3>
The start g-code will move to a set point on the far left of the bed, then moves towards the back of the bed, while extruding relatively fast to prime the nozzle, halfway through the line, the speed is reduced but the extrusion remains the same to continue to clear any air pockets or debris from the hotend. After this, the nozzle is raised slightly, and then your print will begin.

The end g-code will reset your feedrates to their normal 100%, in case you have forgotten to do so (written in bloo....filament blobs). (If you would prefer this not happen, simply remove or comment out these lines with a semi-colon.). The code then retracts the filament to prevent oozing, moves the z axis up slightly to avoid the print and let ooze happen safely if traveling over the print, and then park the bed at the front-most position for easy removal of the print.

<h3>Nozzle Sizing</h3>
If you are using a nozzle bigger than 0.6mm, or smaller than 0.3mm, I would tune the exstrusion amount for the line draw section. Modify the E value using a ratio of your new nozzle
For example:
Assume nozzle size 0.8mm, the line width is 2x the original, so simply multiply your E value by 2. It's simply based on the ratio of your required line width to function properly. Be sure to tune both E values when changing these parameters.

<h3>Speed</h3>
One thing to note, the feedrate is set relatively high in this g-code simply to reduce time of startup, and for less stringing when moving to start the print (gotta get that print going ASAP)
The extruder feedrate is set much higher than stock Marlin firmware allows, and thus, if you are able to extrude quickly enough, I recommend changing these settings in your printers settings using the M203 command. (EG. M203 E120 for 120mm/s) For stock extruders, I would reccommend setting this no higher than 60mm/s, but, YMMV.
Values set for the extruder are high, as I personally am using a dual-gear extruder on my setup. If you are using the stock extruder, or other single gear extruders and have slipping issues, these values may not work for you. The easiest thing to do is set max feedrate for you extruder in your EEPROM using M203 as stated above.
The value for the z-speed has also been modified. I did this as I found the stock speed of 10mm/s to be rather unecessarily slow for travel moves, this helps to reduce oozing of the filament while moving the z-axis and speeds up these travels tremendously (does not effect G28 Home Axis) I modified my own to be 20mm/s (using M203 as above) and I found that to be a nice speed.

<h2>Conclusion</h2>
This custom g-code has worked excellent for me to start my prints more reliably than others I have seen posted. This code is fast, minimizes waste, and is very clear cut in what it does.
If you have any issues with this code you are unable to resolve yourself, please create an issue and I'll be happy to try and help!



<h3>Extras</h3>
I run my printer through OctoPrint (which is BRILLIANT if you haven't used it) and have a start g-code set there with a G28 M84 to home the axis, park the nozzle against the bed, and prevent any filament that would otherwise ooze from, well, oozing!
This can cause issues with special types of filament, so it is not recommended in all cases, but I usually only print with PLA, PETG, and ocassioanly TPU and have had no issues, even with wood PLA. Again, YMMV but I recommend this to prevent having to cleanup the plastic that build on the nozzle due to ooze THEN homing. 
I was unable to put these 2 commands in the custom g-code as, at least in Cura, it completely breaks some things and temperatures go haywire at the beginning (heated bed set to maximum)
