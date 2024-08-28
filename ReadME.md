This repo includes all the files necessary to setup automation of opening timelogging sheet every day at 4 PM (on mac). I inlcuded two script files for opening timesheet: 
* `timelogging.sh` utilizes firefox
* `timeloggingChrome.sh` utilizes Chrome


# Basic Setup
Save script of your choice in a folder under user directory. 
Give script executable permissions with `chmod +x {path to script}`

Update `com.timeloggingweekdays.plist` with appropriate script location and log files.

Save plist file to desired daemon/agent directory. See [Job Definition section of launchd tutorial for more info](https://www.launchd.info/). 

Load the plist into launchd. `launchctl load -F {path to plist}`. Verify it loaded properly and is present in launchd list of jobs. `launchctl list | grep timeloggingweekdays`. 

Test job by starting it manually `launchctl start timeloggingweekdays`. Troubleshoot as necessary. For changes to plist file to take effect, you must unload the plist and load it back in. 

Happy Coding!