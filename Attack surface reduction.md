# Attack surface reduction
Attack surface reduction (ASR) rules are a set of security policies designed to block common malware and ransomware behaviors, protecting endpoints from threats before they can cause harm


## Steps:
- Inroll the endpoint into Intune

Head to https://intune.microsoft.com/
From the sidebar select `Devices -> Device onboarding -> Enrollment`

<img width="2875" height="1465" alt="Screenshot 2025-11-11 113426" src="https://github.com/user-attachments/assets/c4221e46-00e7-46ab-b5ef-12ca84a759c4" />


For the `MDM user scope` select `All` and click `Save`

<img width="2846" height="1450" alt="image" src="https://github.com/user-attachments/assets/8677ba50-8fe4-4acd-b88b-ae527f001f14" />

Then we need to RDP into the VM. 
Open `access work or school`, click on Connect for `Add a work or school account`. Then select `Join this device to Microsoft Entra ID` and sign in with your test user account. Going forward this VM is going to be jenny@Marscyber.onmicrosoft.com 




Now lets RDP into the Jennys's VM.
Once we are in, in Microsoft Intune admin center select `Devices` and under `Windows` section we should see a device connected.

<img width="2876" height="1456" alt="image" src="https://github.com/user-attachments/assets/8e2301ad-7b3d-4900-b854-394404d8922d" />

In the `Endpoint security -> Setup -> Microsoft Defender for Endpoint` and turn the following settings on and save

<img width="2568" height="1458" alt="image" src="https://github.com/user-attachments/assets/9531ac4b-4cd4-4f56-86e4-602727168703" />




Now we can push out policies to our endpoints to automatically onboard onto Microsoft Defender for Endpoint or configure policies for additional protections, which is covered in next section


# Configure ASR rules in Intune
Now lets create an ASR policy in Intune:
Go to Endpoint `security -> Attack surface reduction` click on `Creat Policy` and select the following example settings:

<img width="2879" height="1463" alt="Screenshot 2025-11-11 115815" src="https://github.com/user-attachments/assets/4d4f8090-6736-4293-8338-358ea4097958" />

<img width="1576" height="1440" alt="image" src="https://github.com/user-attachments/assets/b074b17b-e119-4c5b-bbb8-a607d5bfdbf5" />
<img width="1862" height="1460" alt="image" src="https://github.com/user-attachments/assets/11d2a146-a5a1-473c-98b0-361b93eb3694" />

These policies can be applied to only groups. You can either select the `group` from the drop down or create a `custom group` by clicking on Groups in the left side bar.


To determine, if the policy was applied successfuly just click into the policy
<img width="2136" height="1478" alt="image" src="https://github.com/user-attachments/assets/830767a3-ba97-4a0c-880e-9427a5f63007" />
