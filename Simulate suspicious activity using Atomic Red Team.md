# Simulate suspicious activity using Atomic Red Team
My goal is to simulate suspicious activity on our test VM using Atomic Red Team which is a popular Red Canary project that mimics real adversary behaviour so we can test endpoint detections. I want to trigger alerts in Microsoft Defender for Endpoint and observe how it responds. 

## Installing Atomic Read Team 
Before installing we need to make an exclusion and select folder `C:\` drive. To do that we need to RDP into the VM, 
Go to `Windows Security` -> `Virus & threat protection` -> `Manage settings` -> `Exclusions` -> `add or remove exclusions` -> `click on Add an exclusion` -> Select `Folder` and add your `C:\` drive here
Then for installation we need to open Powershell as an admin, and run this command:

`Install-Module -Name invoke-atomicredteam,powershell-yaml -Scope CurrentUser `
<img width="2358" height="1064" alt="image" src="https://github.com/user-attachments/assets/883c0a23-9244-4b35-8380-ed2592ecbca6" />

Next we need to paste this command to install the Atomic-Red-Team, then we can see the Atomic forlder in C drive. 
`IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing); Install-AtomicRedTeam -getAtomics`

<img width="2252" height="1176" alt="image" src="https://github.com/user-attachments/assets/e97cc011-f6ae-489c-a8d5-3dbd260cbf16" />

Under the Atomic folder we can see some MITRE techniques
<img width="2256" height="1176" alt="image" src="https://github.com/user-attachments/assets/315425e7-672a-40a1-a15e-26ae7f0e1944" />


Let's pick T1547 Technique and specifically 001 technique, to do that we run the following command

`Invoke-AtomicTest T1547.001`

Let's take a look at Defender before and after the atmoic red team. 

Before: 

<img width="1911" height="896" alt="Screenshot 2025-11-10 120953- before atomic was deployed" src="https://github.com/user-attachments/assets/6c4bfdc6-1076-4960-aa1e-f06b2f763471" />


After:

<img width="1892" height="911" alt="Screenshot 2025-11-10 121449-after-atomic" src="https://github.com/user-attachments/assets/5c20b69b-121b-4a1d-ac1b-ac822cf3a0e3" />

As you can see this has generated many alerts for us. 

