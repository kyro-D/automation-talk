This repo includes all the files necessary to setup automation of opening timelogging sheet every day at 4 PM (on mac). I inlcuded two script files for opening timesheet: 
* `timelogging.sh` utilizes firefox
* `timeloggingChrome.sh` utilizes Chrome


# Basic Setup
Save script of your choice in a folder under user directory. 
Give script executable permissions with `chmod +x {path to script}`

Update `com.timeloggingweekdays.plist` with appropriate script location and log files.

Save plist file to desired daemon/agent directory. See [Job Definition section of launchd tutorial for more info](https://www.launchd.info/). 

Load the plist into launchd. `launchctl load -F {path to plist}`. Verify it loaded properly and is present in launchd list of jobs. `launchctl list | grep timeloggingweekdays`. 

Test job by starting it manually `launchctl start timeloggingweekdays`. Troubleshoot as necessary. For changes to plist file to take effect, you must unload the job from launchd `launchctl unload {path to plist}` and load it back in. 

# Troubleshooting Tips

For changes in plist to take effect job has to be unloaded from launchd and loaded again. Making edits to plist file without unloading and reloading the job won’t do anything. 

When in doubt check error logs defined in plist.

I ran into inconsistency issues with my job when key `RunAtLoad` was not set. Job would work on some days and wouldn't on others. Adjusting this key made my job run consistently. 

Launchd couldn’t run my script when it was saved under User/Documents. Apple considers this folder as private. Moving script out of this directory resolved permission denied issues. 


Happy Coding!
