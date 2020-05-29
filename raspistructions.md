# Taking Photos With A Raspberry Pi

## To Turn RasPi On/Off

### On
- Plug battery into Pi
- Wait 10ish seconds for it to boot up

### Off
- `sudo shutdown now -P` to shut Pi down safely and power it down
- Wait a few seconds, then unplug the battery

## To Transfer Files from RasPi to Mac

- Download FileZilla Client: https://filezilla-project.org

- Set the following settings:
	- You can also save these settings into a profile if you click the icon in the top left (Site Manager) and click new site. When you restart FileZilla you can just click this icon again, choose the saved site and click connect.
- Host: sftp://rubus1
- Username: pi
- Password: password
- Port: 22


- Click Quick Connect
- Click OK to accept the Unknown Host Key

There will now be a side by side with your computer’s filesystem on the left and the RasPi’s on the right.

- Navigate to your Desktop on the left (/Users/yourname/Desktop)
- Navigate to the photo folder on the Pi’s Desktop on the right (/home/pi/Desktop/photos)
- Drag a photo (or folder) from the right side to the left to copy it from the Pi to your Desktop
- The image(s) will appear on your Desktop once the transfer completes



## To Take Pictures on the RasPi

- Open Terminal
- Type `ssh pi@rubus1.local`
    - Without the backticks ` `
    - Backticks are used to signify code in Markdown (which this document is written in)
- Enter password: `password`
- Type `cd Desktop/photos` to change directory (cd) into the Desktop/photos folder
- Type `ls` to list (ls) files in this folder
	- If you use a filename that already exists, you will overwrite the pre-existing file with a new one
- You are now ready to take photos
- we'll use the raspistill tool to take pictures
- Type `raspistill` to view a list of commands you can run
- Examples:
	- `raspistill -o image.jpg` 
		- Takes a picture named image.jpg. 
		- **You must always specify `-o filename.jpg` or no image will be saved**
		- The picture will take a few seconds to take; once you see another $ in your command line, the picture is ready
		- Type `ls` to list (ls) the files in the photos folder and verify your picture was taken
		- You can now copy the file over with FileZilla and view it on your Mac
	- `raspistill -t 30000 -tl 2000 -o image%04d.jpg`
		- Take an image every 2s (`-tl 2000`)
		- Over 30s/30000ms (`-t 30000`)
		- Name each file image####.jpg sequentially (`-o image%04d.jpg`)
			- image0001.jpg, image0002.jpg, etc.
		- Stitch the images together [TODO](https://www.raspberrypi.org/documentation/usage/camera/raspicam/timelapse.md)
	- `raspistill -o image.jpg -hf -vf`
		- Take a picture naamed image.jpg
		- Flip it horizontally `-hf`
		- And vertically `-vf`


- Type `sudo shutdown now -P` to shut Pi down safely and power it down
- Wait a few seconds, then unplug the battery



## Notes
- Apparently the focus is set to infinity so anything .5m (1.6ft) or more will be in focus
