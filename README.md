
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Network Protocols Using Wireshark</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- Network Security Groups and Inspecting Network Protocols with Wireshark https://www.youtube.com/watch?v=w8H5fWBHddA&t=24s

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Windows and Linux Virtual Machines
- Remote Desktop Connection
- Powershell and Various Command-Line Tools
- Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (packet analyzer or network sniffer)

<h2>Operating Systems Used </h2>

- Windows 10 Pro
- Linux Ubuntu

<h2>High-Level Steps</h2>

- Observe ICMP Traffic (Internet Control Message Protocol)
- Configure a Firewall (Network Security Group)
- Observe SSH Traffic (Secure Shell)
- Observe DHCP Traffic (Dynamic Host Configuration Protocol)
- Observe DNS Traffic (Domain Name System)
- Observe RDP Traffic (Remote Desktop Protocol)

<h2>Actions and Observations</h2>

<p>

 <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Make sure that both of the Virtual machines are running. Start with logging into the Windows Virtual Machine using Remote Desktop Connection. Copy and paste the public IP address of the Windows Virtual Machine and supply the credentials to log in.   
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observing ICMP Traffic. We start by typing icmp all lower case in the green search bar and pressing "Enter". This tells Wireshark to filter out all inbound and outbound traffic except for ICMP Traffic. We will now be able to see the ICMP packets captured.    
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
After opening Powershell, we will run the Ping Command, followed by the Private IP Address of the Linux Virtual Machine , "ping 10.0.0.5".  This will allow Wireshark to capture and display the ICMP traffic that we're looking for. 
</p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Back in Wireshark, we see the packets, which are requests from the Linux Virtual Machine, as well as the replies from the Windows Virtual Machine. This shows that the Windows and Linux Virtual Machines both have a successful connection.   
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Configuring a Firewall (Network Security Group). To start, we initiate a perpetual/non-stop ping from the Windows 10 Virtual Machine to the Linux Virtual Machine by running the command... "ping 10.0.0.5 -t". We will notice that Wireshark starts to non-stop ping ICMP Traffic.  
</p>
<br />

<p>

 <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<p>
Back in Microsoft Azure, open the Network Security Group for the Linux Virtual Machine and disable incoming or inbound ICMPv4 traffic, this is the traffic that appears in Wireshark after running the "Ping" command . Click on Network Settings, open the Network Security Group settings for the Linux Virtual Machine, click inbound rules, and click add new inbound rule. Source/Destination Ports have the (*) symbol, which means any port, this is because ICMP Protocol does not use any specific ports. Finally we click "add". We can see that our new inbound rule was successfully created.   
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
After enabling our new Inbound Security Rule, we now only see "Request timed out". This shows that our new Inbound Security Rule is working and we now have successfully configured a Network Security Group (NSG). We can delete the rule if we want to revert the changes.  
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe SSH Traffic. Secure Shell (SSH) is used to make a secure connection from one computer to another, this ebables all communication to be encrypted or hidden. In the Windows virtual machine, open Wireshark and start a packet capture. Filter for SSH traffic only. Next, open PowerShell and run the command  "ssh labuser@10.0.0.5", this tells the Windows virtual machine that we want to Secure Shell (SSH) connect to the Linux Virtual Machine from the Windows Virtual Machine. We specified the username and private IP Address of the Linux Virtual Machine after the SSH command in order to connect our Windows Virtual Machine to the Linux Virtual Machine via Secure Shell (SSH) connection. Say "yes" to fingerprint and provide the Linux virtual machine credentials to successfully connect via Secure Shell (SSH). Secure Shell uses TCP Port: 22.
 </p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p> 
 We can see that the connection to the Linux VM was successful.
</p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe DHCP Traffic. This protocol is used to assign an IP address to devices when they are first connected to the network. Dynamic Host Control Protocol (DHCP) uses UDP Ports: 67 and 68. Back in Wireshark, we filter for DHCP traffic only from the Windows 10 virtual machine, attempt to issue a new IP address from the command line. Open PowerShell as an adminintrator and run the command "ipconfig /renew". We will now see the DHCP traffic being captured in Wireshark.

</p>
<br />


<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe DNS Traffic. DNS, or Domain Name System, uses TCP/UDP Port: 53. From Powershell in the Windows VM, run the command "nslookup" followed by the URL of "google.com" and "disney.com" to see what the IP addresses are. In Wireshark, filter for DNS traffic only. Observe the DNS traffic being shown in WireShark

</p>
<br />

<p>

 <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe RDP Traffic (Remote Desktop Protocol). In Wireshark, we type "rdp" in the search bar, followed by pressing "enter", in order to filter for RDP traffic only. RDP or Remote Desktop Protocol, is used for remotely connecting from one computer to another, gaining a Remote Desktop Graphical User Interface (GUI). RDP uses TCP Port: 3389
</p>
<br />
