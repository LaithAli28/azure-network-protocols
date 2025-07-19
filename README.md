
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Network Protocols Using Wireshark</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- Network Security Groups and Inspecting Network Protocols with Wireshark https://www.youtube.com/watch?v=w8H5fWBHddA&t=24s

<h2>Environments and Technologies Used</h2>

- Microsoft Azure Windows and Linux Virtual Machines
- Remote Desktop Connection(RDP)
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
Make sure that both the DC-1 and Client-1 VMs are running. Start with logging into both Windows Virtual Machine using RDP(use public IP to find VMs, then sign in as normal).  
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observing ICMP Traffic: In Wireshark, type "icmp" in the green search bar at the top and press Enter. This filters all but IMCP traffic.
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Now, open Powershell. After opening Powershell, we will run the ping command, followed by the Private IP Address of the Linux VM: "ping 10.0.0.5".  This will allow Wireshark to capture and display new ICMP traffic. 
</p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Back in Wireshark, we see packets which are requests from the Linux VM and the replies from the Windows VM, demonstrating the successful connection between both VMs.  
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Configuring a Firewall (Network Security Group): To start, we start a non-stop ping from the Windows 10 VM to the Linux VM by running the command: "ping 10.0.0.5 -t". This will continue until the firewall is configured.
</p>
<br />

<p>

 <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


</p>
<p>
Back in Microsoft Azure, open the Network Security Group for the Linux VM and disable incoming or inbound ICMPv4 traffic. Then, click on Network Settings, open the Network Security Group settings for the Linux VM, click inbound rules, and click add new inbound rule. Source/Destination Ports have the "*" symbol(which means any port) because ICMP Protocol does not use a specific port. Finally we click "add", and we can see that our new rule was successfully added to the inbound rules.   
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
After enabling our new inbound security rule, we should see a bunch of "Request timed out" notes in Powershell. This shows that our new inbound security rule is working, and with that we have successfully configured a Network Security Group (NSG)! To revert these changes, simply delete the new rule in Azure.
</p>
<br />

<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe SSH Traffic: Secure Shell (SSH) is used to make a secure connection between two computers, enabling all communication to be encrypted or hidden. In the Windows VM, navigate back to Wireshark and start a packet capture with SSH traffic only(type "SSH" into the search bar). Next, go back to PowerShell and run the command  "ssh labuser@10.0.0.5". This tells the Windows VM that we want to Secure Shell connect to the Linux VM from the Windows VM. Next, say "yes" and provide the Linux VM credentials to successfully connect via SSH. SSH uses TCP Port 22.
 </p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p> 
 You should now see the Linux VM's command line in Powershell. This means the SSH connection was successful!
</p>
<br />

<p>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe DHCP Traffic: This protocol assigns an IP address to devices that are connecting to a network for the first time. DHCP uses UDP Ports 67 and 68. Back in Wireshark, filter for DHCP traffic. We will now attempt to issue a new IP address from Powershell. To do this, open PowerShell as an adminintrator and run the command "ipconfig /renew". This starts new DHCP traffic which will be captured in Wireshark.

</p>
<br />


<p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe DNS Traffic: DNS translates between human-readable domain names and IP addresses, and uses TCP/UDP Port 53. From Powershell, run the command "nslookup" followed by the URL of "google.com" and "disney.com" to see what the IP addresses are. In Wireshark, filter for DNS traffic only and observe.

</p>
<br />

<p>

 <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

</p>
<p>
Observe RDP Traffic:(I think you know what RDP does) and it uses TCP Port 3389.  In Wireshark, type "tcp.port == 3389"("rdp" doesn't work) to filter for RDP traffic only. Since this lab is being performed within Azure VMs, there will be a lot of RDP traffic. With that, this lab is complete!
</p>
<br />
