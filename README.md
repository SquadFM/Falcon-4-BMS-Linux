# Falcon 4 BMS on Linux (tested with BMS 4.37)


## Installation
- Install Falcon 4.0 on Steam
- In Steam, right click on Falcon 4.0 > Properties > Compatibility > enable "Force use of a specific Steam Play compatibility tool" > select Proton 7.0-6 (older/newer Proton versions should work too)
- Run Falcon 4.0 once, then exit the game (this creates the folder /home/x/.local/share/Steam/steamapps/compatdata/429530)
- Download BMS installer and updates from https://www.falcon-bms.com/downloads/ (use qBittorrent as other torrent apps have had issues with the download in the past)
- Install BMS from your ~/Download folder; Run in terminal: 

`
WINEPREFIX="/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx" wine "/home/x/Downloads/Falcon BMS_4.37_Full_Setup.exe"
`
- wait for the installation to finish
- optional: make a backup of the game folder if something breaks in the future: /home/x/.local/share/Steam/steamapps/compatdata/429530

## Run BMS
- Find the path to the Proton executable you want to use, e.g.: 
/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton

- run BMS with included Alternative Launcher:

`STEAM_COMPAT_DATA_PATH="/home/x/.local/share/Steam/steamapps/compatdata/429530/" STEAM_COMPAT_CLIENT_INSTALL_PATH="/home/x/.local/share/Steam/" "/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton" run "/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/Falcon BMS 4.37/Launcher/FalconBMS_Alternative_Launcher.exe"`

- Run BMS with standard launcher:

`STEAM_COMPAT_DATA_PATH="/home/x/.local/share/Steam/steamapps/compatdata/429530/" STEAM_COMPAT_CLIENT_INSTALL_PATH="/home/x/.local/share/Steam/" "/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton" run "/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/Falcon BMS 4.37/Launcher.exe"`

- Tip: copy-paste either command in a file like falconbmslauncher.sh and set it to be an executable file (usually right-click on file > Permissions > enable "Allow this file to run as a program"). Move the file to your Desktop and you can doubleclick it to start BMS. 


## Opentrack Headtracking
- install opentrack
- in Steam > Falcon 4.0 > Properties > Launch Options:

`WINEDEBUG=+plugplay PROTON_LOG=1 %command% -nomovie`

- add user to input group (x = yourusername)

`sudo usermod -a -G input x`

- restart computer
- in Opentrack:
  - Input: PointTracker
  - Output: Wine
    - Wine (system): /home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/
    - Wine variant (select this one, not "Wine (system)"): Proton (select Proton version that Falcon 4.0 is using in Steam, e.g. Proton 7.0)
    - select FSYNC (not ESYNC)
    - Protocol: Both
    - Steam application id: 429530
    - confirm with "OK"
  - Filter: Accela
  - Options > Game Detection:
    - Executable: Falcon BMS.exe
    - Profile: select your opentrack profile for BMS
- in BMS > Setup > Controllers > Advanced:
  - Enable Natural Head: yes
  - Enable 3d Cockpit TrackIR: yes
  - Enable TrackIR Vector: yes
  - TrackIR Vector Z Axis Mode: FOV Control
- always start Opentrack first, and then BMS
- Alt + c, t = restarts TrackIR BMS module (usually not needed, just FYI)

