These files provide Klipper configuration statements to add features useful when using a top cover on the Snapmaker U1.  These can be added to the Klipper configuration via the Fluidd or Mainsail interface.  It is recommended to add the configuration statements to Configuration Files/extended/klipper/custom.cfg.  Alternatively, they can be added to printer.cfg, but they will be lost when there is a firmware update to the Snapmaker U1.

1.  Rockchip_Temp_Display adds a temperature readout of the U1's Rockchip controller in the Thermals panel of Fluidd or the Temperatures panel of Mainsail.  These statements can be used on any Snapmaker U1.

2.  TMC2240_Configuration optimizes the TMC2240 stepper drivers for use with Snapmaker U1s using the Shenzhen Keli Motor Ltd. model BJ42D29-100V78 stepper motors.  This configuration can be used on any Snapmaker U1 using those stepper motors.

3.  Panda_Breath_Control only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, is flashed with the Pax12 firmware and in which a Panda Breath running stock firmware 1.0.3 or higher has been installed.  DO NOT USE THIS IF USING DRAGONBREATH FIRMWARE IN THE PANDA BREATH!  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.

4.  Panda_Breath(DragonBreath)_Control only works on a Snapmaker U1 that includes the official Snapmaker U1 Top Cover, is flashed with the Pax12 firmware and in which a Panda Breath running DragonBreath firmware has been installed.  DO NOT USE THIS IF USING STOCK FIRMWARE IN THE PANDA BREATH!  These statements provide chamber pre-heating and filament macros in the Fluidd or Mainsail interface.

Notes:

1. In the Panda_Breath_Control and Panda_Breath(DragonBreath)_Control statements there is the following section defining default drying parameters:  

        'PLA':       {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600},
        'Silk_PLA':  {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600},
        'PETG':      {'bed': 60, 'chamber': 60, 'int_fan': 0.45, 'exh_fan': 0.20, 'time': 21600},
        'ABS':       {'bed': 70, 'chamber': 70, 'int_fan': 0.50, 'exh_fan': 0.20, 'time': 21600},
        'ASA':       {'bed': 70, 'chamber': 70, 'int_fan': 0.50, 'exh_fan': 0.20, 'time': 21600},
        'PVA':       {'bed': 50, 'chamber': 50,  'int_fan': 0.40, 'exh_fan': 0.20, 'time': 21600}

'bed' is bed temperature, 'chamber' is chamber temperature, 'int_fan' is the Snapmaker U1 Top Cover circulation fan, 'exh_fan' is the Snapmaker U1 Top Cover exaust fan, and time is the time the filament drying cycle runs in seconds (21600 seconds is 6 hours).  

2.  If it is desired to use filament drying and chamber pre-heating macros with a top cover that does not have fans, remove the 'int_fan' and 'exh_fan' settings from the above statements, remove the {% set int_speed = profiles[selected_material].int_fan %} and {% set exh_speed = profiles[selected_material].exh_fan %} statements from the macros, and remove every SET_FAN_SPEED FAN=circulation_fan ... and SET_FAN_SPEED FAN=exhaust_fan ... command from the startup, timer completion, and cancellation macros.  But, this has not been tested on any cover other than the official Snapmaker U1 top cover.  Your milage may vary.

3.  It is suggested to create a Chamber Heating and Filament Drying macro category in Fluidd or Mainsail, and move the macros into that category.
