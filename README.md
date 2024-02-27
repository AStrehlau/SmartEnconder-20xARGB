# SmartEncoder-20xARGB

This "SmartEncoder" uses 20 adressable LEDs (SK6805-EC15 or potentially XL-1615RGBC-WS2812B) to visualize the set point of the encoder. The SmartEncoder boasts WiFI and Bluetooth capability using the ESP32, which makes it viable for Smart Home and PC control applications.
It should be noted that stock Windows does not normally have the capability to send the current volume level over BT, which is why a PC side software to take care of that will be uploaded  in the future for use as a BT PC volume knob.

<img src="/images/Lightshow.gif" alt="Lightshow" width="400">

## Hardware

You can directly order the three PCBs needed for this project using the Gerber files (generated for JLCPCB but likely to work with most common providers) or modify the PCB files at your discretion and generate new Gerber files.

Each of the three PCBs have to be completely assembled before they can be stacked in the correct order using the 3D printed spacers and either wire or very long headers. For the assembly of the Top/LED PCB it is recommended if not necessary to order a stencil with the PCBs. The other PCBs can be assembled without one if so desired.

There is a complete BOM (except the very long headers/wire and M3x25m screws!) for all three PCBs and an interactive BOM for the PCB with the ESP32 on it. There is no ibom for the other two PCBs since every capacitor used on them is 100nF, every resistor on the encoder PCB is 10k and the one resistor on the LED PCB is 330R as can be seen in the schematics.<br>
The EMI filter on the ESP32 PCB (L1, L2 and C4) can be left out and Jumper JP1 soldered instead, although it is not recommended. Doing this has no effect on the functionality.<br>
Especially if you don't plan on running intensive animations on the LEDs the 20 bypass capacitors are definitely overkill (even though the datasheet might disagree). If you want to save on parts/ time spent placing them you can just place C14, C15 and C16 which was more than enough in my testing even just one of them might work for you.

<img src="/images/PCBs_unpopulated.jpeg" alt="Unpopulated PCBs" width="900">

<img src="/images/PCB_Stackup.jpeg" alt="PCBStackup" width="400">

## 3D printed case

Thanks to [Nedos on Thingiverse](https://www.thingiverse.com/nedosdergolem/) designing a case including two knob versions for you to choose from and anti-bleed part for this project you can simply download the files and print them.<br>
The holes in the knob are meant to be filled with regular 1.75mm diameter transparent filament and either both surfaces cut flush using a side cutter or even sanded down for a better look.<br>
The anti-bleed part can simply be put on the LEDs making sure not to damage them.<br>
For assembly you only need the printed parts including spacers and M3x25mm screws, preferably with a flat underside.

<img src="/images/FinishedEncoder.jpeg" alt="Finished Encoder" width="400">

## Software 

Because of layout reasons the LEDs have to be addressed in the opposite than expected order (LED number on the silkscreen is correct) which can result in longer code depending on the application.

There is a demo code for the LEDs which is just a slightly modified version of the Adafruit NEOPIXEL "strandtest" example to check if the LEDs are soldered correctly and undamaged as well as to give you a nice lightshow as can be seen at the top.<br>
This code can be flashed onto the ESP32 using the Arduino IDE.

Also available is a ESPHome configuration to integrate the SmartEncoder into HomeAssistant.

WIP: Code for ESP and PC to communicate via Serial over Bluetooth to use as a volume knob with accurate volume display on the SmartEncoder side