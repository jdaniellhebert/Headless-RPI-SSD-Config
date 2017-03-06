# Headless-RPI-SSD-Config
Recipe to boot RPI and connect via wifi and SSH
#### Copy Raspbian image to SD Card with Etcher Application (MacOS)
* Download application:  https://etcher.io/
* Download latest Raspbian from Rpi foundation: https://www.raspberrypi.org/downloads/raspbian/ (Lite version)
* Run Etcher Application and copy to SD card.

#### Set up headless boot Wifi credentials and enable SSH for initial boot from SD card
The boot partition on a Pi should be accessible from any machine with an SD card reader, on Windows, Mac, or Linux. 

* To set the Wifi credentials copy a file called "wpa_supplicant.conf" to the /boot/ directory on the SD card.  The file should contain the following:
```
network={
  ssid="Your_ESSID"
  psk="Your_wifi_password"
}
```
* If you want to enable SSH, all you need to do is to put a file called ssh in the /boot/ directory. The contents of the file don’t matter: it can contain any text you like, or even nothing at all. When the Pi boots, it looks for this file; if it finds it, it enables SSH and then deletes the file.  On first boot run raspi-config to enable SSH.
```
$ cd /Volumes/boot
$ touch ssh
```
* Both the ssh file and the wpi_supplicant.conf file will be deleted on first boot after they are used.  Both of these files are included in this repository.

#### Boot RPI with SD card
* Insert SSD card with new flash image.
* Power up the RPI and wait 20 seconds.
* Try to connect to the RPI with SSH.  The out-of-the-box hostname for the RPI is "raspberrypi".  There should be a Bonjour like service running and when the RPI connects to wifi the <hostname> of the RPI should map to the <IP address>.
```
$ ssh pi@raspberrypi.local
```
* Alternate: Run "My Net" MacOS application to find IP address of RPI. You can find this application in the App Store in the applicaiton tray.  SSH to pi@<IP address>
```
$ ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no pi@<IP address> # password: raspberry
```
#### Configure RPI
* Once connected to RPI use raspi-config to change:
 * change to default SSH on
 * enable camera
```
$ sudo raspi-config  # change SSH default to on & change the rpi password.
```
#### Links
* https://www.raspberrypi.org/blog/a-security-update-for-raspbian-pixel/
* https://www.arrow.com/en/research-and-events/articles/headless-setup-for-your-raspberry-pi-3
