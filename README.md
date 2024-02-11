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
Deploy Sentintel to Azure<br/>
<br />
<br />
<br />
I start by using the github repository provided for Sentinel and deploy to Azure. I name my instance "SEC-Monitoring" and add the following options before deploying Sentinel:<br />
<div align="center">

  <b>[Initial Settings](https://imgur.com/a/0WixhPy)</b>

</div>
<p align="center">
<img src="https://i.imgur.com/FwwJ5nn.png" height="80%" width="80%" alt="setup"/>
<br />
<br />
<br />
<p align="center">
<b>Adding Diagnostic, Analytics, and Watchlist Rules:</b><br/>
<br />
<br />
<br />
Fist I set up a diagnostic rule to have my logs sent to my workspace. I add the following options:
<br />
<br />
<img src="https://i.imgur.com/5jdpCop.png" height="80%" width="80%" alt="diagnostic rule"/>
<br />
<br />
<p align="center">
I now navigate to the settings and enable UEBA to make use of AI to assist in flagging possible threats and logging incidents.<br/>
<br />
<img src="https://i.imgur.com/ZLOaSbI.png" height="80%" width="80%" alt="UEBA"/>
<br />
<br />
I also provide the workspace with playbook permissions so that Sentinel automation rules can run.<br/>
<br />
<img src="https://i.imgur.com/DrieWVi.png" height="80%" width="80%" alt="permissions"/>
<br />
<br />
I will now create the first Watchlist, this list will be used to watch for TOR IP addresses. The IP addresses have been uploaded from a .csv file. The Search key was named IpAddress to increase query performance<br/>
<br />
<img src="https://i.imgur.com/c7zkodc.png" height="80%" width="80%" alt="Watchlist"/>
<br />
<br />
Moving on to analytics, I will now create a new scheduled query rule. I name it "Successful Sign-ins from Tor Network". I utilized ChatGPT to provide me a description using the following prompt: "can you give me a description of this Microsoft sentinel analytics rule? Successful sign-ins from Tor Network"<br/>
<br />
<br />
<img src="https://i.imgur.com/yZICcNG.png" height="80%" width="80%" alt="Analytics rule"/>
<br />
<br />
Moving on to the "Rule Logic" tab. Using KQL I created a query to provide me with specific information when an incident has been logged. This will ensure I recieve relevant data for faster and more thorough analysis.
The rule has also added entities to assist in providing more specific data such as display names, and IP addresses. The query is scheduled to run every five minutes.<br/>
<br />
<br />
<img src="https://i.imgur.com/cYdwlL2.png" height="80%" width="80%" alt="Analytics rule1"/>
<img src="https://i.imgur.com/EvXSVVj.pngg" height="80%" width="80%" alt="Analytics rule2"/>
<br />
<br />
Alert grouping was then enabled to group matching alerts with matching IP addresses and names into the same incident. More than 150 alerts will result in a new incident being created.<br/>
<br />
<img src="https://i.imgur.com/i93ZPNS.png" height="80%" width="80%" alt="alert grouping"/>
<br />
<br />
<br />
<p align="center">
<b>Disabling Security Features, Adding New Users and Creating Incidents:</b><br/>
<br />
<br />
<br />
I first disable security settings provided by Azure AD to allow for weaker passwords, password spray attacks, and much more to occur.<br/>
<br />
<img src="https://i.imgur.com/BCgXKno.png" height="80%" width="80%" alt="disable security settings"/>
<br />
<br />
I then create a new account that will act as the bad actor, I give it the user principal name of "Haru". I auto generate the password and then enable the account. The account is then assigned the "Security Reader" Role on Azure AD and in the "SEC-Monitoring" resource group it is assigned "Contributor"<br/>
<br />
<img src="https://i.imgur.com/cXgLu52.png" height="80%" width="80%" alt="account creation"/>
<img src="https://i.imgur.com/QWy30ia.png" height="80%" width="80%" alt="role assignment"/>
<br />
<br />
I use the "Brave" internet browser to log with the bad actor account because it has a private TOR browsing feature. When logging in using the auto generated password it prompts me to change it again, so I used a commonly used password attempted in breaches "7ujMko0admin", this password was discovered in the Honeypot project I conducted prior to this. We are then logged into Azure with the bad actor account and are ready to behave like an attacker.<br/>
<br />
<img src="https://i.imgur.com/GCAATnh.png" height="80%" width="80%" alt="role assignment"/>
<br />
<br />
I proceed to the resource group for "SEC-Monitoring" and then navigate to the diagnostic settings. I disable the settings I created earlier, I then also disable the diagnostic settings and the "Health Settings" in Sentinel.<br/>
<br />
<img src="https://i.imgur.com/Beg2dFR.png" height="80%" width="80%" alt="security disable"/>
<img src="https://i.imgur.com/aW4uLtl.png" height="80%" width="80%" alt="security disable2"/>
<br />
<br />
After disabling the security settings, I then proceed to create a new VM from where I can run powershell from. Once its finished deploying, I run powershell and let it sit for approximately 40 minutes.<br/>
<br />
<img src="https://i.imgur.com/sIIXsJ7.png" height="80%" width="80%" alt="VM"/>
<br />
<br />
<br />
<p align="center">
<b>Incident Analysis:</b><br/>
<br />
<br />
<br />
Now that Incidents and have been generated I can now conduct analysis to find information such as IP addresses, location, and authenitcation requirements.<br/>
<br />
<img src="https://i.imgur.com/dRRiEzF.png" height="80%" width="80%" alt="Incidents"/>
<img src="https://i.imgur.com/9alVdcr.png" height="80%" width="80%" alt="Incidents"/>
<br />
<br />
We can see that IP addresses have been using "Haru" to log in. We can see that the IP addresses are coming from different parts of the world. This one in particular is from Austria and has been reported in multiple web attacks.<br/>
<br />
<img src="https://i.imgur.com/9alVdcr.png" height="80%" width="80%" alt="Incidents"/>
<img src="https://i.imgur.com/kM6iKw7.png" height="80%" width="80%" alt="Incidents"/>
<br />
<br />
I can edit the query created for the rule logic to see all past logins for the account to see what past activity for this account may have looked like. This would be useful information when doing analysis in an enterprise enviornment. When navigating to "Entity Behavior" we can search Haru and then have it display things such as Alerts, Anaomalies, and Azure activities.<br/>
<br />
<img src="https://i.imgur.com/J1kyA4w.png" height="80%" width="80%" alt="query edit"/>
<img src="https://i.imgur.com/RwNM2Q8.png" height="80%" width="80%" alt="entity behavior"/>
<br />
<br />
<br />
<p align="center">
<b>Incident Remediation:</b><br/>
<br />
<br />
<br />
Now that I have gathered evidence of suspicious activity that would be considered malicious, I then proceed to deactivate the account in order to stop more incidents from occuring. The Virtual Machine is also deleted next. From the logs I can see that the account deleted Analytic rules and diagnotstic settings, so those must be restored. I leave comments to ensure steps are documented.<br/>
<br />
<img src="https://i.imgur.com/h3HxjX8.png" height="80%" width="80%" alt="account disable"/>
<img src="https://i.imgur.com/BPM3Gck.png" height="80%" width="80%" alt="VM deletion"/>
<img src="https://i.imgur.com/y1X6yPY.png" height="80%" width="80%" alt="diagnostic settings restored"/>
<br />
<br />
I now proceed to close the incidents making sure to comment my findings and remediation steps after talking to the owner of the account.<br/>
<br />
<img src="https://i.imgur.com/nXf1dza.png" height="80%" width="80%" alt="incident closed"/>
<br />
<br />
<br />
<b>Playbook Creation for ChatGPT:</b><br/>
<br />
<br />
<br />
Now that we have remeidated the incidents we can create a new Playbook utilizing ChatGPT. I navigtate to "Automation" in Sentinel, then create a playbook with incident trigger. The following settings are used:<br/>
<br />
<img src="https://i.imgur.com/gj4ak3m.png" height="80%" width="80%" alt="playbook Creation"/>
<br />
<br />
Once the Playbook is created, the Logic app designer is opened. From here I will add a new step and then select GPT3, which will then prompt me for an API key. Using ChatGPT I can recieve one free use of the API key generator. I generate the key and enter it in in the Logic app designer.<br/>
<br />
<img src="https://i.imgur.com/o6TJZ7e.png" height="80%" width="80%" alt="logic app"/>
<img src="https://i.imgur.com/jcvW4gh.png" height="80%" width="80%" alt="api key creation"/>
<img src="https://i.imgur.com/dP9A0f6.png" height="80%" width="80%" alt="api submit"/>
<br />
<br />
Once the key is submitted, I add a custom engine as "Davinci-002/3" has been deprecated, instead I use "gpt-3.5-turbo-instruct" as the engine. I then change the max token to 300 so that the auto generated responses have more characters available. For the prompt I add the following to shape the responses ChatGPT will give. This make is so ChatGPT provides a comment on an incident with reccomendedations on how to remediate when the playbook is run.<br/>
<br />
<img src="https://i.imgur.com/BoZSjjy.png" height="80%" width="80%" alt="logic app step1"/>
<img src="https://i.imgur.com/NRcPF95.png" height="80%" width="80%" alt="logic app step2"/>
<br />
<br />
I then assign permissions to GPT to allow to write the comments within Sentinel. This requires that the Playbook be assigned the "Responder" role.<br/>
<br />
<img src="https://i.imgur.com/Ou98SZA.png" height="80%" width="80%" alt="playbook role assignment1"/>
<img src="https://i.imgur.com/0vKNSYw.png" height="80%" width="80%" alt="playbook role assignment2"/>
<img src="https://i.imgur.com/YF8SGrX.png" height="80%" width="80%" alt="playbook role assignment3"/>
<br />
<br />
Now that the Playbook has the appropriate role, I can now run it against an incident. I kept one incident open from earlier and now I can run the Playbook to generate a comment.<br/>
<br />
<img src="https://i.imgur.com/M9kZ7Or.png" height="80%" width="80%" alt="GPT comment1"/>
<img src="https://i.imgur.com/61GESG3.png" height="80%" width="80%" alt="GPT comment2"/>
<br />
<br />
I will now create an automation rule to run the playbook automatically without me needing to run it for an incident manually. I set the trigger to "When an incident is created" and change the action to "Run playbook" and then select the ChatGPT playbook. The order of the rule is changed to "5" I then create a predefined incident to test the automation on. The automation is working as expected.<br/>
<br />
<img src="https://i.imgur.com/fcqDmbS.png" height="80%" width="80%" alt="Automation rule"/>
<img src="https://i.imgur.com/ZFWWlCI.png" height="80%" width="80%" alt="Incident Creation"/>
<img src="https://i.imgur.com/1Y0osBR.png" height="80%" width="80%" alt="Automation comment"/>
<br />
<br />
Using the provided Github repository, I use the provided link to deploy to Azure and create a playbook and name it "ChatGPT-Incident-Enrichment-V2". This will provide a more advanced version of ChatGPT, one that will allow for detailed remediation steps. From there I navigate to the logic app designer and then change the connections the one established when creating the first playbook this will add the previous parameters that were set in the first playbook. Then the max tokens are set to 600.<br/>
<br />
<img src="https://i.imgur.com/Z4ChuWS.png" height="80%" width="80%" alt="GPT2 app1"/>
<img src="https://i.imgur.com/DJjKhIy.png" height="80%" width="80%" alt="GPT2 app2"/>
<br />
<br />
With this set up I now assign the responder role as I previously did and the navigate to instances to run the playbook to see the differences. This version should provide me with detailed steps that should taken to remediate an incident and will even open tasks for me to complete.<br/>
<br />
<img src="https://i.imgur.com/g4S66Nm.png" height="80%" width="80%" alt="comment Generated"/>
<img src="https://i.imgur.com/hIzjCsR.png" height="80%" width="80%" alt="GPT2 app2"/>
<br />
<br />
<br />
<br />
<h2>Conclusion</h2>
<br />
Microsoft Sentinel has been successfully deployed and configured to monitor and log suspicious and malicious activity and has been enhanced through the use of ChatGPT to reccomend steps to remediate the various kinds of incidents that are generated.
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
