# Overview
Greetings Stranger! I'm not surprised to see your kind here.<br>
This is a free tool I made for loading multiple Diablo 2 Resurrected instances (AKA Multiboxing/Multiboxes). 
Instead of setting up shortcuts on your desktop for each account (or worse, opening the game from the battlenet client with multiple game installs) and then manually using ProcExp to kill the "Check for other instances" handle, run this one script instead and keep it open to easily switch realms for trades/dclones etc.
Oh yea, and no more plain text passwords either. Cool aye?

Script Screenshot:<br>
![Launcher](https://user-images.githubusercontent.com/63577525/233829526-2b28f2b9-761b-4d95-af0f-6561bda8ddf3.png)<br>
What your windows will look like:<br>
![GameWindows](https://user-images.githubusercontent.com/63577525/233829532-f81afad2-4806-4d6a-bb9e-817c25758346.png)

## But what does it do?
Script will allow opening multiple Diablo 2 resurrected instances and will automatically close the 'DiabloII Check For Other Instances' handle.<br>
It will achieve this by importing account details from a CSV that you populate and essentially launches the game the same way you would with a shortcut by passing account, password and region arguments to D2r.exe.<br>
	Note: Plain text passwords entered into the CSV will be convered into a secure string after running. If you don't want to enter plain text passwords EVER then you can leave the PW field in the CSV blank and manually type in when running the script.<br>
Once the game has initialised, the window will be renamed so it's easier to tell which game is which.<br>
This also helps the script know which games are open to prevent you accidentally opening a game with the same account twice.<br>
Optionally you can also have the game launch using custom settings.json for each account in case you want different graphics/audio/game settings for each account you have.

Note: If for some unknown reason you prefer to, you can call the script with account, password & region parameters: -account username@emailaddress.com -pw MyBNetAccountPassword -region na.actual.battle.net

# Setup Steps
## Download
1. Download the latest [release](https://github.com/shupershuff/Diablo2RLoader/releases) this and extract the zip file to a folder of your choosing.
2. Right click on D2loader.ps1 and open properties.
3. Check the "Unblock" box and click apply.<br>
![image](https://user-images.githubusercontent.com/63577525/234503557-22b7b8d4-0389-48fa-8ff4-f8a7870ccd82.png)


## Setup Handle viewer
1. Download handle viewer from https://learn.microsoft.com/en-gb/sysinternals/downloads/handle
2. Extract the executable files (specifically handle64.exe) to the .\Handle\ folder

## Setup Your Accounts
1. Open Accounts.csv in a text editor or excel.
2. Add number for each account starting from 1.
3. Add your account sign in address
4. Add your account password. This will be converted to an encrypted string after first run. If left empty, you will be prompted to enter it when running script and the encrypted password string will be added to the csv.
5. Add a 'friendly' name for each account, this will appear in your diablo window. You can put anything here, I just added my Bnet usernames.

If opening in Excel you add this info in each column. Otherwise open and edit in notepad.

## Run the script manually for the first time
1. Browse to the folder, right click on D2Loader.ps1 and choose run.
2. If you get prompted to change the execution policy so you can run the script, type y and press enter.
   ![image](https://user-images.githubusercontent.com/63577525/234580880-e78df284-edea-4a5e-b4c6-4825f6031b4e.png)   
   a) If you instead get a message about "D2Loader.ps1 cannot be loaded because running scripts is disabled on this system" then you will need to perform the following steps:   
   b) Open the start menu and type in powershell. Open PowerShell.<br>
   c) Enter the following command: **Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser**<br>
   d) Type in y and press enter to confirm.<br>
   e) Run the D2Loader.ps1 script again.<br>
3. If the script prompts to trust it and add it to the unblock list, type in y and press enter to confirm.
4. This will perform the first time setup for compiling settext.exe, encrypting your passwords and will create a shortcut on your desktop.

If you've skipped ahead, the script will error out and tell you which of the previous setup steps you've skipped. 

## Settings Switcher (Optional)
Do you want your primary account to launch with decent graphics settings with your other accounts to be set to poo tier settings? This is for you! This feature is disabled by default, as it will cause confusing behaviour for users who haven't read and understood this first.<br>

What this feature does is create copies Settings.json (found in the "C:\Users\\\<yourusername>\Saved Games\Diablo II Resurrected" folder) for each account you have.<br>
E.G if you have 3 accounts, you will have Settings1.json, Settings2.json & Settings3.json. When the script runs and you choose account 1, it copies Settings1.json to Settings.json causing the game to essentially load off those settings. This essentially turns Settings.json into a temporary file that's just used at load time.<br>
NOTE: Any changes you make to non-character options in game (eg graphics, audio, game options) will be saved to Settings.json, which will be overwritten the next time you launch a game via this loader. Therefore if you want to edit your game settings for say your 2nd account, you would need to open your 2nd account, make the options changes you'd like to see that account have each time, close the game and then copy Settings.json to Settings2.json.

**Quick Guide to updating Game settings** for a particular account with this auto switcher.<br>
*For these instructions, let's assume we're trying to edit the config for account 1*
1. Launch the Game (via the Loader or via Bnet client, doesn't matter, the account you log into doesn't matter either).
2. Make the required graphics/audio/game changes via the menu.
3. Close the game.
4. Browse to "C:\Users\\\<yourusername>\Saved Games\Diablo II Resurrected"
5. If there's already a file called Settings1.json, delete it (1 being the account ID in accounts.csv).
6. Copy the Settings.json file and paste into the same folder.
7. Rename to Settings1.json
8. Launch the game and proceed find all of the high runes. All of them.

## Script Config (Mostly Optional)

