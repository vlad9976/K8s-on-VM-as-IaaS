# VirtualBox Master🤖 Workers👾👾 Setup.

<h1>Create virtual machines</h1>
<h3>Let’s create virtual machines. I will describe the detailed scenario for master node and you can create 2 worker nodes by yourself.</h3>
<h3>First, download required images. You can use the following link https://ubuntu.com/download/server to download Ubuntu iso image. </h3>

# <h4>1. Open VirtualBox and choose “New” to start configuration.</h4> 
<img src="images/Screenshot_5.png" width="600" height="100">

# <h4>2. In the opening form type new virtual machine name and choose the path where VM data will be stored.</h4>
<img src="images/Screenshot_1.png" width="700" height="400">

# <h4>3. Now press “Next” and configure CPU and memory resources. I would suggest at least 2 CPU and 2G RAM.</h4>
<img src="images/Screenshot_2.png" width="700" height="350">

# <h4>4. Configuration of disk space resources. For master node we will set 20GB disk and 50GB for each worker node </h4>
<img src="images/Screenshot_3.png" width="700" height="350">
# <h4>Press “Next” and finish set up.</h4>

# <h4>Shutdown the new create vm to configure the network</h4>
<img src="images/Screenshot_9.png" width="600" height="100">

# <h4>Choose “Settings” for you new virtual machine</h4>
<img src="images/Screenshot_4.png" width="600" height="100">

# <h4>Go to “Network” and choose “Bridge Adapter” as a network interface. With this option your virtual machine will be in the same network as you computer and will get access to internet</h4>
<img src="images/Screenshot_6.png" width="700" height="350">

# <h4>I chose network interface "Intel(R) Wi-Fi 6 AX201 160MHz". Let’s check such interface exists in my network. My desktop is running on Windows 10</h4>
<img src="images/Screenshot_8.png" width="700" height="350">









