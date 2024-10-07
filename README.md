# ARMA 3 CONFIGURATION GUIDE  

## CLIENT  
-----------------------------
### Arma 3 Performance Tuning:  

Benchmark: https://steamcommunity.com/sharedfiles/filedetails/?id=375092418

1- Go to Steam > Settings > In-Game, tick In-game FPS counter, tick high contrast colour.

2- Go to C:\Users\[your_username]\Documents\Arma 3. Open Arma3.cfg with text editor, If you have monitor with refresh rate above 60Hz, set refresh to your refresh rate (for example: refresh=144;). Save changes and close file.  
**Optional, not recommended**, for reducing display lag to 1 frame (at the expense of lower median fps and more framespikes), set "GPU_MaxFramesAhead=1" and "GPU_DetectedFramesAhead=1" (Nvidia Control Panel call it "Low Latency Mode", more info here: https://blurbusters.com/gsync/gsync101-input-lag-tests-and-settings/14/#mprf-101).

3- Go to C:\Users\[your_username]\Documents\Arma 3. Open [your_username].Arma3Profile with text editor, set "mouseSmoothing=0" and "mouseAcceleration=0". This will give you direct raw mouse control, instead of the smoothed filtered movement. Save changes and close file.

-Open Steam, select ARMA 3, Properties (right mouse button on ARMA 3 in library), go to BETA tab, select "profiling - Performance Profiling Build". (IMPORTANT: When new arma version comes out you will need to switch back to default branch from performance one (select "default" instead of "profiling") or otherwise game will crash).

-Start ARMA 3 Launcher, open Options (upper right corner), select Launcher Options, set "Action after game start" to "Close Launcher after clicking Play".

-Start ARMA 3 Launcher, select PARAMETERS and go to ALL PARAMETERS tab. Set "Platform" to "64-bit", tick "Show static background in menu", tick "Skip logos at startup", Set "Memory allocator (64-bit)" to "Intel TBB 4 allocator - 64 bit", tick "Enable Large-page Support", tick "No Logs", set "World" to "empty", tick "No Pause", tick "No Pause Audio".

-Start Process Lasso (https://bitsum.com), start ARMA 3 (game, not launcher). In Process Lasso, click with right mouse button on "arma3_64x.exe" -> CPU Priority -> Always -> High. Click with right mouse button on "arma3_64x.exe" process -> CPU affinity -> Always -> Untick CPU 0.


-"Bitsum Highest Performance Mode" es mejor que "ultimate performance mode.
I just realized something -- in the "Bitsum Highest Performance" plan, the setting "USB Selective Suspend" is enabled, 



Windows 11 DVR - LWin+G
Click Windows Start, execute regedit.exe as admin, 
HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\GameDVR and change "AppCaptureEnabled" from 1 to 0.
HKEY_CURRENT_USER\System\GameConfigStore and change "GameDVR_Enabled" from 1 to 0.

-Disable Cortana. Windows Settings, Apps, Installed Apps, search Cortana, Advanced options, "Never" Let this app run in background.
-Uninstall "Cortana", "News", "Start Experiences App", "Power Automate", "Weather", "Clipchamp", "365 (Office)", "Widgets Platform Runtime", "Quick assist", "Feedback Hub", "Snipping tool", "Sticky notes", "Web Search from Microsoft Bing", "Microsoft To Do", "People, "Maps", "OneDrive", "Movies & TV", "Phone Link", "Tips"

Game mode ON
Game Bar - Allow controller to open game bar

meter lo del nvidia panel

y la gestion de energia

-----------------------------
### Starting parameters:  

"D:\Steam\steamapps\common\Arma 3\arma3_x64.exe" -skipIntro -noSplash -hugePages -noLogs -world=empty -noPause -noPauseAudio -malloc=tbb4malloc_bi_x64 -setThreadCharacteristics


--------------------------------------------------------------------------  
SERVER NETWORK CONFIG:  

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

--------------------------------------------------------------------------
ARMA SERVER MONITOR:
https://github.com/dayz9998jp/ASM

https://forums.bohemia.net/forums/topic/229229-server-administration-guides-tutorials-compilation-list/


--------------------------------------------------------------------------


-SERVER
-----------------------------
"D:\Steam\steamapps\common\Arma 3\arma3server_x64.exe" "-profiles=D:\Steam\steamapps\common\Arma 3\MyArmaServer" "-config=D:\Steam\steamapps\common\Arma 3\MyArmaServer\server.cfg" "-cfg=D:\Steam\steamapps\common\Arma 3\MyArmaServer\basic.cfg" -mod="@xxx;@yyy" -name=myserver -world=empty -port=2302 -hugePages

// -enableHT - Prioritizes the use of HT cores for threads with minor tasks/micro jobs.  
// -autoInit - This will break the Arma_3_Mission_Parameters function, so do not use it when you work with mission parameters.  
// -netlog - Enables multiplayer network traffic logging.  
// -serverMod= - Loads the specified sub-folders for different server-side (not broadcasted to clients) mods.  
// -filePatching - Add only if needed, like if using "userconfig/cba_settings.sqf"  
// -battleyeLicense=1 ?????borrar???  
// -ranking="D:\Steam\steamapps\common\Arma 3\MyArmaServer\ranking.log"  
// -loadMissionToMemory - Server will load mission into memory on first client downloading it. Then it keeps it pre-processed pre-cached in memory for next clients, saving some server CPU cycles.  
// -bandwidthAlg=2 - Uses a new experimental networking algorithm that might be better than the default one.  
// -limitFPS=300 - Start parameter to adjust server FPS limit between 5-1000 FPS (default 50).  

Comparar el server con el client y homogeneizar  

Ver si es lo mismo que el "mp statistics.log"  
Lo mismo con el RPT  
Lo mismo con el Console Logfile  


-HEADLESS CLIENT
-----------------------------
"D:\Steam\steamapps\common\Arma 3\arma3server_x64.exe" -client -connect=127.0.0.1 -nosound -port=2302 -password=1234 -nologs -world=empty -enableHT -name=HC -profile=HC -mod="xxx"


NITRADO LINEA:
== "C:\SERVICES\ni4816181_1_SHARE\ftproot\arma3\arma3server_x64.exe" -mod="@ace;@CBA_A3;@Enhanced Movement;@Enhanced Movement Rework;@RHSAFRF;@RHSGREF;@RHSSAF;@RHSUSAF;@Task Force Arrowhead Radio BETA;@Advanced Sling Loading;@Immersion Cigs;@Zeus Enhanced;@Fawks' Enhanced NVGs;@ILBE Assault Pack - Rewrite;@ACSTG AI Cannot See Through Grass;" -serverMod="" -ip=46.251.234.146 -port=18000 -maxmem=2048 -hugePages -enableHT -malloc=tbb4malloc_bi -profiles=config -config=config/server.cfg -cfg=config/basic.cfg -name=arma3 -loadMissionToMemory



PDTE GENERAR LAS LINEAS DE ARRANQUE DE LOS AUTOBATS PARA SERVER Y EL HC  
https://community.bistudio.com/wiki/Arma_3:_Startup_Parameters  

5-Crear el .bat de arranque con:  

D:\Games\Arma3\A3Master\Users\Adminstrator\Administrator.Arma3Profile  
D:\Games\Arma3\A3Master\Users\Administrator\Arma3.cfg  


--------------------------------------------------------------------------
FILE LOCATIONS

D:\Games\Arma3\A3Master\Users\Administrator\Administrator.Arma3Profile (Difficulty settings)  
D:\Games\Arma3\A3Master\Users\Administrator\Administrator.vars.Arma3Profile (Some binarised content which you cannot edit)  
D:\Games\Arma3\A3Master\Users\Administrator\Arma3.cfg (Bandwidth settings)  
D:\Games\Arma3\A3Master\MPMissions\ (This is where custom made mission.pbo's need to be placed)  
D:\Games\Arma3\A3Master\arma3.rpt (Debug Log, automatically created every time the arma3server.exe is started)  
D:\Games\Arma3\A3Master\CONFIG_server.cfg (Manually created)  
D:\Games\Arma3\A3Files\Arma3server_steamcmd_example.cmd (Manually created)  
D:\Apps\Steam\  

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
