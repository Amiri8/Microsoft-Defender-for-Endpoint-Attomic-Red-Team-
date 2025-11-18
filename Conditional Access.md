# Conditional Access 

Create a CA policy if the sign-in is coming from a country that we do not do business with or we don't trust. In this case block the access entirely.


- Sign-in with your test user account in Outlook. Once we sign in this will create a sign-in event within Entra ID. This will be used as our legitimate activity. 
- Navigate to https://entra.microsoft.com/. Go to `Monitoring & health -> sign-in logs` and filter on your test user assume this activity to be legitimate from that location and IP.

<img width="2872" height="1162" alt="image" src="https://github.com/user-attachments/assets/fa544e00-e79e-4f39-bcf8-e104f3b6e459" />

## Simulate risky sign-in 
Create a VM in a region different from your test account who logged into Outlook (as above because we will consider that as legit activity). For that purpose we will create a VM in Azure located in East US.



After deploying another Microsoft VM located in East US, I wanted to see what is the IP address of this machine. 
<img width="2790" height="1644" alt="Screenshot 2025-11-12 132714" src="https://github.com/user-attachments/assets/16183e78-96cc-4caf-befd-bd6df0b709e5" />


Now on the US VM, open Outlook and sign-in as our test user (jenny's account) and it asks us for MFA. So here the assumption is that the attacker has acquired Jenny's credentials and when the attacker sign-in, they they will be asked for MFA. 

<img width="1014" height="852" alt="image" src="https://github.com/user-attachments/assets/53f53018-202e-4e76-afe4-953d80d298b3" />


In Entra ID we see the event generated based on above malicious sign-in attempt with IP `20.81.164.176` from Virginia and MFA is enabled. We can get more information by clicking the events and going through different tabs inside it. For example if you click on Conditional Access, you will see an MFA policy called Security defaults applied by default. These are defaults that are enabled for all Entra ID P1 and P2 plans. The control for this policy makes sure that for the sign-in to be successful it must require MFA. When the attacker did not provide MFA, this event became Interrupted, hence the Status is Failure.
<img width="2860" height="1468" alt="Screenshot 2025-11-12 132837" src="https://github.com/user-attachments/assets/8ada29d9-8240-4444-a8e9-ba7a1d76eda6" />

<img width="2224" height="860" alt="image" src="https://github.com/user-attachments/assets/e9649f40-2cc9-437d-8726-0b212c00cf37" />


# Create a Conditional Access policy
Let's create CA policy to block connections from US, as we do not do business with it.
to do this we need to block US, we need to go ` ID Protection -> Dashboard -> Conditional Access -> Named Locations -> Countries location` and search for `United States` and name it, in this case `blocked-countries`. 
<img width="2854" height="1452" alt="image" src="https://github.com/user-attachments/assets/aeafb14e-bef8-48b8-ad15-e40fdfa5703e" />

Then we can create a Policy
Go back to `Conditional Access -> Policies -> New Policy`. 


Name: Create a new policy `Ali's-Conditional-Access-Policy`
Assignments: Select the user(s). 
<img width="2878" height="1436" alt="image" src="https://github.com/user-attachments/assets/c89bacaa-40d9-4d55-960a-4f488c40ee67" />


Target resources: `All resources`
Network: select the following

<img width="2874" height="1466" alt="Screenshot 2025-11-12 133522" src="https://github.com/user-attachments/assets/a75dc9c0-b7c1-492e-a0a7-a3590f7e39e1" />


Conditions: Keep default

Access controls → Grant → select Block access

Enable policy: select `On` and click `Create`
<img width="2878" height="1468" alt="Screenshot 2025-11-12 134902" src="https://github.com/user-attachments/assets/139ca569-db8a-4b32-ac9b-74607c7a6068" />



Now that our CA, policy is in place let's try to log in again with our Jenny's account from m our US VM. Now the access is blocked, and we don't see the MFA prompt because it's sourcing from a blocked country
<img width="2852" height="1676" alt="Screenshot 2025-11-12 134538" src="https://github.com/user-attachments/assets/8e2eb529-3fdc-4f75-91ba-b707c618214a" />
