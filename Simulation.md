# Simulate and hunt an activity
##  Goal 
- Run Atomic Red Team tests for  MITRE ATT&K technique T1197 - BITS Jobs on test VM and forward logs to Defender.
- Create a hypothesis and hunt for Atomic Test #4 - Bits download using desktopimgdownldr.exe (cmd)

## Simulation
Simulated Atomic Test #4 - Bits download using desktopimgdownldr.exe (cmd):

```
Invoke-AtomicTest T1197 -TestNumbers 4 -ShowDetailsBrief

Invoke-AtomicTest T1197 -TestNumbers 4
```
<img width="1874" height="1118" alt="Screenshot 2025-11-17 125900" src="https://github.com/user-attachments/assets/36abccf0-5e61-484f-9e7c-6921c0498178" />


desktopimgdownldr.exe is a legitimate Windows binary used by the Personalisation/lockscreen feature to fetch images (desktop or lock screen backgrounds) from a URL or Microsoft service. In normal use it is called with a /lockscreenurl: (or similar) pointing to a trusted image (jpg/png) on Microsoft CDNs or vendor CDNs, and the BITS service (running as svchost.exe -k netsvcs -s BITS) performs the actual download and saves the image to the Personalization/LockScreenImage folder. Attackers abuse it by supplying an arbitrary URL (pointing to a malicious .exe or script), so suspicious desktopimgdownldr invocations followed by svchost outbound connections to non-Microsoft domains likely indicate abuse.

## Hypothesis 
Unusual `desktopimgdownldr.exe /lockscreenurl:` invocations that reference non-Microsoft or non-image URLs and are followed (within minutes) by svchost.exe -k netsvcs -s BITS network activity to those same hosts indicate likely abuse of the BITS download flow to fetch arbitrary/malicious files.


## Investigation 

on Nov 17, 2025 12:57:51 PM Local Time a command with `desktopimgdownldr.exe /lockscreenurl:` refrencing a  URL to download GitHub raw .md file (not an image or Microsof service) was executed on host Win-11-VM-2 indicating it is a test or abuse rather than normal behavior.

The results partially support my hypothesis because telemetry was only generated for DeviceProcessEvents in Defender and logged the following events.


```
DeviceProcessEvents
| where InitiatingProcessCommandLine contains "desktopimgdownldr.exe"
| sort by TimeGenerated asc
| project-reorder TimeGenerated, InitiatingProcessCommandLine, DeviceName, InitiatingProcessFileName, FileName, InitiatingProcessFolderPath
```


<img width="2872" height="1452" alt="Screenshot 2025-11-17 131546" src="https://github.com/user-attachments/assets/9d463bb6-dc4e-4e99-9780-7cf10c2bc6d3" />



## Recommendations
Investigate the following:

- Was URL malicious and what was downloaded on the host machine.
- Did anyone else browsed to the URL
- Block the URL
