# Kubernetes Installation

<h3>Configure share folder</h3>

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

# Disable Swap

```sh
sudo sed -i '/\sswap\s/s/^/#/' /etc/fstab
sudo swapoff -a
free -h
```
<h3>Should look like this</h3>
<img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*XFIwxWHc9SMMXMcWb65-GQ.png" width="800" height="600">
