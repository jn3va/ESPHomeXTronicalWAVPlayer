# ESPHome XTronical WAV Player
How to use XTronical's wav player from ESPHome

XTronical has a very nice set of tutorials and a library for playing WAV files on an ESP8266 or ESP32
https://www.xtronical.com/the-dacaudio-library-download-and-installation/

To use this with ESPHome 

1) Create a folder inside of the config/esphome folder on homeassistant called esp_wav_player_incl
2) Place Xtronicals DAC library for WAV (XT_DAC_Audio) in this folder.  You need 3 files

     MusicDefinitions.h
     
     XT_DAC_Audio.cpp
     
     XT_DAC_Audio.h
     
     
     You can get these files from XTronicals site linked above.  I have included the files in the example sub-folder listed here.
     I've tested this setup with verison 4.2.1 / 2019
     
3) Also place esp_wav_player.h in this folder
 This file is the interface between ESPHome and XTronicals code.
 This file contains the wav data encoded as hex, global declarations and the override functions that ESPHOME uses to run code that would be needed in a void loop() function if you were using this from the Arduino IDE.
 
   When you replace the WAV sound with your own, remember to change the length
   i.e.  4608 to match the lengh of your WAV  e.g.:
   
   
   const unsigned char PROGMEM ErrorWav[4608] = {
   
     0x52, 0x49, 0x46, 0x46, 0xF8, 0x11, 0x00, 0x00, 0x57, 0x41, 0x56, 0x45,
     
     ...
     
   };
 
 
4) In esphome create a new device and paste in the example esp-wav-player.yaml code

    Update the passwords to match your configurtion
    
    Compile and upload

5) You will get a switch that when activated will play the defined WAV.  The WAV only plays when the switch is turned on.  Nothing is defined when the switch turns off.
  
I use an Adafruit PAM8302 to interface to the speaker for added volume  

My configuration uses an ESP32 WROOM DEV board.  Pinout connections as follows:

  GPIO25 -> A+ on the PAM8302
  
  GND    -> A- on the PAM8302


--------------
sound folder
--------------
The sound folder has the StartUp-sound.WAV file that I used in the example, included here so you can hear what this project will play if you are successful.  You do not include the /sound folder in the ESPHome folder.

The .c file which shows the hex code was created by loading the wav file in the HDX editor ( https://mh-nexus.de/en/hxd/ ) and saving the file as a .c file. 
