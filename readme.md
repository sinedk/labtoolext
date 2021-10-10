LabTool
Labtool is a c# tool designed to reproduce Windows real world issues (High CPU, Memory Leak, Unexpected Reboot, etc..) inside lab environment for learning and investigation purposes. Most of the labs contains the "Start" button which will break Windows in order to reproduce the intended issue. Clicking on "Stop" button will revert/undo to the original state. Note that some labs has only the "Start" button where the user will need to manually revert the changes. for this reason is recommended to run labtool only on lab environment.

The tool contains

Active Directory: 5 labs Exchange: 5 labs Network: 1 lab Sql: 1 lab Performane: 21 labs High Availability: 2 labs

Start button

Calls another function responsible to reproduce the issue
Save the start time to disk
Stop button 3. Calls another function to stop the issue and undo the changes made by the Start button 4. Calls API LabTool.Score.ScoreUpload.scoreUploadCloud passing two arguments, the name of the lab and total time spent during the lab

APIs LabTool.Score.PersistedTimeSpent.Save(LabName) - Used to record lab start time to a disk file in case the tool crashes or machine is restart during the lab. Note there are some labs where machine must be restarted in order to be able to reproduce the issue. e.g (Windows Firewall Down lab) It creates txt file with the name of the lab inside c:\temp folder and writes the lab start time

LabTool.Score.ScoreUpload.scoreUploadCloud(LabName, PersistedTimeSpent.Restore(LabName)) - receives labname and call PersistedTimeSpent.Restore(LabName) PersistedTimeSpent.Restore - It calculates how much time user spent troubleshooting the lab based on the lab start time info and current time.
