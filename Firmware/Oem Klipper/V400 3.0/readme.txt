EDIT/UPDATED. THIS WILL BE possibly become a / UNIFIED SR/V4 REPO. the old "legacy versions" will only recieve required klipper compatability updates going forward. Note" this is a less then alpha branch. code, may as well be considered "random" or "broken" the currrent release is in main repo/master.

Current beta/overhaul.

Import Notes:

pid_tune macros do not save_config to allow running both without double reboots.If pid_bed is enabled for "calibrate macro,"
-Both virtual_sdcard and variables.cfg locations may need to be changed. It depends on how Klipper was installed and what directories it's using. The assumption is it's using the printer_data directory and a "single install." Otherwise, tools like WinSCP or PuTTY can be used to find the "current" locations.

Since a clean config will have no calibration settings, a bed_mesh error will pop up and disappear after "calibrate" is run.

To avoid cluttering macros, restore "mainsail" under settings with the provided backup-mainsail.json layout to put macros under categories.

What's New?

Filament_dehydrate macro for use with a filament box or bed heater.
SR firmware emulator/speed macros for non-dynamic acceleration or adjusting print speed during filament G-code. Use "active" in the pull-down menu to resume values after a reboot. These can also be used to speed up or slow down prints.
Overhauled macros with pull-down menus available in Mainsail/Fluidd. Most macros use 1=on or 0=off.
Filament flow/rotation distance calculators.
5 extruder/effector selection macros for quick swaps or common mod support. The default will be v400 effector on a fresh config.
Rotation distance can be adjusted or saved with the extrude_140 macro. A negative value will also reverse the motor direction.
Most macros display errors/hints in the print stats section or terminal.
Built-in slicer profile overrides. By default, these are inactive until values are set. Profiles like PLA 100, PETG 94, etc can be used by saving required changes in the machine with save_profile To make a profile. first put in the flow value this also doubles as selecting. e.g pla 100 flow , all retract values and, p.a. Speed override is selecteded differently. use 1 in the "flow value" then whatever value more or less. e.g 120%. this will make the printer run 20% percent faster or 20% more of the profile.
Firmware retraction values per profile can be saved and used when a specific filament is chosen using select_profile macro, such as PLA.
To use these either click select_profile macro and, select one. the value can be anything e.g 1 nothinng specific is assigned. This will load the profile and, also the selected profile will remain active until changed. E.g If pla is selected and, the printer is rebooted this will remain said retract / flow values on boot. These can either be used alone or callee in slicers with perfilament/gcode profiles such as ideamaker/prusa/supersslicer. E.G select_profile PETG=1 would go in start_gcode or X slicers custom filament/gcode options. This should avoid to much reliance on slicers / faster settings changes. NOTE: Ensure slicers defaults on Flow are 100 or 1.0 and, Firmware retract is enabled. (Firmware retract is not required saved retract values wont work unless its enabled) regular slicer retract can also be used and, Only the flow,p.a and speed modifer values will be used. FURTHER NOTE: To turn off profile overrides simply add any value to PROFILES_OFF. This can also be put on end gcode to only use overrides on certain profiles. Tip: The variables file can be directly edited for faster chages on profiles settings or diagnostics.
The M500 macro lists "saved_variables" and displays things like current flow, rotation distance, input shaper, etc., in the terminal similar to marlin. optionally you can open the variables file to view asigned values / change things like the flow/retract profiles.

Calibrate Macro Update:

The calibrate macro now attempts to run a shaper_calibration. If no shaper is found, it will display an error, reboot, and continue to the next calibration. The terminal will show this information if an ADXL is present or if the calibration failed.
The calibrate macro has an option to change the default safe height in the pull-down menu. The default is 2mm high to avoid scrapes and should be lowered during the first print. The old default is 0.6mm high. The large height increase is to accommodate varying effectors/mods/probes.
Regular delta_calibrate/Probe_calibrate behavior remains the same as on the website. If used in the terminal, these macros will not leave the nozzle high for the first print. ALWAYS reset "zoffset" before hand aka babysteps.
The "Calibrate Settings" macro currently has the option to enable PID tuning of the bed during the calibration routine. The default behavior is off on a clean config with no variables file. It also includes the option to enable shaper or turn it off (useful for pritners with permanet adxls) value 1=on 0=off.
Prime blob extrude amount/length can now be adjusted with the prime_blob_settings macro, which also allows for extrude speed. Note that speed values are in mm/s instead of mm/min for simplicity.

Other updates include Prusa support macros, adjustable values in the pull-downs for PID bed/hotend macros, and fan speed override (m106 adjustment). Refer to the documentation at https://github.com/garethky/klipper-voron2.4-config/blob/mainline/printer_data/config/part-cooling.readme.md (created by the original author) for details on overriding fan speeds.