# SFSv2OnSv07
How to add BTT SFS V2.0 on Sovol Sv07 and Sv07 Plus

# What you need
1. SFS V2.0
2. Printed part of couplerholderV0.3.3mf and SFSV2Holder.3mf
3. Tools

**IF YOU HAVE AN SV07 PLUS, YOU WILL NEED TO EXTEND THE CABLE THAT COMES WITH THE SFS V2.0 OR BUY A LONGER ONE.**

# How to
1. Remove the button plate of the printer.
2. Unconnect the old filament Runout sensor and remove it.
3. Connect the SFS V2.0.

![Mainboard](https://github.com/TomasOlsson/SFSv2OnSv07/blob/main/SovolSv07Mainboard.jpg?raw=true)

4. Run the SFS V2.0 wire where the old runout sensor wire is.
5. Mount the printed parts and the SFS V2.0
6. Add the button plate of the printer.
7. Start printer.
8. Edit printer.cfg

   Remove:
   ```
    [filament_switch_sensor my_sensor]
    #pause_on_runout: True
    #runout_gcode:
    #RESPOND TYPE=error MSG="Filament Runout! Please change filament!"
    #event_delay: 3.0
    #pause_delay: 0.5
    switch_pin:PD11
   ```

   Add:

   ```
   [filament_switch_sensor switch_sensor]
   switch_pin: PD11
   pause_on_runout: False
   runout_gcode:
     PAUSE #[pause_resume] is required in printer.cfg
     RESPOND TYPE=error MSG="No filament was detected!"
   insert_gcode:
     RESPOND TYPE=echo MSG="Filament was inserted"

   [filament_motion_sensor encoder_sensor]
   switch_pin: ^PB14
   detection_length: 3
   extruder: extruder
   pause_on_runout: False
   runout_gcode:
     PAUSE # [pause_resume] is required in printer.cfg
     RESPOND TYPE=error MSG="Filament is stuck!"
   insert_gcode:
     RESPOND TYPE=echo MSG="Filament was inserted"
   ```
9. Save and restart.
10. Check if its working:

    Mainsail: Under dashboard you will see:

    ![Mainsail](https://github.com/TomasOlsson/SFSv2OnSv07/blob/main/image.png?raw=true)

    Fluidd: You will find it under the page "Tune"

    ![Fluidd](https://github.com/TomasOlsson/SFSv2OnSv07/blob/main/fluid.png?raw=true)

11. If everything checks out try to print.

    # HAPPY PRINTING
