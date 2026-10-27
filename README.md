These files provide Klipper configuration statements to add features useful when using a top cover on the Snapmaker U1.  
These can be added to the Klipper configuration via the Fluidd or Mainsail interface.  These files are provided here for development purposes.  AI (ChatGPT) was used in the development of the chamber pre-heating and filament drying configurations.

**WHERE TO COPY THE KLIPPER STATEMENTS CONTAINED IN THE FILES**

-   If using Paxx12 firmware, copy the statements to Configuration Files/extended/klipper/custom.cfg.  They should stay persistent, even after Paxx12 firmware updates.
-   If using stock firmware, create a new file in Configuration Files, name that new file 'custom.cfg', and copy the statements to that file.  In printer.cfg add the following line, somewhere near the top:
        [include custom.cfg]
That line will need to be re-added to printer.cfg after firmware updates.
-  Note that some of the files work both with stock firmware and Paxx12 firmwhere, while other files work with one or the other.  Carefully read each file's description below for different use cases.

**FILE DESCRIPTIONS AND USE CASES**

1.  Rockchip_Temp_Display adds a temperature readout of the U1's Rockchip controller in the Thermals panel of Fluidd or the Temperatures panel of Mainsail.  These statements can be used on any Snapmaker U1, regardless of whether it uses stock firmware or Paxx12 firmware.
-   Rockchip_Temp_Display has been thoroughly tested in Fluidd, and is expected to work in Mainsail.
  
2.  TMC2240_Configuration optimizes the TMC2240 stepper drivers for use with Snapmaker U1s using the Shenzhen Keli Motor Ltd. model BJ42D29-100V78 stepper motors.  This configuration can be used on any Snapmaker U1 using those stepper motors.  Credit for this configuration goes to crusardgameamos; it is a feature suggestion crusardgameamos posted for Paxx12.  THANK YOU, crusardgameamos!!!  If a future version of Paxx12 includes this or a similar TMC2240 configuration, then remove these statements from your Klipper configuration.
-   TMC2240_Configuration has been tested to a limited extent, and shown to reduce stepper driver temperatures around 8 - 9 C.  Consider this beta.  If bugs are found, please report them here.

3.  Panda_Breath_Control only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, is flashed with the Paxs12 firmware, and in which a Panda Breath running stock firmware 1.0.3 or higher has been installed.  DO NOT USE THIS IF USING DRAGONBREATH FIRMWARE IN THE PANDA BREATH!  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.
-   Updates from Panda_Breath(DragonBreath)_Control have been back ported to Panda_Breath_Control since the last time Panda_Breath_Control was tested.  Consider this experimental.  If bugs are found, please report them here.

4.  Panda_Breath(DragonBreath)_Control only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, is flashed with the Paxs12 firmware, and in which a Panda Breath running DragonBreath firmware has been installed.  DO NOT USE THIS IF USING STOCK FIRMWARE IN THE PANDA BREATH!  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.
-   Panda_Breath(DragonBreath)_Control has been tested and optimized.  Consider this beta.  If bugs are found, please report them here.

5.  Temp_Control_No_Chamber_Heater_Pax12 only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, is flashed with the Paxs12 firmware, but does not have a dedicated chamber heater.  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.
-   Temp_Control_No_Chamber_Heater was tested.  Consider this early beta.  If bugs are found, please report them here.

6.  Temp_Control_No_Chamber_Heater_Stock_Firmware only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, uses stock firmware, but does not have a dedicated chamber heater.  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.
-   Temp_Control_No_Chamber_Heater has not been tested tested.  Consider this experimental.  If bugs are found, please report them here.


Notes:

1. In the Panda_Breath_Control and Panda_Breath(DragonBreath)_Control statements there is the following section defining default drying parameters:  

        'PLA':       {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600},
        'Silk_PLA':  {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600},
        'PETG':      {'bed': 60, 'chamber': 60, 'int_fan': 0.45, 'exh_fan': 0.20, 'time': 21600},
        'ABS':       {'bed': 70, 'chamber': 70, 'int_fan': 0.50, 'exh_fan': 0.20, 'time': 21600},
        'ASA':       {'bed': 70, 'chamber': 70, 'int_fan': 0.50, 'exh_fan': 0.20, 'time': 21600},
        'PVA':       {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600}

'bed' is bed temperature, 'chamber' is chamber temperature, 'int_fan' is the Snapmaker U1 Top Cover circulation fan, 'exh_fan' is the Snapmaker U1 Top Cover exaust fan, and time is the time the filament drying cycle runs in seconds (21600 seconds is 6 hours).  Temp_Control_No_Chamber_Heater_Pax12 and Temp_Control_No_Chamber_Heater_Stock_Firmware each include a similar section, but without 'chamber' values.  If you wish to experiment with different values temperatures, fan settings and times, do so in this section.

2.  If it is desired to use filament drying and chamber pre-heating macros with a top cover that does not have fans, remove the 'int_fan' and 'exh_fan' settings from the above statements, remove the {% set int_speed = profiles[selected_material].int_fan %} and {% set exh_speed = profiles[selected_material].exh_fan %} statements from the macros, and remove every SET_FAN_SPEED FAN=circulation_fan ... and SET_FAN_SPEED FAN=exhaust_fan ... command from the startup, timer completion, and cancellation macros.  But, this has not been tested on any cover other than the official Snapmaker U1 top cover.  Your milage may vary.

3.  It is suggested to create a Chamber Heating and Filament Drying macro category in Fluidd or Mainsail, and move the macros into that category.
