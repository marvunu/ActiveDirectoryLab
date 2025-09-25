<h1>Active Directory - Homelab</h1>



<h2>Description</h2>
In this project, I built a private network lab to host a Windows Server domain. The server uses two network adapters: one for internet access and a second to create a private internal network. On this internal network, the server acts as a central manager (Domain Controller) that handles logins, automatically assigns IP addresses (DHCP), and directs traffic (DNS/NAT). To simulate a real-world environment, I used a PowerShell script to automate the creation of over 1,000 user accounts. A Windows 10 client was successfully joined to the domain, validating the entire authentication system.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 

<h2>Environments Used </h2>

- <b>Virtual Box</b>

- <b>Windows Server 2019</b>

- <b>Windows 10</b>


<h2>Project walk-through:</h2>

<p align="center">
I built the foundational infrastructure in Oracle VirtualBox by deploying a Windows Server 2019 virtual machine. I configured two network adapters: a NAT adapter for internet access and an Internal Network adapter to create a private, isolated segment for domain traffic.: <br/>
<img src="https://i.imgur.com/luNOkl7.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
Network Configuration: I renamed the server's network adapters to INTERNET and INTERNAL, then assigned a static IP (172.16.0.1/24) to the INTERNAL adapter. Setting the DNS to 127.0.0.1 prepared the server to use its own DNS service for Active Directory.

  <br/>
<img src="https://i.imgur.com/uiskCBF.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I promoted the server to a Domain Controller by installing the Active Directory Domain Services role. This involved creating a new forest with the root domain mydomain.com, establishing the server as the central authority for the network.: <br/>
<img src="https://i.imgur.com/Fg1lLEj.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
Using the Active Directory Users and Computers console, I created an ADMINS Organizational Unit (OU). Inside it, I established a dedicated administrative user account and added it to the Domain Admins group for secure domain management.  <br/>
<img src="https://i.imgur.com/POIEodZ.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I installed the Remote Access role with the Routing feature to enable internet connectivity for the internal network. This allows the server to function as a router, forwarding traffic from the private network to the internet.  <br/>
<img src="https://i.imgur.com/DEFHtjx.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<img src="https://i.imgur.com/GwMornb.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I configured NAT (Network Address Translation) on the server's public-facing INTERNET adapter. This allows all internal clients to share the server's internet connection by translating their private IP addresses.  <br/>
<img src="https://i.imgur.com/YuyhQeb.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I installed the DHCP Server role to automate IP address, DNS, and gateway assignment for clients on the internal network.  <br/>
<img src="https://i.imgur.com/rJRS6wA.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I created and activated a DHCP scope for the 172.16.0.100-200 range, then authorised the server in Active Directory to enable IP address leasing.  <br/>
<img src="https://i.imgur.com/RRUUkNm.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I used a PowerShell script to automatically create one thousand test user accounts in the domain, enabling flexible login testing on the Windows 10 client.  <br/>
<img src="https://i.imgur.com/39oOPWp.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<img src="https://i.imgur.com/YOhuWzH.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
I installed a Windows 10 VM named CLIENT1 and connected it to the private domain network by configuring its VirtualBox adapter to use the "inet" internal network.  <br/>
<img src="https://i.imgur.com/PUXvon8.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
The ipconfig command on CLIENT1 confirmed successful network connectivity, showing it received an IP address (172.16.0.100) via DHCP, with the domain server correctly set as its gateway and DNS.  <br/>
<img src="https://i.imgur.com/PV2Ia4J.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
The final step was to integrate the client into the domain management system. In the System Properties of CLIENT1, I changed its workgroup membership to the domain, mydomain.com.  <br/>
<img src="https://i.imgur.com/htUpsER.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<br />
<br />
After a restart, I was able to log in successfully using the credentials of one of the thousand user accounts created by the PowerShell script. This successful login confirmed that the client was fully recognized and authenticated by the Active Directory domain.
  <br/>
<img src="https://i.imgur.com/W8HxMXg.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<img src="https://i.imgur.com/4Cssbi1.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
<img src="https://i.imgur.com/i4HIS1q.png" height="80%" width="80%" alt="ActiveDirectoryHomelab"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
