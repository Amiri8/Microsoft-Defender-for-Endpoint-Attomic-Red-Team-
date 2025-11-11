# Microsoft-Defender-for-Endpoint-Attomic-Red-Team
For this project we are going to: 
1. Onboard a VM
2. Create Attack Surface Reduction Rules
3. Enroll an endpoint into Intune
4. Simulate suspocious activity using Atomic Red Team
5. Threat Hunt


# What is Microsoft Defender for Endpoint
Microsoft Defender for Endpoint is a comprehensive enterprise security platform that helps organisations prevent, detect, investigate, and respond to advanced cyberthreats on endpoints like laptops, mobile devices, and servers.

# onboarding a VM 

In the https://security.microsoft.com

Before onboarding we need to enable few options, 
Navigate the following from the left panel `System -> Settings -> Endpoints -> General -> Advanced features`

Enable the following: 
- Enable EDR in block mode
- Enable Live Response
- Microsoft Intune connection
- Enable Custom network indicators
- Enable Web content filtering
- Tamper protection (on by default)



Next we are ready to onboard a VM, in my case I'm using a Windows 11 machine hosted by Azure 
On Microsoft Defender page, navigate to `System -> Settings -> onboarding. Select the operating system as shown in the screenshot and then Download the onboarding package. 
<img width="1875" height="898" alt="Screenshot 2025-11-10 104042" src="https://github.com/user-attachments/assets/89df4700-efa7-4b8e-9e27-66842bb039e4" />

# Install onboarding package on the VM 

After downloaing the onboarding package, we need to RDP into the VM, copy Defender onboarding package into the VM. Extract the file and run the file as Administrator 
<img width="1932" height="840" alt="image" src="https://github.com/user-attachments/assets/90a7c61a-96cc-46ee-84af-fc06eafce455" />


go back in the Defender for Enpoint portal, under 2. Run a detection test we can see a command prompt which we need to copy. 
<img width="1543" height="693" alt="Screenshot 2025-11-10 104307" src="https://github.com/user-attachments/assets/13d4d40d-b1e4-4e0b-9d51-6b94ef0b18d8" />



On the VM open Powershell with privilidge mode and paste the command copied earlier. 


After waiting for a few minutes we can see that the status has changed to `complete`, which means that our VM has been successfuly onboarded to Microsoft Defender for Endpoint

<img width="1179" height="586" alt="Screenshot 2025-11-10 104424" src="https://github.com/user-attachments/assets/fa08b6f8-f5d1-443e-b9cb-f0eb53ad7fb1" />



We can go to `Assets -> Devices` to confirm. 

<img width="1881" height="824" alt="Screenshot 2025-11-10 104521" src="https://github.com/user-attachments/assets/58568dcf-b12e-4180-8427-c52d81e1742f" />



# Attack surface reduction
Attack surface reduction (ASR) rules are a set of security policies designed to block common malware and ransomware behaviors, protecting endpoints from threats before they can cause harm


# Steps:
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


Next parts of this project will be up soon ... 
