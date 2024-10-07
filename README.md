# ARMA 3 CONFIGURATION GUIDE  

## CLIENT  

### Arma 3 Client Performance Tuning:  
All below settings are optional, but they will provide better performance or improve usage characteristics for Arma 3. Those settings are set for Windows 11 and a fairly new high performance computer, with a good CPU and GPU (Nvidia), and at least 16Gb of RAM.

1- Go to Steam > Settings > In-Game, tick In-game FPS counter, tick high contrast colour. Optional FPS counter to aid in tunning settings.

2- Go to C:\Users\[your_username]\Documents\Arma 3. Open Arma3.cfg with text editor, If you have monitor with refresh rate above 60Hz, set refresh to your refresh rate (for example: refresh=144;). Save changes and close file.  
**Optional, not recommended**, for reducing display lag to 1 frame (at the expense of lower median fps and more framespikes), set "GPU_MaxFramesAhead=1" and "GPU_DetectedFramesAhead=1" (Nvidia Control Panel call it "Low Latency Mode", more info here: https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/#mprf-101).  

3- Go to C:\Users\[your_username]\Documents\Arma 3. Open [your_username].Arma3Profile with text editor, set "mouseSmoothing=0" and "mouseAcceleration=0". This will give you direct raw mouse control, instead of the smoothed filtered movement. Save changes and close file.  

4- Open Steam, select ARMA 3, Properties (right mouse button on ARMA 3 in library), go to BETA tab, select "profiling - Performance Profiling Build". This "performance" branch will give you some more fps, but if stability is paramount to you, just stick with the normal branch.  

5- Open ARMA 3 Launcher, go to Options (upper right corner), select Launcher Options, set "Action after game start" to "Close Launcher after clicking Play".  

6- Start ARMA 3 Launcher, select PARAMETERS and go to ALL PARAMETERS tab. Set "Platform" to "64-bit", tick "Show static background in menu", tick "Skip logos at startup", Set "Memory allocator (64-bit)" to "Intel TBB 4 allocator - 64 bit" (the default one, just to be sure), tick "Enable Large-page Support", tick "No Logs", set "World" to "empty", tick "No Pause", tick "No Pause Audio".  

7- Install and open "Process Lasso" (https://bitsum.com), start ARMA 3 (the game, not just the launcher). In Process Lasso, click with right mouse button on "arma3_64x.exe" -> CPU Priority -> Always -> High. Click with right mouse button on "arma3_64x.exe" process -> CPU affinity -> Always -> Untick CPU 0. This will give Arma 3 priority above other system processes, and avoid it from using the first core which is usually very busy with system dutties.  

8- In "Process Lasso", go to Main, Active Power Profile, and select "Bitsum Highest Performance". Go to Options, Power, Start Process Lasso with Power Profile" and select "Bitsum Highest Performance". This will set Windows energy management to avoid CPU throttling.  

9- Click Windows Start, execute regedit.exe (right click, as administrator), go to "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\GameDVR" and change "AppCaptureEnabled" from 1 to 0. Go to "HKEY_CURRENT_USER\System\GameConfigStore" and change "GameDVR_Enabled" from 1 to 0. This will disable Windows 11 DVR if it is not needed.  

10- Optional, uninstall any uneeded applications that comes with Windows from "Add or remove programs": "Cortana", "News", "Start Experiences App", "Power Automate", "Weather", "Clipchamp", "365 (Office)", "Widgets Platform Runtime", "Quick assist", "Feedback Hub", "Snipping tool", "Sticky notes", "Web Search from Microsoft Bing", "Microsoft To Do", "People, "Maps", "OneDrive", "Movies & TV", "Phone Link" and "Tips".  

11- Open Windows' settings "Gaming", then "Game Mode settings" and make sure it is ON.   

12- Open Windows' settings "Gaming", then "Game Bar", then "Allow your controller to open Game Bar" to OFF.  

13- Right click on the Desktop, click Display settings, click Graphics, click on Arma 3, click Options and set "High Performance". Click on "Default graphics settings" and set to ON the three settings.

14- If you have a G-SYNC monitor, set "Max Frame Rate" to 3 frames below the maximum (with a 144hz monitor, use 141Hz), and set "Monitor Technology" to G-SYNC Compatible.  

15- If you have an Nvidia GPU, open the Nvidia Control Panel, go to 3D Settings, Manage 3D Settings, Program Settings, and add "arma3_x64.exe". Set "Anisotropic filtering" to 16x, "Vertical Sync" to On, "Power Management Mode" to High Performance, "Shader Cache Size" to 10 Gb and "Texture filtering - Quality" to High quality. Then go to Display, Set-up G-SYNC, tick "Enable G-SYNC", tick "Enable for windowed and full screen mode", select your display and tick "Enable settings for the selected display model". Make sure you activate G-SYNC/Freesync on your monitor buttons menu.  

16- Press Start button, search "Core Isolation", set "Memory integrity" to OFF.

17- Press Start button, search "Mouse Settings", click on "Additional mouse settings", go to Pointer Options tab and untick Enhance pointer position.

18- Press Start button, search "Sticky keys", and put all the settings to OFF.

19- Restart the computer.  

20- Run Arma 3, go to Options, Video Options and click the button "AUTODETECT". Go to tab Display, set Display mode to "Fullscreen", set your resolution, set your aspect ratio, set "VSYNC" to Disabled. This is your base configuration, if you want now you can fine tune the settings on the "General" tab and the "AA & PP" tab to your liking. You can see here if a setting is more CPU or GPU dependant:
https://community.bistudio.com/wiki/Arma_3:_Performance_Optimisation

21- Optional. This is the gold standard benchmark for testing Arma performance settings, if needed:
Benchmark: https://steamcommunity.com/sharedfiles/filedetails/?id=375092418  

-----------------------------
### Arma 3 Client Launch Parameters:  

"D:\Steam\steamapps\common\Arma 3\arma3_x64.exe" -skipIntro -enableHT -noSplash -hugePages -noLogs -world=empty -noPause -noPauseAudio -malloc=tbb4malloc_bi_x64 -setThreadCharacteristics

-----------------------------

## SERVER 

### Arma 3 Server Network Configuration:  

1- Add on Window's Firewall the rules for the application "arma3server_x64.exe", and allow it both on "Private" and "Public" networks.

2- On Windows' Firewall Advanced Settings, look for the two rules of "arma3server_x64.exe", and enable on both of them the setting "Allow edge traversal".  

3- Set the ICMP "echo reply" as allowed so the server is able return ping delay properly (https://manage.accuwebhosting.com/knowledgebase/2609/How-to-Allow-Pingor-ICMP-Echo-Request-in-Windows-Firewall.html)  

4- NAT forward those six ports on both TCP and UDP. uPnP could be used instead, but it is better to NAT them:
2302 (default Arma 3 Game port) + (VON is now part of main gameport due to NAT issues)  
2303 (STEAM query, +1)  
2304 (Steam port, +2)  
2305 (VON port, +3 - not used atm. but allocated)  
2306 (BattlEye traffic, +4)  
27015 (STEAM Rcon port of SRCDS with TCP, and game's traffic with UDP)  

-----------------------------
### Arma 3 Server Launch Parameters:  

"D:\Steam\steamapps\common\Arma 3\arma3server_x64.exe" "-profiles=D:\Steam\steamapps\common\Arma 3\MyArmaServer" "-config=D:\Steam\steamapps\common\Arma 3\MyArmaServer\server.cfg" "-cfg=D:\Steam\steamapps\common\Arma 3\MyArmaServer\basic.cfg" -mod="@xxx;@yyy" -name=myserver -port=2302 -world=empty -hugePages -noLogs -malloc=tbb4malloc_bi_x64 -skipIntro -enableHT -noSplash -noPause -noPauseAudio -loadMissionToMemory -limitFPS=144

// -enableHT - Prioritizes the use of HT cores for threads with minor tasks/micro jobs.  
// -autoInit - This will break the Arma_3_Mission_Parameters function, so do not use it when you work with mission parameters.  
// -netlog - Enables multiplayer network traffic logging.  
// -serverMod= - Loads the specified sub-folders for different server-side (not broadcasted to clients) mods.  
// -filePatching - Add only if needed, like if using "userconfig/cba_settings.sqf"  
// -ranking="D:\Steam\steamapps\common\Arma 3\MyArmaServer\ranking.log"  
// -loadMissionToMemory - Server will load mission into memory on first client downloading it. Then it keeps it pre-processed pre-cached in memory for next clients, saving some server CPU cycles.  
// -bandwidthAlg=2 - Uses a new experimental networking algorithm that might be better than the default one. Seems to be better without it.  
// -limitFPS=300 - Start parameter to adjust server FPS limit between 5-1000 FPS (default 50). 

-----------------------------
### Arma 3 Server Headless Client:  

"D:\Steam\steamapps\common\Arma 3\arma3server_x64.exe" -client -connect=127.0.0.1 -skipIntro -noSplash -hugePages -nosound -port=2302 -noPause -password=1234 -malloc=tbb4malloc_bi_x64 -nologs -world=empty -enableHT -name=HC -profile=HC -mod="xxx" 

-----------------------------
REVISAR CUANDO ESTE MONTADO LAS RUTAS, SI SON CORRECTAS, LAS DE LOS PERFILES SOBRETODO:

### File Locations:  

D:\Steam\steamapps\common\Arma 3\MyArmaServer\myserver.Arma3Profile (Difficulty settings)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\myserver.vars.Arma3Profile (Some binarised content which you cannot edit)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\basic.cfg (Bandwidth settings)  
D:\Steam\steamapps\common\Arma 3\MPMissions\ (This is where custom made mission.pbo's need to be placed)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\arma3.rpt (Debug Log, automatically created every time the arma3server.exe is started)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\server.cfg (Manually created)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\StartServer.bat (Manually created)  
D:\Steam\steamapps\common\Arma 3\MyArmaServer\StartHC.bat (Manually created)  

--------------------------------------------------------------------------
SERVER ADMIN COMMANDS

you can use the admin command #monitor

https://community.bistudio.com/wiki/Multiplayer_Server_Commands

SERVER MANAGEMENT

    #login <password> : Admin login
    #logout : Admin logout
    #lock : Lock server (Auto unlocks at end of mission)
    #unlock : Unlocks server
    #missions : Stops mission, reloads mission list
	#mission <filename> <difficulty> : Select mission to load. Parameter difficulty is optional
    #reassign : Moves all players from their unit selection slots back into the lobby
    #restart : Returns the mission to the unit selection screen, with all players in their slots and restarts the mission
	#restartserver : Shuts down and restarts the server immediately 
	#restartserveraftermission : Shuts down and restarts the server after mission ends
    #shutdown : Shuts the server down
	#shutdownaftermission : Shuts down the server after mission ends
    #Init : Reloads file defined by -config command line parameter


PLAYER MANAGEMENT

    #userlist : Displays the list of users on the server (use pgup to scroll up)
    #kick <Server Player ID> (First entry for a player using #userlist)
    #kick <nickName> (Second entry for a player using #userlist
    #kick <Player UID> (Third entry for a player using #userlist)

    #exec kick <Server Player ID> (First entry for a player using #userlist)
    #exec kick <nickName> (Second entry for a player using #userlist
    #exec kick <Player UID> (Third entry for a player using #userlist)

    #exec ban <Server Player ID> (First entry for a player using #userlist)
    #exec ban <nickName> (Second entry for a player using #userlist
    #exec ban <Player UID> (Third entry for a player using #userlist)
	
	#beclient <players> : Displays the list of GUID's of all players on the server.
	#beclient <guid> : Show your own GUID.


DEBUGGING

    #monitor 10 : Activates the server monitor which reports Bandwidth and memory useage Every * seconds via chat window)
	#monitords : Shows performance information in the dedicated server console. Interval 0 means to stop monitoring. 
    #monitor 0 : Deactivates the server monitor
    #debug off : Deactivates debugging
    #debug 30 : Debug reporting interval (Default is 10 seconds
    #debug von
    #debug console
    #debug checkFile expansion\Dta\ui.pbo
    #debug userSent <username>
    #debug userInfo <username>
    #debug userQueue <username>
    #debug JIPQueue <username>
    #debug totalSent 10 
	
	
	
--------------------------------------------------------------------------






More information at: https://community.bistudio.com/wiki/Arma_3:_Basic_Server_Config_File  
More information at: https://community.bistudio.com/wiki/Arma_3:_Performance_Optimisation  
More information at: https://community.bistudio.com/wiki/Arma_3:_Server_Side_Scripting  
More information at: https://community.bistudio.com/wiki/Multiplayer_Server_Commands  
More information at: https://community.bistudio.com/wiki/Arma_3:_Difficulty_Settings  
More information at: https://community.bistudio.com/wiki/Arma_3:_Startup_Parameters  
More information at: https://community.bistudio.com/wiki/Arma_3:_Server_Config_File  
More information at: https://community.bistudio.com/wiki/Arma_3:_MP_Mission_Names  
More information at: https://community.bistudio.com/wiki/Arma_3:_Dedicated_Server  
More information at: https://community.bistudio.com/wiki/Arma_3:_STEAMWORKSquery  
More information at: https://community.bistudio.com/wiki/Arma_3:_Headless_Client  
More information at: https://community.bistudio.com/wiki/Arma_3:_Server_Profile  
More information at: https://community.bistudio.com/wiki/Arma_3:_Mission_Voting  
More information at: https://community.bistudio.com/wiki/Biki_Export_Scripts  
More information at: https://community.bistudio.com/wiki/server.armaprofile  
More information at: https://community.bistudio.com/wiki/Description.ext  
More information at: https://community.bistudio.com/wiki/BattlEye  
