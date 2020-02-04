
V0.6

Before starting this:

Parts:
- Raspberry Pi Zero WH (Wireless, and with Headers presoldered)
- PiOled
- Microsd card (at least 8GB strongly recommended, though you may
be able to get away with 4GB with Raspbian Buster Lite.
- USB-microsd adaptor or USB-SD adaptor so you can mount the microsd in
your laptop.
- Microusb power supply

- Download the Raspbian Buster image from
https://www.raspberrypi.org/downloads/raspbian/ .  You only need the
Lite version for this project.  If you want the desktop or
desktop+recommended software version, feel free to get those.  Each is
delivered as a zip file; if you're using Balena Etcher (cross-platform,
recommended), you do not need to unzip the file.

- Mount the microsd in an existing computer (you may need a USB-microsd
adaptor or SD-microsd adaptor)

- Follow the install instructions at
 https://www.raspberrypi.org/documentation/installation/installing-images/README.md

- After the image has been written, if the microsd was automatically
unmounted on that system, eject it and reinsert it.  It may show up in a 
directory called "boot".

- Create an empty file called "ssh" (no extension) in the top level
directory of your microsd (this directory will have multiple files
including "config.txt").

Create another file in the microsd top level directory called
wpa_supplicant.conf and place the following lines in it:


ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US
network={
	ssid="MYWIFINAME"
	psk="wifipassword"
	key_mgmt=WPA-PSK
}


(This will end up in /etc/wpa_supplicant/wpa_supplicant.conf in the
installed OS.)  Replace US with the two letter ISO country code for your
country.  If your wifi network has no password, delete the psk line and
change the key_mgmt line to "	key_mgmt=NONE" without quotes.  If this
wireless network is hidden, add "scan_ssid=1" below the "ssid=" line. 
More details at:
https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md

- Unmount and eject the microsd and place it in your Rasberry Pi 4/4GB

- Connect the microsd power adaptor to the connector the furthest from
the microusb port and boot the system.

- "ssh pi@raspberrypi.local." from your laptop.  Password is raspberry.

- Immediately change the password with "passwd".

- Copy this script over to your pi with:
scp -p pi_sensor pi_project_lib pi@raspberrypi.local:

- In your ssh session, run:
chmod 755 pi_sensor
./pi_sensor