Default settings within config.xml *should* be ok but can be optionally changed.
- **Most importantly**, if you have a game path that's not the default ("C:\Program Files (x86)\Battle.net\Games\Diablo II Resurrected"), then you'll need to edit this to wherever you chose to install the game.<br>

All other config options below this are strictly optional:<br>
- Set your default region if you just want to mash enter instead of choosing the region.
- Set 'AskForRegionOnceOnly' to True if you only want to choose the region once.
- Set CreateDesktopShortcut to False if you don't want a handy dandy
- Set ShortcutCustomIconPath to the location of a custom icon file if you want the desktop icon to be something else (eg the old D2LOD logo).
- Set ConvertPlainTextPasswords to False if you want your passwords to be ~~stolen~~ in plain text.
- Set ForceWindowedMode to True if you want to force windowed mode each time. This causes issues with Diablo remembering resolution settings, so I recommend leaving this as False and manually setting your game to windowed.
- Set SettingSwitcherEnabled to True if you want your Diablo accounts to load different settings. This essentially changes settings.json each time you launch a game. See the Setting Switcher section above for more info. Disabled by default.

# Notes #
## FAQ / Common Issues

**Q:** The script won't let me run it as it gives me security prompts about scripts being disabled or the current script being untrusted :(<br>
**A:** See Instructions above. The default script policy for Windows 10/11 devices is restricted. We can change this to remote signed. A full write up of the policies can be seen [here](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.3).

**Q:** When Diablo opens it won't allow me to select an online character<br>
**A:** This will be due to your password or username being entered in incorrectly. Please note that multiple failed authentication requests can cause a temporary lockout from that realm (seems to be around 15-30mins).

**Q:** I can't login despite my password being entered in correctly.<br>
**A:** Try logging into the Battlenet client and approve any 2FA/verification requests that might pop up.

**Q:** I have reset one of my Bnet account passwords, how do I update accounts.csv<br>
**A:** Open accounts.csv and clearout the password field and the PWIsSecureString field. Leave the PWIsSecureString field blank. Either enter your password into the csv file or leave it blank and the script will ask you next time you run it. 

**Q:** A UAC prompt opens each time asking me to run as Admin. This is annoying. Can I disable this?<br>
**A:** Yes, there are a couple ways to do this, see here: https://silicophilic.com/add-program-to-uac-exception/#Method_2_Run_Programs_With_Admin_Privileges_Without_UAC_Prompt

**Q:** Why does the script need to run as admin?<br>
**A:** The script needs to run as admin in order to be able to rename your D2r windows once launched. The script uses the names of these Windows to detect which accounts are currently active.

**Q:** I would like to say Thankyou. How do I do that?<br>
**A:** Please pay my entire mortgage. Thanks in advance. Or [D2JSP funny money](https://forums.d2jsp.org/gold.php?i=1328510). Or just a message :)<br>

**Q:** I have suggestions and/or issues with, where do I post these?
**A:** Please use GitHub issues for any feedback. Thanks!

**Q:** Is this Script against ToS?<br>
**A:** Multiboxing itself is not against Blizzard TOS as per this [Blizzard Rep](https://us.forums.blizzard.com/en/d2r/t/blizzard-please-give-us-an-official-statement-on-multiboxing/21958/5) and this [Blizzard Article](https://eu.battle.net/support/en/article/24258). However the only way of achieving this without additional physical computers or Virtual Machines is by killing the "check for Other instances handle".

Outside of killing this handle and renaming the window, there are absolutely no modifications to the game made by this script.
The script is essentially launching the game the same way you would if you had setup shortcuts to the game with account,region,pw parameters, launching that way and then killing the "Check for other instances" handle. This script just helps save you mouse clicks to get you to the character select screen faster with a reduced chance of RSI :).

So the real question is, is using procexp or another method to kill the "check for other instances" handle against ToS? I don't think so, but there are discussions on various forums regarding this matter.

## Notes about the Window title rename (SetText.exe)

The script will generate the .exe file if it doesn't exist. This is to prevent your browser considering it a dodgy file and stopping the download.
To compile the .exe this requires DotNet4.0. If you don't have it the script will prompt you to download this from Microsoft.
~~A Windows Defender exception will also be automatically added for the directory this sits in, as at the time of writing (24.4.2023), Windows Defender considers it to be dodgy.~~ A submission has since been sent to Microsoft and submission has been cleared :)

If you have a Anti-Virus product installed and it kicks up a fuss you may need to manually add an exception to the .\SetText\ folder.

Optional: If you don't trust me and want to build the .exe yourself you can do the following.
1. Browse to the SetText Folder.
2. In the Address bar (the part that shows the path of the folder you're in), click in this, clear out anything that's in it, type in cmd and press enter.
3. This will open the command prompt with it set in the path of where you've saved the script.
4. Next copy and paste the following into CMD:
	SET var=%cd%
	"C:\Windows\Microsoft.NET\Framework\v4.0.30319\vbc.exe" /target:winexe /out:"%var%\SetText.exe" "%var%\SetText.bas" /verbose
5. This should compile SetText.exe. This is used to give the Diablo windows a unique name once it's initialized.

See this site for more information on what this does: https://stackoverflow.com/questions/39021975/changing-title-of-an-application-when-launching-from-command-prompt/39033389#39033389

# What's Next #
* Maybe add a counter for how many times you've launched each account and save this as a column in accounts.csv.
* Perhaps make a GUI *if* there's enough interest.

# Credit for things I stole: #
- Handle killer script: https://forums.d2jsp.org/topic.php?t=90563264&f=87
- Set Text executable: https://stackoverflow.com/questions/39021975/changing-title-of-an-application-when-launching-from-command-prompt/39033389#39033389
- https://learn.microsoft.com/en-gb/sysinternals/downloads/handle
- MoonUnit for thoughts around converting plain text passwords to encrypted strings.
- Google.com
