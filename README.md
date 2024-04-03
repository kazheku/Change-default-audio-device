<h2>Change default audio device at startup</h2>


So i found a way to run a **script** at startup that will set your **default audio device** *(which also switches to that device when it's run)*

I started by adding a **cmdlet** to ***powershell*** (this allows powershell to run a command that isn’t natively installed).
The one I used included multiple audio related commands (such as set default device). Then I created a basic script (.ps1 file) which just uses the set default audio command. Last I created a scheduled task which runs Powershell and runs the script.

**INSTALL cmdlet**

I used this one: https://github.com/frgnca/AudioDeviceCmdlets

Run your Powershell as admin, then type the following command and hit enter.

***Install-Module-Name AudioDeviceCmdlets***

You get a couple prompts saying it needs to allow unrecognized repositories (do your own due diligence to check into this). Once it’s installed you can use all the new commands in Powershell that were listed on the GitHub page.


**CHANGING DEFAULT AUDIO DEVICE USING POWERSHELL**

Open Powershell to test if the install worked. In my case, my preferred audio device was device 2 (can be checked using command ***Get-AudioDevice-List***) So my command ended up as:

***Set-AudioDevice 2 -DefaultOnly***

**CREATE SCRIPT**

- Run Windows Powershell ISE as admin.
- Create new file.
- Paste command using your preferred audio device (which was 2 in my case)

***Set-AudioDevice 2 -DefaultOnly***

Save the file as ps1.

**CREATE SCHEDULED TASK**

- Open task scheduled.
- Create a new task in the task scheduler library.

_General Tab_
- Run whether the user is logged on or not.
- Run with highest privileges.
- Configure for Windows 10.

_Triggers tab_
- New > At log on, delay task 30 seconds (arbitrary but i wanted it to have a chance against SONAR in case i reinstall it)

_Actions tab_
- Start a program.
- Settings> C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe (or wherever Powershell is install for you)
- Settings > add arguments (location of ps1 file) > C:\Users\User1\Documents\Scripts\Change_default_audio_device.ps1

Lastly click ok to save the task(need to enter admin password). Then you can test the task works by first changing to a different default audio device then going to the task scheduler library, right click on the task, then click run. If everything is done correctly it will change the audio default to whatever you selected.

“I personally had to change one thing: Allow scripts to be run on PC by giving permission. I had to run the command:

***Set-ExecutionPolicy Unrestricted***

In Powershell to fix this”










  



