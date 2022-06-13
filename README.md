<h1>Azure Sentinel (SIEM) Live Attack Project</h1>

<h2>Description</h2>
In this project we will create a VM which is purposely vulnerable to entice attackers to try brute force our VM, essentially a 'Honeypot'. These attacks will then be logged in our 'Windows Event Viewer', which we will then fed to a third-party API by using our custom Powershell Script. The Powershell script will extract the 'Failed Remote Login (eventId:4625)' data from the 'Windows Event Viewer' and forward it to a third-party API which will gather further geolocation data such as 'Country,Longitude,Latitude etc'. Once done we will have this new logged data referenced in our Azure log analytics workspace, which will have custom fields setup.

Lastly we will have Azure Sentinel (Microsoft's cloud SIEM) workbook configured. This will be connected to our log anayltics workbook, allowing us to have a relation to our 'failed RDP attack data'. With this we can use Azure Sentinel to visualise our global attack data on a world map , to give us a clear image of where the attacks are coming from.
<br />

<h2>Utilities Used</h2>

- <b>Azure Sentinel workbook</b>
- <b>Azure Log analytics workbook</b>

<h2>Environments Used </h2>

- <b>Windows 10(VM)</b> 




<h2>Project Walk-Through</h2>

<p align="center">
  
<h3>Setting up VM,Log Analytics & Sentinel Workbook</h3>

Creating VM: <br/>
<img src="https://i.imgur.com/UTXviQy.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

Creating Log Analytics Workspace: <br/>
<img src="https://i.imgur.com/Hlii8m1.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
Creating Sentinel Workspace: <br/>
<img src="https://i.imgur.com/SZTzMzL.png" height="80%" width="80%" alt="NessusLab"/>
<br />
<br />


<h3>Making Our Machine Vulnerable (HoneyPot)</h3>


After all the basic setup is done we will now try to make our VM is vulnerable as possible. We will start by removing the firewall inbound and outbound rules on the VM , whilst also disabling windows defender. I will also be changing the inbound rules on AZURE to accept any incoming IP's trying to connect to us. As stated earlier we want as many people as possible to try and connect to our machine so we can populate our sentinel world map.

Disabling VM Firewall: <br/>
<img src="https://i.imgur.com/vcBTCB8.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

Custom Inbound Rules To Allow Everyone: <br/>
<img src="https://i.imgur.com/UdtBds3.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

<h3>Creating Custom Fields For Logs</h3>


here we will.. With disabling firewall we wont be able to reach our machine e.g...

Third-Party API We Will Use: <br/>
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

<h3>Creating Custom Fields For Logs</h3>


here we will.. With disabling firewall we wont be able to reach our machine e.g...

Settings up Fields: <br/>
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
Exanole: <br/>
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

<h3>Setting up Sentinel To Map Data</h3>


here we will.. With disabling firewall we wont be able to reach our machine e.g...

Settings up Fields: <br/>
<img src="" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
