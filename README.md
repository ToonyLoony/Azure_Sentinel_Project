<h1>Azure Sentinel (SIEM) Live Attack Project</h1>

<h2>Description</h2>
In this project we will create a VM which is purposely vulnerable to entice attackers to try brute force our VM(virtual machine), creating essentially a 'Honeypot'. These attacks will then be logged in our 'Windows Event Viewer', which we will then feed to a third-party API by using our custom Powershell Script.
<br />
<br />
The Powershell script will extract the 'Failed Remote Login (eventId:4625)' data from the 'Windows Event Viewer' and forward it to a third-party API which will then derive further geolocation data such as the 'Country, Longitude, Latitude' and store it in a new log file. Once done we will reference this new log file in our Azure log analytics workspace and create custom fields.
<br />
<br />
Lastly, we will have Azure Sentinel (Microsoft's cloud SIEM) workspace configured. This will be connected to our log analytics workspace, allowing us to have a relation to our 'failed RDP attack data'. With this we can use Azure Sentinel to visualise our global attack data on a world map, to give us a clear image of where the attacks are coming from.


<h2>Utilities Used</h2>

- <b>Microsoft Azure Suite</b>

<h2>Environments Used </h2>

- <b>Windows 10 Pro(VM)</b> 




<h2>Project Walk-Through</h2>

<p align="center">
  
<h3>Setting up VM,Log Analytics & Sentinel Workspace</h3>

<b>Creating VM:</b> <br/>
<img src="https://i.imgur.com/UTXviQy.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

<b>Creating Log Analytics Workspace:</b> <br/>
<img src="https://i.imgur.com/Hlii8m1.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<b>Creating Sentinel Workspace:</b> <br/>
<img src="https://i.imgur.com/SZTzMzL.png" height="80%" width="80%" alt="NessusLab"/>
<br />
<br />
<br />

<h3>Making Our Machine Vulnerable (HoneyPot)</h3>

After all the basic setup is done we will now try to make our VM is vulnerable as possible. We will start by removing the firewall inbound and outbound rules on the VM, whilst also disabling windows defender. I will also be changing the inbound rules on AZURE to accept any incoming IP's trying to connect to us. As stated earlier we want as many people as possible to try and connect to our machine so we can populate our sentinel world map.

<b>Disabling VM Firewall:</b> <br/>
<img src="https://i.imgur.com/vcBTCB8.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

<b>Custom Inbound Rules To Allow Everyone:</b> <br/>
<img src="https://i.imgur.com/UdtBds3.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<h3>Creating Powershell Script & Using API</h3>

<b>Third-Party API We Will Use:</b> <br/>
<img src="https://i.imgur.com/z1BhZWw.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<b>Inputting API Key into Our Script:</b> <br/>
<img src="https://i.imgur.com/tXTlyIq.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<b>Testing Script:</b> <br/>
<img src="https://i.imgur.com/y9VJCtF.jpeg" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
Here I made a failed login attempt on purpose. As you can see from the image the API returned further geological data of the attacker and stored it in failed_rdp.log.
<br />
<br />

<h3>Creating Custom Fields For Logs</h3>

Next, we'll go back to our Azure log analytics workspace and reference our new log file. So to put it simply we will be bringing the new custom log that has our API data on it from our VM and syncing it with our log analytics workspace :)

We will also be creating some custom fields so we can accurately populate each field for visualization.

<b>Settings up Custom Log Path:</b> <br/>
<img src="https://i.imgur.com/G8IsT6U.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<b>Creating Fields:</b> <br/>
<img src="https://i.imgur.com/WSls7fk.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />
<b>Finished Result:</b> <br/>
<img src="https://i.imgur.com/rWjIoLu.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

Now the log analytics has successfully synced up with our VM and we have set our custom log fields. I once again performed another failed remote login from my Host Machine and from the results above you can see the custom fields separated the data nicely.

<h3>Setting Up Sentinel To Map Data</h3>

In this step, we will need to create a new custom workbook where we will run a log query to gather our information to plot on the map. 

Creating Azure Sentinel Workspace: <br/>
<img src="https://i.imgur.com/Zggef86.png" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

Log Analytics Query: <br/>
<img src="https://i.imgur.com/D4S7fvP.png)" height="80%" width="80%" alt="SIEM_Lab"/>
<br />
<br />

Configuring Map Settings: <br/>
<img src="https://i.imgur.com/U9hchoI.png" height="50%" width="50%" alt="SIEM_Lab"/>
<br />
<br />


<h3>END RESULTS (SUMMARY)</h3>

<h4>Results</h4>
<img src="https://i.imgur.com/mEV3zux.png" height="80%" width="80%" alt="SIEM_Lab"/>
Now I will preface by saying I did not advertise the VM's IP at all. I had the script run on the VM for a day and as you can see thousands of login attempts were made from all around the world! It demonstrates just how important firewalls and security measures are!

From the results, Japan and Russia are essentially tied with the most login attempts, albeit Russia just taking the 1st place medal. The results are highly intriguing I honestly didn't expect to have nearly 200 login attempts from Iran, whilst even more bizarre having a single login attempt from someone in Trinidad and Tobago!
<br />
<br />
<h4>(Edit)Updated Results</h4>

So I forgot to close down my workspaces and shut down my VM so I proceeded to do so to avoid being charged more money. I took the liberty to have one final look at the map 2 days later and these are the results!

<img src="https://i.imgur.com/bWfq0ml.png" height="80%" width="80%" alt="SIEM_Lab"/>
As you can see Russia now wins by a milestone, with Belize coming out of nowhere and taking 2nd place! It really demonstrates that hackers can be anywhere in the world  
<h3>Excessive use Of Administrator</h3> 

<img src="https://i.imgur.com/K7Me8Q9.png" height="80%" width="80%" alt="SIEM_Lab"/>
Probably the biggest thing i noticed was that 'Administrator' was the most commonly used username. Again this demonstrates just how important it is to avoid using default credentials or commonly used usernames like 'Admin' 'Administrator'
<br />
<br />
<h3>How To Prevent?</h3>

In this section, we will quickly look at how we might remediate these issues

The most important step we must take first is ensuring our firewall is set up and configured correctly. As demonstrated earlier if your firewall settings are disabled it is only a matter of time before hackers/bots will find you and try any attack vector possible to gain a foothold in your system. 

Next, from the results, we can see that the same IP is trying hundreds and thousands of times to log in. To stop this we could set up a script to only allow a certain amount of attempts to be made. This will prevent multiple attempts with the same IP.

As conveyed early 'Administrator' was the most commonly used username when hackers tried to brute force our VM. With this knowledge, we should avoid using common/basic usernames such as 'Admin' or 'Administrator.

Lastly, in case the attacker does guess the username & password we could try to set up something like 2FA. This will add another layer of security to our clients and ourselves.
