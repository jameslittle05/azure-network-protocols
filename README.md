<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this project, I observed various network traffic to and from Azure Virtual Machines with Wireshark as well as experimented with Network Security Groups. <br />



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

-Create Resources 
-Observe ICMP Traffic 
-Observe SSH Traffic
-Observe DHCP Traffic
-Observe RDP Traffic

<h2>Actions and Observations</h2>

<p>
First, I created two Virtual Machines (pictured below) with different Operating Systems (Windows 10 21H2 & Linux Ubuntu Server 20.04) to be used for Remote Desktop and to observe network traffic between the two devices.
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, I conducted a quick search for "remote desktop connection". This allowed me to access the VM. Here I entered the details of the public IP address for VM1 (Windows 10 21H2) to install Wireshark (packet analysis software). (below pictured search of remote desktop and the result to enter IP address)
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
On the virtual machine with Windows 10, I downloaded Wireshark (Windows Installer 64-bit) and continue with all the default options.

Then I opened Wirehsark in the VM, click Ethernet and then click the blue fin at the top left under 'File' to begin capturing packets. There was already traffic happening in the background.


After retrieving the private IP address from VM2 (Linux Ubutu Server 20.04) I then pinged that private IP address from VM1 (Windows 10 21H2) that I used to remote into.  I was now able to view the traffic travel from VM1 to VM2 by filtering the ICMP packets in wireshark. The filtered traffic that is requested and its corresponding reply is shown below in Wireshark is pictured (left) and Powershell (right):
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To deny the ping request I played around with this rule in the Network Security settinggs. Once added this rule to VM2, we can see that the traffic times out in PowerShell along with Wireshark longer displaying a reply to this request.


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Wireshark and PowerShell timed out after denying icmp (ping) traffic



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Then I filtered SSH only traffic. I entered SSH into Linux Virtual Machine (VM2) (using "ssh labuser@ip address" its private IP address).  SSH traffic is observed spamming in WireShark. 


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lastly, I filtered RDP traffic only (tcp.port == 3389) because the RDP (protocol) is constantly showing a live stream from one computer to another, therefore traffic is consistently being transmitted

