# <h1>Microsoft Sentinel and ChatGPT Integration</h1>

<h2>Description</h2>
This project includes the deployment and network configuration of Azure Cloud resources to create a vulnerable machine for Microsoft Sentinel to monitor and log incidents. Integrates ChatGPT into playbooks to include auto generated tasks with reccomended remediation steps. Finally, included is the configuration of Azure AD (Entra ID), watchlists, analytic rules, and user and entity behavior analytics (UEBA).
<br />


<h2>Utilities and Repositories Used</h2>

- <b>[Azure](https://azure.microsoft.com/en-us)</b>
- <b>[ChatGPT](https://chat.openai.com/)</b>
- <b>[Sentinel](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/Sentinel-All-In-One)</b>
- <b>[ChatGPT Playbook](https://github.com/format81/MicrosoftSentinel-ChatGPT-playbook)


<h2>Environments Used </h2>

- <b>Microsoft Azure</b> 

<h2>Program walk-through:</h2>

<p align="center">
Deploy Sentintel to Azure <br/>
<br />
I start by using the github repository provided for Sentinel and deploy to Azure. I name my instance SEC-Monitoring and add the following options before deploying Sentinel:<br />
<div align="center">

  <b>[Initial Settings](https://imgur.com/a/0WixhPy)</b>

</div>
<img src="https://i.imgur.com/FwwJ5nn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<p align="center">
Adding Diagnostic, Analytics, and Playbook Rules: <br/>
<br />
Fist I set up a diagnostic rule to have my logs sent to my workspace. I add the following options:
<br />
<br />
<img src="https://i.imgur.com/5jdpCop.png" height="80%" width="80%" alt=""/>
<br />
<br />
<p align="center">
Install Git and then T-pot Configuration: <br/>
<img src="https://i.imgur.com/P8AhxEi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Connect to the Machine via Browser <br/>
<img src="https://i.imgur.com/GtSlmOw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Navigate to the Attack Map: <br/>
<img src="https://i.imgur.com/c6FhMBN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Navigate to Kibana and Open the T-pot Dashboard  <br/>
<img src="https://i.imgur.com/il5mpbC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/WL3UiuU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
You Can Research Some of the Provided CVE's From the Dashboard:  <br/>
<img src="https://i.imgur.com/8nKIgcO.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select an IP address of an Attacker and Navigate to Spiderfoot to Scan for Further Information:  <br/>
<img src="https://i.imgur.com/WmfqYRL.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/ymF8dbI.png?1" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
