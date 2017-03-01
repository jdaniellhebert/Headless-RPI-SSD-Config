# Headless-RPI-SSD-Config
After you follow this recipe you will be able to boot RPI and connect via wifi and SSH
#### Install Hypriot flash command (MacOS)
```
$ brew install pv  
$ brew install awscli  

$ curl -O https://raw.githubusercontent.com/hypriot/flash/master/$(uname -s)/flash  
$ chmod +x flash  
$ sudo mv flash /usr/local/bin/flash  
```
#### Copy image to SD Card using Hypriot flash command (MacOS)
```
$ diskutil list   # Lists mounted drives.  Make a note of the disk # of the SD card.  
$ flash --hostname <unique-rpi-hostname> --ssid <Your-Wifi-SID> --password <Your-Wifi-Password> http://downloads.hypriot.com/hypriotos-rpi-v1.0.0.img.zip  

# Modify the fields above that are delinated by "<>" with a unique hostname and wifi creditionals.
# WARNING: flash will prompt you to double check the SD card disk #, take care.

# Example:  
$ flash --hostname v2c1 --ssid "name with spaces" --password passwordwithnospaces https://github.com/hypriot/image-builder-rpi/releases/download/v1.1.0/hypriotos-rpi-v1.1.0.img.zip  
```
#### Start up Rpi3 with Docker
1. Plug in SD card and apply power to Rpi3
2. Use an application for MacOS like "My Net" to scan the network for the IP_Address of the Rpi
3. From the command line SSH to pi@<IP_Address>, the password is "raspberry".
```
# use a net work scanning app or tool to find the ip address (ex. 192.168.7.41)
$ ssh pi@192.168.7.41

$ ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no pi@<IP address> # password: raspberry
```
#### Configure RPI
* Once connected to RPI use raspi-config to change:
 * expand filesystem
 * default SSH on
 * enable camera
 * enable I2C
 * etc
```
$ sudo raspi-config
```
