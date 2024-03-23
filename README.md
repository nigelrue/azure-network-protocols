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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1. Create a new Resource Group. Name it "RG-1".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2. Create a new virtual machine.  using the image: Windows 10 Pro, Version 21H2. Name this virtual machine, "VM-1". Use the same resource group created in step 1, "RG-1". Create a username and password for the virtual machine. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3. Create another virtual machine using the same resource group, "RG-1". Name this virtual machine, "VM-2". Select the image: Ubuntu Server 20.04 LTS. Create a username and password. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 4. Use Microsoft Remote Desktop to log into the Windows 10 virtual machine's public IP address.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 5. Navigate to the Microsoft Edge browser and enter "https://wireshark.org/download.html" and download the latest version of the Wireshark application.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 6. After the Wireshark application is finished downloading, install the app using the default installation settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 7. In Wireshark, begin capturing packets by selecting the Ethernet adapter and clicking the blue shark fin icon. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 8. Observe the network traffic and filter it for ICMP traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 9. Navigate to Windows PowerShell and ping the private IP address of VM-2 (the Ubuntu Server) and observe the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 10. In Windows PowerShell, ping the private IP address of VM-2 once again using the "-t" command which will create a non-stop ping.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 11. In the Azure Portsl, navigate to the network security groups section. Select VM-2 and go to the Inbound Security Rules section and click "Add".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 12. Change the Protocol to "ICMP', select "Deny" for the Action and change the Prioirty to "299" and click "Add".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 13. Observe how the ICMP traffic timed out due to the adjustments made in the network security group section.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 14. Navigate to the Azure portal, network security group for VM-2 and switch the Action back to "Allow" and click "Save".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 15. In Windows PowerShell, you should notice that the ICMP traffic has resumed pinging. Press "Ctrl+C" to stop the pinging. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 16. In Wireshark, enter "SSH" to filter for SSH traffic. In Windows PowerShell, we will SSH into VM-2 to analyze incoming/outgoing traffic. To do this, type "ssh (VM-2's username@VM-2's private IP address)" and press "Enter". Type in the password for VM-2 and press "Enter".
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 17. After SSH'ing into VM-2, execute these commands into Windows PowerShell and observe the SSH network traffic:<br>
-id<br>
-uname -a<br>
-pwd<br>
-ls -lasth<br>
Type "Exit" to exit the SSH process in VM-2.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 18. In Wireshrk, filter for DHCP traffic and while in Windows PowerShell, execute the command "ipconfig /renew". This will allow for DHCP to assign VM-2 a new IP address. Observe the traffic in Wireshark.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 19. Filter for DNS traffic in Wireshark. In Windows PowerShell, type "nslookup www.google.com" and observe the network traffic. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 20. In Wireshark, filter for RDP traffic by typing in "tcp.port == 3389". Observe how there is still incoming/outgoing traffic and this is because this port shows a live stream of traffic at all times.
</p>
<br />



