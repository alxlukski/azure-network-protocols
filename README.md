<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Part 1 (Create our Resources)
Create a Resource Group
Create a Windows 10 Virtual Machine (VM)
While creating the VM, select the previously created Resource Group
While creating the VM, allow it to create a new Virtual Network (Vnet) and Subnet
Create a Linux (Ubuntu) VM
While create the VM, select the previously created Resource Group and Vnet
Observe Your Virtual Network within Network Watcher

- Part 2 (Observe ICMP Traffic)
Use Remote Desktop to connect to your Windows 10 Virtual Machine
Within your Windows 10 Virtual Machine, Install Wireshark
Open Wireshark and filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity

- Part 3 (Observe SSH Traffic)
Back in Wireshark, filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]

- Part 4 (Observe DHCP Traffic)
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark

- Part 5 (Observe DNS Traffic)
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark

- Part 6 (Observe RDP Traffic)
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Oserve the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

- Part 7 (Lab Cleanup)
(DON’T FORGET THIS)
Close your Remote Desktop connection
Delete the Resource Group(s) created at the beginning of this lab
Verify Resource Group Deletion


<h2>Actions and Observations</h2>

<p>
![Screenshot 2023-12-02 182025](https://github.com/alxlukski/azure-network-protocols/assets/150772204/abfe1a98-d854-4065-85bb-021601e49779)
/>
</p>
<p>
In this screenshot, we log into Microsoft Azure, create a resource group, then create a Windows 10 virtual machine, and an Ubuntu virtual machine inside of the resource group. This allows us to begin the project.
</p>
<br />

<p>
![image](https://github.com/alxlukski/azure-network-protocols/assets/150772204/d8e56f6f-f3cf-4b9f-86cf-d0267dd9d6ac)
</p>
<p>
In this screenshot, we install Wireshark onto the Windows 10 VM, so that we can monitor network traffic inside of, and between the VM's.
</p>
<br />

<p>
![image](https://github.com/alxlukski/azure-network-protocols/assets/150772204/59362154-3c0d-454f-9f05-3bc637aaed23)
![image](https://github.com/alxlukski/azure-network-protocols/assets/150772204/f3501ec4-5939-467a-a2bd-0b1841a6e48a)
![image](https://github.com/alxlukski/azure-network-protocols/assets/150772204/512a6f08-80ec-49bf-b20d-97c2a70e0861)
![image](https://github.com/alxlukski/azure-network-protocols/assets/150772204/3878824f-e926-41ca-a8db-9050a6d62713)
</p>
<p>
In these screenshots, we first filter network traffic to ICMP inside of Wireshark, then we send a ping from the Windows 10 VM to the Ubuntu VM in order to test requests and replies between the VM's. Next we send a perpetual ping, then open the Ubuntu Network Security Group and add a rule that blocks the pings from interacting with the network.
</p>
<br />
