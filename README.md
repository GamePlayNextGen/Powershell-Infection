Powershell-Infection
====================

Initiate.vbs: Silent wrapper that executes Powershell and then reads config.txt and invokes the commands (.txt is less suspicious then .ps1).

config.txt: Executes the “FetchCommands” function in the “infection.ps1” file on GitHub

ScheduledTask: Executes initiate.vbs which starts the parsing and execution of config.txt
 
The malware operates by checking the raw output of this file on github. This particular file has 2 functions which are “Infect” and “FetchCommands”. When the macro is opened, it executes the infect function which:

– creates 2 files. One in “$env:UserProfile\AppData\Local\Microsoft\Windows\Explorer” called config.txt and the other in “C:\Microsoft\Windows\Desktop” called initiate.vbs. It then sets both files to hidden.

– After the files are created, the infect function creates a scheduled task that executes “initiate.vbs” every 20 minutes.

*To simulate the 20 minute check-in, you can right click on the scheduled task and click “Run”

After the machine is infected, it will pull commands from the FetchCommands function in the Infection.ps1 file on GitHub. To issue add,remove or edit commands you want issued to the infected machine, simply make the changes in the FetchCommands function. (You will need to move this over to your own GitHub account to make changes)


The simplest usage of this is to use the FetchCommands function to Invoke a meterpreter shell when needed.

http://enigma0x3.wordpress.com/2014/07/16/127/
