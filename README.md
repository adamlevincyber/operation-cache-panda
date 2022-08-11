# Operation Cache Panda
Timeframe: [11/2021 - 02/2022]

## Description:
In November 2021, a number of Taiwan financial institutions and securities traders informed the Taiwan Stock Exchange Corporation (TWSE) and the Financial Supervisory Commission (FSC) that they would be suspecting transactions due to suspicious behavior. Unusual large purchases of Hong Kong stocks via Taiwan securities broker customer accounts. Incident response investigations came to the conclusion that the November attacks were due to password mismanagement and credential stuffing; however, this wasn’t 100% confirmed and it is thought that there were more techniques used. After these November attacks, Taiwan shifted their defenses. Then, from February 10-13, Taiwanese financial institutions and securities traders were targeted once again. [CyCraft](https://cycraft.com/) observed login events and files on customer servers and began a investigation. 

### Threat Actor Group:
![image](https://user-images.githubusercontent.com/71887536/184047622-3f0b9406-0dce-4afc-b9e7-484915082855.png)


## Analysis:
This is the QuasarRAT loader, APT10 has used in previous campaigns. First, registers as a service, loading two DLL files, `PresentationFrom[.]dll` and `PresentationStatic[.]dll`. When the executable is launched, it grabs `x86[.]bin` and `DogCheck[.]bin` files from the C2 servers. The shellcode dynamically loads the .NET environment and loads the attacker .NET assembly for later action. `x86[.]bin` is the main part of the backdoor. `DogCheck[.]bin` is the gatekeeper, responsible for checking connection status. `PresentationCache[.]exe` then restarts, ensuring that `x86[.]bin` remains only in memory.

“The current attack targeting Taiwan was codenamed "Operation Cache Panda" and started with exploitation of a web service vulnerability in the security software system management interface. First, the attacker uploaded the ASPXCSharp WebShell commonly used by Chinese hackers to control the website host, and then began to use the well-known penetration tool Impacket to scan intranet computers, trying to implant the DotNet backdoor program on a large scale, and intending to steal the hacked unit data. The attackers then utilized a method known as reflected code loading to execute malicious code on local systems and install a version of the Quasar RAT that provided persistent remote access to the affected system via reverse RDP tunnels. Quasar RAT features include capturing screenshots, recording webcam, editing registry, keylogging, and stealing passwords” [HivePro](https://www.hivepro.com/wp-content/uploads/2022/02/Chinese-APT-group-targets-financial-institutions-in-the-campaign-Operation-Cache-Panda_TA2022040.pdf).



## MITRE ATT&CK TIDs:
![image](https://user-images.githubusercontent.com/71887536/184047870-4e50fecc-ebe8-4215-bb0d-0b92aa6b71c4.png)


## IoCs:

![image](https://user-images.githubusercontent.com/71887536/184047918-fa76c747-b05f-4600-9c78-576ab4fd2595.png)



## Sources:
```https://medium.com/cycraft/smokescreen-supply-chain-attack-targets-taiwan-financial-sector-a-deeper-look-8acf290ddb96
https://cyware.com/news/operation-cache-panda-chinese-apt10-targets-taiwan-9619edf7
https://thehackernews.com/2022/02/chinese-hackers-target-taiwans.html
https://www.hivepro.com/chinese-apt-group-targets-financial-institutions-in-the-campaign-operation-cache-panda/
https://www.hivepro.com/wp-content/uploads/2022/02/Chinese-APT-group-targets-financial-institutions-in-the-campaign-Operation-Cache-Panda_TA2022040.pdf
https://medium.com/cycraft/supply-chain-attack-targeting-taiwan-financial-sector-bae2f0962934
