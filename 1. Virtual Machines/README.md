# VirtualBox Master🤖 Workers👾👾 Setup.

<h1>Create virtual machines</h1>
<h4>Let’s create virtual machines. I will describe the scenario for master node and you can create 2 worker nodes by yourself.</h4>
<h4>First, download required images. You can use the following icon <a href="https://ubuntu.com/download/server" target="_blank"><img style="margin: 10px" src="../img/icons8-ubuntu-96.png" height="50" /></a> to download Ubuntu iso image.</h4>

# <h4>1. <img src="/img/icons8-open-box-64.png" width="30" height="30"> Open VirtualBox and choose “New” to start configuration.</h4> 
<img src="images/Screenshot_5.png" width="600" height="100">

# <h4>2. In the opening form type new virtual machine name and choose the path where VM data will be stored.</h4>
<img src="images/Screenshot_1.png" width="700" height="400">

# <h4>3. <img src="../img/icons8-cpu-96.png" width="30" height="30"><img src="../img/icons8-ram-66.png" width="30" height="30"> Now press “Next” and configure CPU and memory resources. I would suggest at least 2 CPU and 2G RAM.</h4>
<img src="images/Screenshot_2.png" width="700" height="350">

# <h4>4. <img src="../img/icons8-hdd-96.png" width="30" height="30"> Configuration of disk space resources. For master node we will set 20GB disk and 50GB for each worker node </h4>
<img src="images/Screenshot_3.png" width="700" height="350">
<h4>Press “Next” and finish set up.</h4>

# <h4>5. <img src="../img/icons8-shutdown-96.png" width="30" height="30"> Shutdown the new create vm to configure network</h4>
<img src="images/Screenshot_9.png" width="400" height="100">

# <h4>6. <img src="../img/icons8-settings-96.png" width="30" height="30"> Choose “Settings”</h4>
<img src="images/Screenshot_4.png" width="600" height="100">

# <h4>7. Go to “Network” and choose “Bridge Adapter” as a network interface. With this option your virtual machine will be in the same network as you computer and will get access to internet</h4>
<img src="images/Screenshot_6.png" width="700" height="350">

# <h4>8. I chose network interface "Intel(R) Wi-Fi 6 AX201 160MHz". Let’s check such interface exists in my network run ipconfig /all. My desktop is running on Windows 10</h4>
<img src="images/Screenshot_10.png" width="500" height="250">

# <h4>9. I also suggest to configure a shared folder, because it’s very helpful to use bash scripts during setup</h4>
<img src="images/Screenshot_12.png" width="500" height="250">

<h4>10. Now save all your settings</h4>

# Continue

[<img src="../img/icons8-next-96.png" width="75" height="75">   <img src="../img/icons8-ubuntu-96.png" width="75" height="75">][PlDa]

[PlDa]:<../2. Ubuntu Installation/README.md>



