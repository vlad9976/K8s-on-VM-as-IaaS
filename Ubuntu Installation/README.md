# Ubuntu Server 22.04.3 installation

# Start your virtual machine.
<img src="images/Screenshot_12.png" width="600" height="150">

# installe Ubuntu Server
<img src="images/Screenshot_2.png" width="800" height="600">

# Bridge network adapter generated IP 192.168.13.242 for new VM
<img src="images/Screenshot_3.png" width="800" height="600">

# There is no need to use LVM groups, so you can skip it
<img src="images/Screenshot_4.png" width="800" height="600">

# Choose you username/password and server name
<img src="images/Screenshot_5.png" width="800" height="600">

# You can also install OpenSSH to connect to your virtual machine by ssh
<img src="images/Screenshot_6.png" width="800" height="600">

# Now proceed with installation and wait until Ubuntu is successfully installed on your virtual machine


# <h3> Finally🥳, installer will ask you to reboot your machine, so after restart login and let’s check that everything goes right way</h3>

# Check Ubuntu installation.
Check access to you local computer from master node<br>

     ping <Localhost IP>
</br>
Check access to internet on your master node<br>

     curl www.google.com
</br>     
Finally, you can check available network interfaces.<br>

    ip a 
</br>

<h3> If all checks were successfully passed you are ready to install docker and kubernetes on your virtual machine</h3>

# [Continue to K8s Installation][PlDa]
     [PlDa]:<../Kubernetes Installation/

