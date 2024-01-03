# Kubernetes Installation

# Configure share folder

<h4>First of all got to Devices -> Insert Guest Additions CD image<h4>
<img src="images/Screenshot_11.png" width="800" height="600">

<h3>From the terminal, run the following commands:<h3>

```sh
  sudo su
  apt install gcc make
  mkdir --parents /media/cdrom
  mount /dev/cdrom /media/cdrom
  /media/cdrom/VBoxLinuxAdditions.run
  reboot
 ```