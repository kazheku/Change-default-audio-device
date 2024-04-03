<h2>Change default audio device at startup</h2>


So i found a way to run a **script** at startup that will set your **default audio device** *(which also switches to that device when it's run)*

I started by adding a **cmdlet** to ***powershell*** (this allows powershell to run a command that isn’t natively installed).
The one I used included multiple audio related commands (such as set default device). Then I created a basic script (.ps1 file) which just uses the set default audio command. Last I created a scheduled task which runs Powershell and runs the script.

**INSTALL cmdlet**

I used this one: <a href="https://github.com/frgnca/AudioDeviceCmdlets" />

