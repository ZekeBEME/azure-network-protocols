<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


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

- Create our Resources
- Install Wireshark 
- Observe ICMP, SSH, DHCP, DNS, RDP Traffic

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/aJ7TNrs.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Create two Virtual Machines(VM) in Azure, one running Windows 10 and one using Linux (Ubuntu). Ensure both VMs are running on the same virtual network.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Use Remote Desktop to connect to your Windows 10 VM and install Wireshark from the web. Open Wireshark and filter for ICMP Traffic only. Retrieve the Private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM. The request times out because we haven't allowed ICMP traffic through the firewall.
</p>
<br />

<p>
<img src="https://i.imgur.com/SBC5exf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Change both VMs to allow ICMP traffic then initiate a perpetual ping again from your Windows 10 VM to your Ubuntu VM and observe traffic. Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic. Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity. Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using then observe the ICMP traffic in WireShark and the command line Ping activity (should start working)

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Wireshark, filter for SSH traffic only. From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address).Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew). Observe the DHCP traffic appearing in WireShark
</p>
<br />

<p>
<img src="https://i.imgur.com/6Kr7vau.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark

</p>
<br />

<p>
<img src="https://i.imgur.com/XbnBCoE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Observe the immediate non-stop spam of traffic? Why do you think it’s non-stop spamming vs only showing traffic when you do an activity?
Answer: because the RDP (protocol) is constantly showing you a live stream from one computer to another, therefor traffic is always being transmitted

</p>
<br />
