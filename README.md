<h1>Azure Sentinel (SIEM) Live Attack Project</h1>

<h2>Description</h2>
In this project we will create a VM which is purposely vulnerable to entice attackers to try brute force our VM. These attacks will then be logged in our 'Windows Event Viewer', which we will then fed to a third party API by using our custom Powershell Script. The Powershell script will extract the 'Failed Remote Login (eventId:4625)' data from the 'Windows Event Viewer' and forward it to a third party API which will gather further geolocation data such as 'Country,Longitude,Latitude etc'. Once done we will have this new logged data referenced in our Azure log analytics workspace, which will have custom fields setup.

Lastly we will have Azure Sentinel (Microsoft's cloud SIEM) workbook configured. This will be connected to our log anayltics workbook, allowing us to have a relation to our 'failed RDP attack data'. With this we can use Azure Sentinel to visualise our global attack data on a world map , to give us a clear image of where the attacks are coming from.

<br />

<h2>Utilities Used</h2>

- <b>Azure Sentinel workbook</b>
- <b>Azure Log analytics workbook</b>

<h2>Environments Used </h2>

- <b>Windows 10(VM)</b> 
