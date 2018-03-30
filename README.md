# Rasppi JumboTron
Coding and setup for how to set up a simple jumbotron with a raspberry pi. 

This project is to set up a raspbery pi to continually display a slideshow on startup. To do this the slideshow will be hosted on google drive, and the raspberry pi will open it on boot, with a reboot evernight. 

### Slide Show
- Go to google drive and set up a new slideshow (New >> Google Slides). 
- Create your slideshow. You will be able to make changes to the slideshow and it will be pushed to the raspberry pi every night at midnight. 
- Once your ready go to File >> Publish to the Web... 
- Change teh Auto-advance slides: setting to an appropriate time (I put mine for 10 seconds)
- Select Start slideshow as soon as the palyer loads
- Select Restart the slideshow after the last slide
- Copy the URL. Because I had to manually input my url I put it thorugh bit.ly to shorten it. If you use goo.gl it will not keep the new auto advance setting.

### Raspberry Pi Startup
- Assuming that you already have Raspbian installed and running. If not follow [this tutorial](https://www.raspberrypi.org/documentation/installation/installing-images/).

- Navigate to .config/lxsession/LXDE-pi/autostart
- Add the following line `@/usr/bin/chromium-browser --incognito --start-maximized --kiosk http://*yoururlhere*` and replace *yourUrlhere* with your url. 

### Reboot at Midnight
- While the slideshow is editable and you wont need to change the link, inorder for it to apear on the Pi we need to reboot. We can do this by opening terminal and typing $`crontab -e` and add `@midnight /sbin/shutdown -r now`. This will cause the Raspberry Pi to restart at midnight. 

### Notes
- If you need to exit the presentation, spress Alt and Spacebar at the same time. 
