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
