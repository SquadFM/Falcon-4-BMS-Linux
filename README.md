Notes:
- [Click here](#falcon-4-bms-on-linux-with-wine-and-lutris-tested-with-bms-437) for Wine/Lutris installation instructions (e.g. for the GOG version of Falcon 4.0)
- Replace home/x/ with your home directory in the instructions below



# Falcon 4 BMS on Linux with Steam (tested with BMS 4.37)


## Install required software
- Steam
- wine-staging (recommended)
- winetricks
- optional: opentrack

## Installation
- Install Falcon 4.0 on Steam
- In Steam, right click on Falcon 4.0 > Properties > Compatibility > enable "Force use of a specific Steam Play compatibility tool" > select Proton 7.0-6 (older/newer Proton versions should work too)
- Run Falcon 4.0 once, then exit the game (this creates the folder /home/x/.local/share/Steam/steamapps/compatdata/429530)
- Install winetricks (don't use protontricks as it has issues with dotnet installation)
- Run winetricks on prefix:

`WINEPREFIX="/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx" winetricks -q`
- Optional: should winetricks be out of date, run: sudo winetricks --self-update
  - check the updated winetricks version with: winetricks --version
  - if you need to rollback winetricks to the old version from your repository, run: sudo winetricks --update-rollback
- In winetricks > select the default wineprefix > Install a Windows DLL or component > select the following
  - dotnet48 (this will automatically install dotnet40 too)
  - vcrun2015
- Ignore any error notifications during installation (they are automatically skipped after a few seconds; no need to press "OK")
- Once the installation is finished you can close the winetricks window(s)
- Download BMS installer and updates from https://www.falcon-bms.com/downloads/ (use qBittorrent as other torrent apps have had issues with the download in the past)
- Install BMS from your ~/Download folder; Run in terminal: 

`
WINEPREFIX="/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx" wine "/home/x/Downloads/Falcon BMS_4.37_Full_Setup.exe"
`
- Wait for the installation to finish
- Optional: make a backup of the game folder if something breaks in the future: /home/x/.local/share/Steam/steamapps/compatdata/429530

## Run BMS
- Find the path to the Proton executable you want to use, e.g.: 
/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton

- Run BMS with included Alternative Launcher:

`STEAM_COMPAT_DATA_PATH="/home/x/.local/share/Steam/steamapps/compatdata/429530/" STEAM_COMPAT_CLIENT_INSTALL_PATH="/home/x/.local/share/Steam/" "/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton" run "/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/Falcon BMS 4.37/Launcher/FalconBMS_Alternative_Launcher.exe"`

- Run BMS with standard launcher:

`STEAM_COMPAT_DATA_PATH="/home/x/.local/share/Steam/steamapps/compatdata/429530/" STEAM_COMPAT_CLIENT_INSTALL_PATH="/home/x/.local/share/Steam/" "/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton" run "/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/Falcon BMS 4.37/Launcher.exe"`

- Tip: copy-paste either command in a file like falconbmslauncher.sh and set it to be an executable file (usually right-click on file > Permissions > enable "Allow this file to run as a program"). Move the file to your Desktop and you can doubleclick it to start BMS. 


## Opentrack Headtracking
- Install opentrack
- Add user to input group (x = yourusername)

`sudo usermod -a -G input x`

- Restart computer (or logout and then login again)
- In Opentrack:
  - Input: PointTracker
  - Output: Wine
    - Wine variant: Proton (select Proton version that Falcon 4.0 is using in Steam, e.g. Proton 7.0)
    - select FSYNC (not ESYNC)
    - Protocol: Both
    - Steam application id: 429530
    - confirm with "OK"
  - Filter: Accela
  - Options > Game Detection:
    - Executable: Falcon BMS.exe
    - Profile: select your opentrack profile for BMS
- In BMS > Setup > Controllers > Advanced:
  - Enable Natural Head: yes
  - Enable 3d Cockpit TrackIR: yes
  - Enable TrackIR Vector: yes
  - TrackIR Vector Z Axis Mode: FOV Control
- Start Opentrack first, and then BMS
- Alt + c, t = restarts TrackIR BMS module (usually not needed, just FYI)

## Weapon Delivery Planner
- This app can NOT be started from the Alternative Launcher and therefore requires a separate command to run
- Download WDP from 
http://www.weapondeliveryplanner.nl/download/index.html
- Unpack archive and copy folder to 
/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/
- The drive_c folder will therefore contain (under /home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/):
  - Falcon BMS 4.37/
  - Weapon_Delivery_Planner_3.7.24.232/
  - various other windows folders (e.g. ProgramData, Program Files, windows, etc.)
- To start WDP, run

`STEAM_COMPAT_DATA_PATH="/home/x/.local/share/Steam/steamapps/compatdata/429530/" STEAM_COMPAT_CLIENT_INSTALL_PATH="/home/x/.local/share/Steam/" "/home/x/.local/share/Steam/steamapps/common/Proton 7.0/proton" run "/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx/drive_c/Weapon_Delivery_Planner_3.7.24.232/WeaponDeliveryPlanner.exe"`
- ** you'll most likely see a rundll32.exe error message popup which you can ignore, click cancel (it should only show once)
- The WDP starts with a popup that reads "Theatre 'Aegean' not found in your BMS install" - which you can also ignore, click "OK" - once WDP opens you can select "Korea" from the drop down menu in the upper left (under "File")
- ** while using WDP it may happen that you see an error message popup that shows "Unhandled exception has occured in your application" - just click on "Continue" to dismiss 

## Avionics Configurator
- This program only shows a black window. To show it properly run the following command in your terminal:
 
`WINEPREFIX="/home/x/.local/share/Steam/steamapps/compatdata/429530/pfx" wine reg add "HKCU\\SOFTWARE\\Microsoft\\Avalon.Graphics" /v DisableHWAcceleration /t REG_DWORD /d 1 /f`

** if you have an idea how to fix these issues please let me know and I can add it to the guide




### _____________________________________________________________

# Falcon 4 BMS on Linux with Wine and Lutris (tested with BMS 4.37)

## Install required software
- Lutris
- wine-staging (recommended)
- winetricks
- optional: opentrack

## Lutris: Create wine prefix and install Falcon 4.0
- Start Lutris and click on + sign in upper left ("Add Game") > "Install a Windows game from media"
- Game name: "Falcon 4.0" > click "Continue"
- Select setup file: click on "Install" > specify installation directory (e.g. /home/x/Games/FalconBMS)
- Click "Install" > click on "Browse" and select your Falcon 4.0 installer (e.g. from GOG)
- Click on "Continue" and follow the instructions in the Falcon 4.0 installer 
- Once the Falcon 4.0 installation is complete, Lutris will create a launcher with the name we used earlier ("Falcon 4.0")
- Right click on the launcher > Configure > Runner options > Wine version > select "System (8.5 Staging))" > Save (this requires wine-staging to be installed on your computer - older/newer system wine versions should work too)


## Install required libraries into Falcon wine prefix
- Run winetricks on prefix:

`WINEPREFIX="/home/x/Games/FalconBMS" winetricks -q`

- Optional: should winetricks be out of date, run: sudo winetricks --self-update
  - Check the updated winetricks version with: winetricks --version
  - If you need to rollback winetricks to the old version from your repository, run: sudo winetricks --update-rollback
- In winetricks > select the default wineprefix > Install a Windows DLL or component > select the following
  - dotnet48 (this will automatically install dotnet40 too)
  - vcrun2015
- Wait for winetricks to install all libraries (any winetricks pop-ups are normal and will automatically be skipped after a few seconds) and once done, close the winetricks window


## Lutris: Install Falcon BMS
- Now we're going to install Falcon BMS into the same prefix
- In Lutris > right click on "Falcon 4.0" launcher > duplicate
- Right click on the new launcher (should have a "2" at the end of its name) > Configure > Game info > set name to: "Falcon BMS"
- In the same window go to "Game options" > "Executable" > "Browse" and select Falcon BMS installer .exe file > click on "Save"
- Start "Falcon BMS" launcher (or right click > "Play") > follow BMS installer instructions (install DirectX too)
- Wait for the BMS installation to finish
- Right click the "Falcon BMS" launcher > "Configure" > "Game options" > Executable > select Falcon BMS Alternative Launcher.exe which should be under "/home/x/Games/FalconBMS/drive_c/Falcon BMS 4.37/Launcher/FalconBMS_Alternative_Launcher.exe"
- Double-click the "Falcon BMS" launcher to start Falcon BMS


## Opentrack Headtracking
- Add user to input group (x = your username)

`sudo usermod -a -G input x`
- Restart computer (or logout and login again)
- In Opentrack:
  - Input: PointTracker
  - Output: Wine
    - Wine variant: Wine (system): /home/x/Games/FalconBMS/
    - select ESYNC (not FSYNC)
    - Protocol: Both
    - confirm with "OK"
  - Filter: Accela
  - Options > Game Detection:
    - Executable: Falcon BMS.exe
    - Profile: select your opentrack profile for BMS
- In BMS > Setup > Controllers > Advanced:
  - Enable Natural Head: yes
  - Enable 3d Cockpit TrackIR: yes
  - Enable TrackIR Vector: yes
  - TrackIR Vector Z Axis Mode: FOV Control
- Always start Opentrack first, and then BMS
- Alt + c, t = restarts TrackIR BMS module (usually not needed, just FYI)


## Weapon Delivery Planner
- This app can NOT be started from the Alternative Launcher, therefore we'll create a launcher in Lutris
- To run WDP go back to Lutris
- In Lutris > right click on "Falcon BMS" launcher > duplicate
- Right click on the new launcher (should have a "2" in the end of its name) > Configure > Game info > set name to: "Falcon BMS WDP"
- Download WDP from 
http://www.weapondeliveryplanner.nl/download/index.html
- Unpack archive and copy unzipped folder to 
/home/x/Games/FalconBMS/drive_c/
- The path should look like: /home/x/Games/FalconBMS/drive_c/Weapon_Delivery_Planner_3.7.24.232/
- In Lutris right-click on "Falcon BMS WDP" > "Configure" > "Game options" > "Executable" > "Browse" and select the WDP .exe file, path should look similar to the one below:

/home/x/Games/FalconBMS/drive_c/Weapon_Delivery_Planner_3.7.24.232/WeaponDeliveryPlanner.exe
- Click "Save"
- If see a rundll32.exe error message popup you can ignore it, just click cancel or no (it should only show once)
- The WDP starts with a popup that reads "Theatre 'Aegean' not found in your BMS install" - which you can also ignore, click "OK" - once WDP opens you can select "Korea" from the drop down menu in the upper left (under "File")
- While using WDP it may happen that you see an error message popup that shows "Unhandled exception has occured in your application" - just click on "Continue" to dismiss 


## Avionics Configurator - Prevent black window
- This app can be started from the Alternative Launcher
- This program only shows a black window. To show it properly run the following command in your terminal:

`WINEPREFIX="/home/x/Games/FalconBMS" wine reg add "HKCU\\SOFTWARE\\Microsoft\\Avalon.Graphics" /v DisableHWAcceleration /t REG_DWORD /d 1 /f`
