# Rasppi JumboTron
Coding and setup for how to set up a simple jumbotron with a raspberry pi. 

This project is to set up a raspbery pi to continually display a slideshow on startup. To do this the slideshow will be hosted on google drive, and the raspberry pi will open it on boot, with a reboot evernight. 

### Slide Show
- Go to google drive and set up a new slideshow (New >> Google Slides). 
- Create your slideshow. You will be able to make changes to the slideshow and it will be pushed to the raspberry pi every night at midnight. 
- Once your ready go to File >> Publish to the Web... 
- Change the *Auto-advance slides:* setting to an appropriate time (I put mine for 10 seconds)
- Select *Start slideshow as soon as the palyer loads*
- Select *Restart the slideshow after the last slide*
- Copy the URL. Because I had to manually input my url I put it thorugh bit.ly to shorten it. If you use goo.gl it will not keep the new auto advance setting.

### Raspberry Pi Startup
- Assuming that you already have Raspbian installed and running. If not follow [this tutorial](https://www.raspberrypi.org/documentation/installation/installing-images/).
- Navigate to `.config/lxsession/LXDE-pi/autostart`
- Add the following line `@/usr/bin/chromium-browser --incognito --start-maximized --kiosk http://*yoururlhere*` and replace `*yourUrlhere*` with your url. 
- Comment out the line `@xscreensaver -no-splash` in my experience this dosn't do anything...

### Reboot at Midnight
- While the slideshow is editable and you wont need to change the link, inorder for it to apear on the Pi we need to reboot. We can do this by opening terminal and typing `crontab -e` and add `@midnight /sbin/shutdown -r now`. This will cause the Raspberry Pi to restart at midnight. 

### Update Every Hour
- To have the pi refresh the tab were going to add to the crontab. First well need to create a script. In documents create a new file named *refresh.sh*. Fill it with this code:
`export DISPLAY=":0"
WID=$(xdotool search --onlyvisible --class chromium|head -1)
xdotool windowactivate ${WID}
xdotool key ctrl+F5`
- To get it to work we will need to install xdotool. From command line type `sudo apt-get install xdotool`
- Add permsion to the file by `chmod +x /path/to/yourscript.sh`
- Now go to the command line and type `crontab -e` and add `@hourly /home/pi/Documents/refresh.sh'

### Notes
- If you need to exit the presentation, spress Alt and Spacebar at the same time. 


### Refrences
Adding hourly refreshing https://www.raspberrypi.org/forums/viewtopic.php?t=52613
xdotool permission http://theembeddedlab.com/tutorials/simulate-keyboard-mouse-events-xdotool-raspberry-pi/
Running .sh files https://askubuntu.com/questions/38661/how-do-i-run-sh-files
