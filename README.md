# GNS3-Network-Project
Built a Network from ground up.
[10:42 AM] Jordan Marshall (Guest)
# GNS3-project

GNS3 network creation

## **Start of project**

![STAGE 0 drawio (1)](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/d08e00aa-4c10-4a21-905d-df3a76f3f706)
 
This was the start of the project given to us by the staff of Divergence Academy, and is the network before installation of other switches or routers.
 
---

STAGE 1
 
![Stage 1 drawio](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/21317d16-f1e5-4e3f-8c63-d6a72c955274)
 
In this stage, I added a Fortinet firewall, 2 ethernet switches, and a windows 10 workstation

From there: 

Link the WAN port on the firewall to the WAN-SWITCH.

Link the LAN port on the firewall to the LAN-SWITCH.

Link the DMZ port on the firewall to the DMZ-SWITCH.

Link the Win10 workstation to the LAN-SWITCH.
 
---

STAGE 2
 
![STAGE 2 drawio](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/81ace8a6-8893-4a63-9eff-ba46dae2f8c5)
 
![Screenshot 2024-05-21 155928](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/ebcbc22c-dc51-4c2c-bb6b-8870f79b9feb)
 
In this screenshot, we had to set a static IP address for our network adapter. The reason a static IP address was needed was because for our network we can't have the IP address changing everytime the server turns on and connects to the internet. When information travels to our network and pings our server, traffic will be lost if the IP address is constantly changing using DHCP.
 
![Screenshot 2024-05-21 155952](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/f2dc514d-325a-4381-9d08-26447c48b375)
 
Step 1 : Add a Win2012r2 server to the lab workspace.

Step 2 : Link the Win2012r2 server to the LAN-SWITCH

Step 3 and 4 : After setting our static IP address, subnet mask, and default gateway; along with our DNS Server. I had to ping the google.com server to ensure that the DNS server was responding to requests. I pinged 8.8.8.8 (google DNS) to ensure there was connectivity to the internet from our IP address.

Step 5 and 6 : of this process consisted of me setting up an active directory service to create user accounts (12 total) 2 per user in my group. An admin and an user account.
 
---

STAGE 3
 
![STAGE 3 drawio](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/6fb1101d-3c8e-4ad9-b3e5-c9939cd3d107)
 
Step 1 : As you can see I added another windows server, linked it to the LAN switch.
 
![Screenshot 2024-05-21 164710](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/4d653f49-2d7e-4621-aa77-e497ff563a9b)
 
Step 2 : In this server I assigned another static IP address to the new server with the same subnet mask and default gateway. I changed the DNS 1 IP address due to the domain controller acts as the internal DNS server. So if windows2012r2-2 has a request, it reaches out to Windows server 2012r2-1, if win2012r2-1 server doesn't have the DNS query asked for, win2012r2-1 reaches out to the router/firewall who then asks 8.8.8.8 or google.com if they have the answer. After that I Synced the time using NTP (network time protocol).

Installed IIS webserver on windows server and joined the server to the domain.
 
---

STAGE 4
 
![STAGE 4 drawio](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/eef50f79-9c70-4068-a446-5f94d1466f60)
 
Step 1 : Add an ubuntu server and link it to the DMZ Switch.
 
![Screenshot 2024-05-23 105805](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/7b045682-3740-4d3c-8bee-aae7646589b4)
 
Here we set another static IP address to the server. This time it was because we did not have a DHCP server for the DMZ switch. The Ubuntu server was on a different server and subnet from the DHCP server established in the Local Area Network. Our Ubuntu server is also on a DMZ switch which is a public facing network and you want that IP address to be consistent so we had 2 reasons for creating the network this way.
 
![Screenshot 2024-05-23 110144](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/dc196b56-59a0-41a2-b946-62b4f0a52d03)
 
Step 2 : Installing dokuwiki on the Ubuntu server using the terminal on ubuntu.
 
![image](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/6a594e80-fb06-407a-8b37-72a2aaccfa32)
 
This is how dokuwiki looked after installation, and before configuring the webpage.
 
![Screenshot 2024-05-23 115901](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/7894ad92-f1f8-42ba-a21b-46c5e7fc06bf)
 
Step 3 : Here I configured the dokuwiki webpage to all of the admin accounts created in stage 2. I configured a documentation report of the network detailing of the firewall, windows 10 workstation, a domain controller (dc) which was also the internal DNS and provided Active Directory (AD) services, an IIS webserver, and a dmz network.
 
![image](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/ae677f20-45a4-4c98-b0ae-c2a3073f49cb)
 
Step 4 : After configuring the dokuwiki webpage, I configured a Virtual IP (VIP) for the public side of the webserver on the firewall.

This picture details how traffic flows through the firewall and what ports certain parts of our traffic are configured on. For example, our DMZ (demilitarized zone) network is configured on port 4 and our LAN (Local Area Network) is configured on port 2.
 
---

STAGE 5
 
![STAGE 5 drawio](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/c8c643c9-cfd2-42fd-881e-1ba02bd6f006)
 
Step 1 : In this stage like the other I created another windows server and linked it to the DMZ switch.
 
![Screenshot 2024-05-23 122614](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/7a27a82a-5848-4aa0-8546-dc7316e683ba)
 
Step 2 : Another static IP address was set for the server, along with other static addressing as seen in the photo. After configuring the addressing I synced the computer using the NTP protocol and then joined the server to the domain of our network.

Step 3 : In this step an FTP service was installed, however my group and I had to implement steps from a microsoft guide on how to do so, but I cannot provide a screenshot for view, due to the excessive length of the steps.
 
---

STAGE 6
 
In this stage there were no changes to the lab workspace. Instead I created a "Hardening Research Notes" tab for us to detail how we could harden the existing network on the Dokuwiki webpage.
 
![Screenshot 2024-05-23 123844](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/1a92fe2e-7543-4a57-bde3-4af4f0eaaaa9)
 
This is an example of the hardnening notes. Top right corner shows the rest of the notes for the servers and workstation implemented in the network.
 
---

STAGE 7 (Bonus Stage)
 
In this stage we conducted a vulnerabiity scan on the network using a Greenbone server.
 
![image](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/77919318-bb18-4de4-b81d-48da730b7c7b)
 
 
Here are a few of the vulnerabilities on the network. 

Next will be the documentation of the scans (severity, summary, impact and solution).
 
![image](https://github.com/BlazWilson/MSP-LAN-/assets/170445236/6148aea2-2552-4b28-86c4-d286c79d792d)
 
The documentation report was created based on our vulnerability scan to detail the weaknesses in our network, the severity of the weakness, how it impacts our system, and how we can fix it in the future. Here are just a few of the vulnerability that were shown in the scan. The network was created the way it is in order for this scan to show possible vulnerabilities.
 
---

Summary
 
In this detailed diagram we created a 

A SMB (small/medium business) network, with a LAN, DMZ, and Guest network.

A Windows domain environment.

A IIS webserver.

A Windows FTP server.

A Win10 workstation.

A LAMP webserver running on Ubuntu, hosting a wiki.

A FortiGate firewall, with a VIP for a DMZ webserver.
