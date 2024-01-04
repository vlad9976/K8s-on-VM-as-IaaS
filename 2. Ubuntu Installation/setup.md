# <img src="../img/icons8-ubuntu-96.png" width="60" height="60"> Ubuntu Server 22.04.3 installation

# <h4>1. Start <img src="../img/icons8-start-96.png" width="20" height="20"> your virtual machine.</h4>
<img src="images/Screenshot_12.png" width="600" height="150">

# <h4>2. installe Ubuntu Server</h4>
<img src="images/Screenshot_2.png" width="800" height="600">

# <h4>3. Bridge network adapter generated IP 192.168.13.242 for new VM (Your ip would be similer to your network ip range)</h4>
<img src="images/Screenshot_3.png" width="800" height="600">

# <h4>4. There is no need to use LVM groups, so you can skip it</h4>
<img src="images/Screenshot_4.png" width="800" height="600">

# <h4>5. Choose you username/password and server name</h4>
<img src="images/Screenshot_5.png" width="800" height="600">

# <h4>6. You can also install OpenSSH <img src="../img/icons8-ssh-96.png" width="20" height="20"> to connect to your virtual machine by ssh</h4>
<img src="images/Screenshot_6.png" width="800" height="600">

# <h4>Now proceed with installation and wait⏳ until Ubuntu is successfully installed on your virtual machine</h4>


# <h4>Finally🥳, installer will ask you to reboot your machine, so after restart login and let’s check that everything goes right way</h4>

# 7. Check Ubuntu installation.
✅Check access to you local computer from master node<br>

     ping <Localhost IP>
</br>
✅Check access to internet on your master node<br>

     curl www.google.com
</br>     
✅Finally, you can check available network interfaces.<br>

    ip a 
</br>

<h4> If all checks were successfully ✅✅✅ passed you are ready to install docker and kubernetes on your virtual machine</h4>

# [Continue to K8s Installation][PlDa]
[PlDa]:<../3. Kubernetes Installation/README.md>

