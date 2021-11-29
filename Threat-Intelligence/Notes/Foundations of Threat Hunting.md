# Threat Hunting

Threat Hunting is the hypothesis-driven proactive detection of malicious activity. 

In a nutshell TH is: 
- proactively identifying threats in our networks and systems,
- finding threats that already compromised our environment, and
- detecting advanced threats which evade our existing solutions.

You first beed to start by creating a hypothesis. The you Investigate

# Creating a Hypothesis.

Hypotheses are analytic questions that define the focus of the threat hunt, such as detecting a specific threat actor, tool, or technique. So, in this step, threat hunters ask questions, such as _"how would a threat actor infiltrate our network?"_ These questions must be broken down into specific and measurable hypotheses that describe the threats that may exist in the network and how they can be detected.

A hypothesis must be testable, which means that threat hunters must have:

- The required data visibility.
- Know the TTPs to test hypotheses 
- Detailed steps prescribing how to implement an adversary technique.

There are Three hypothesis creation types.

### 1. Intelligence-driven hypothesis. 

Threat intelligence can help threat hunters construct hypotheses by providing a foundation for the questions they ask. 
In this approach, threat hunters create hypotheses based on threat intelligence, such as Indicator of Compromises (IOCs) or Tactics Techniques and Procedures (TTPs). 

Here are two best practices for this approach: 
- The first one is avoiding over-reliance on IOCs. You could become overburdened with low-quality matches if you try to create a hypothesis that requires analysis of every data in a feed or every IOC in an intelligence report. Instead, use IOCs for quick wins but move up the **Pyramid of Pain** to understand adversary TTPs. 
- The second best practice is that hypotheses should be based on TTPs with additional context provided by assessments of the threat and geopolitical landscapes.

An example hypothesis based on threat intelligence about a threat actor is that _"I know that the Hafnium Group is a high priority threat for my organization because of our location and industry. If this threat actor is present in our network, we should be able to detect evidence of multiple techniques used by the Hafnium Group, consistent with their known attack paths"._

### 2. Situational awareness based hypothesis. 

The second hypothesis creation approach is the situational awareness driven hypothesis. According to this approach, defenders must be aware of their surroundings and be able to identify when it changes significantly. Analysts can develop hypotheses about adversary activities that might occur in their environment if they have situational awareness. 

- The first best practice around the situational awareness hypothesis is that focusing on the most critical assets and information. In order to identify important assets, you can use the **Crown Jewels Analysis** technique. 
- Situational analysis requires keeping up with rapidly changing infrastructure, applications, and vulnerabilities. As the second best practice, use automation, particularly in dashboarding, reporting, and risk scoring, to keep up with this rapidly changing environment.

Let's create a situational awareness driven hypothesis. I will limit my search to just high-value targets identified with Crown Jewels Analysis, and domain admin accounts are included in these high-value targets. My hypothesis is _"if attackers abuse domain admin credentials in our network, we should be able to detect outliers like a spike in domain admin account logons."_

### 3. Domain expertise driven hypothesis creation. 

This approach is related to the hunter's domain expertise. Of course, each hunter has a unique set of experiences and skills that influence their hypothesis generation.

As mentioned in the situational awareness approach, a good hunter should have knowledge of both the organization's network and the threats faced. So, domain expertise can be viewed as both cyber threat intelligence and situational awareness in a historical context.

It is obvious that experience is very useful for hunting. However, experience often comes with an unwanted side effect, **bias**. Hunters need to be aware of cognitive biases to ensure good decisions are made and accurate conclusions are drawn. As a best practice, models like the Diamond Model of Intrusion Analysis can be used to overcome bias by structuring threat data.

![image](https://user-images.githubusercontent.com/58165365/143830590-e2548eeb-c945-4c5e-8851-c2334ac2f880.png)

______________________________________________________

Now, we will create a hypothesis. As a kick-start method, I choose to create a hypothesis around a most likely threat actor. Suppose we have a threat intelligence indicating the **MuddyWater threat group** is targeting companies in our industry and country.
So, my hypothesis is, _"according to a new threat intelligence, the MuddyWater APT group is targeting telecommunication companies in Europe. So, MuddyWater is a high-priority threat for my organization. If the MuddyWater group is present in our network, we should be able to detect evidence of multiple techniques used by the MuddyWater group, consistent with their known attack paths."_

Not that we should know TTPs used by the MuddyWater group to test our hypothesis. So, how can we learn these TTPs used by the MuddyWater  group? MITRE ATT&CK provides techniques and tools used by hundreds of threat groups.  ATT&CK also provides descriptions of techniques, as you can see in screenshots. 

![image](https://user-images.githubusercontent.com/58165365/143837936-ac892b61-8dc1-4177-bf28-2c4b952eab6d.png)
![image](https://user-images.githubusercontent.com/58165365/143838074-09846b42-c548-4183-a6fd-348d1258b5d3.png)

However, knowing the definition of a technique is not enough to form a hypothesis. An attack technique can be implemented by using multiple procedures. A procedure is a step by step instruction on how the attacker implements a technique in detail. The threat hunter must know the specific procedure to test the hypothesis. Still, we need to know specific procedures used by the MuddyWater group.

Threat Libraries of Breach and Attack Simulation (BAS) tools provide specific procedures used by a threat group to implement the attack technique. For example, the first screenshot shows actions of an adversary emulation playbook, also known as attack scenario, of the MuddyWater threat group. The MITRE ATT&CK technique of the marked attack scenario action is `"Modify Registry"`. `"Registry Ru, Keys / Startup Folder"` is also an appropriate MITRE ATT&CK sub-technique for this action. Its procedure is that "creating a new registry key named **WindowsDefenderUpdate**  in HKLM hive. 

![image](https://user-images.githubusercontent.com/58165365/143839113-19ff5bda-f524-4469-86ef-7e342d872871.png)


The second screenshot shows the detail of the action. According to its description, the MuddyWater group uses the **reg.exe**  command-line utility to create a new registry key in the HKLM hive for persistence. So, this BAS Threat Library provides detailed descriptions of adversary behaviors.

A comprehensive BAS library like Picus provides adversary emulation playbooks of threat groups, their malware, and their attack campaigns. These playbooks  help you to find TTPs of threat groups.
_______

Now, we know the specific actions of MuddyWater. But, we cannot hunt all actions at once in a big hypothesis. So, we need to create sub-hypothesis utilizing an adversary action. In our example, the MuddyWater threat group creates a new registry, run key named `"WindowsDefenderUpdater"` to maintain persistence. Accordingly, our sub-hypothesis is that _"the MuddyWater Group added a new Registry Run Key named WindowsDefenderUpdater through reg.exe command-line utility in our Window systems to preserve persistence."_ 

(In this sub-) hypothesis, we use 3 MITRE ATT&CK techniques.
- The first one is "Modify Registry", since we are adding a new entry to the registry. 
- The second technique is "Registry Run Keys / Startup Folder", because we add a new entry to the registry run key to maintain persistence.
- The third technique is Masquerading, because the name of the entry WindowsDefenderUpdater that seems like a legitimate name, but it is not. There is not a legitimate service named "WindowsDefenderUpdater" in Windows. 

![image](https://user-images.githubusercontent.com/58165365/143842914-97ea5d0a-2939-4cc0-96df-2ae08531ad81.png)

Until now, we learned that the process name that can be used in the search query is "reg.exe",  the registry operation is "add", and the name of the new registry entry is "WindowsDefenderUpdater".  Our example is a well-defined procedure, so we can easily create the search query. However, most of the time, it was not simple as in this example. Especially, ambiguous queries may result in false positives.

Some BAS platforms provide vendor-specific or vendor-agnostic search queries for adversary actions. For example, you can see that the specific search query named"persistence viaWindowsDefenderUpdaterautorun key" for IBM Radar SIEMin the screenshot. You can use the search query to hunt for this adversary action.

![image](https://user-images.githubusercontent.com/58165365/143843025-7febbb98-46ba-4f75-b5db-73bfc6046eb9.png)

# Investigate Via tools & techniques

Now, we have a hypothesis, and we know how to test this hypothesis; In other words, we have the search query. In this step, the hypothesis is investigated using a variety of tools and techniques. The goal of the step is to prove or disprove the hypothesis. So, we hunt the threat in this step.

Prior to hunting, we need to do three important checks: 
- Which data sources we need? 
- Do we have the required data visibility?
- Do we have the required historical data for hunting?

_____

Let's start with the first check, "which data sources we need?" 

MITRE ATT&CK provides the names of the high-level data sources required to detect or hunt the ATT&CK technique or sub-technique.  For example, MITRE ATT&CK gives `Command Execution`, `File Modification`, `Process Creation`, `Windows Registry Key Creation`, and `Windows Registry Key Modification` as data sources to detect the Registry Run Keys / Startup Folder sub-technique. 

Still, we need to do additional research on the data sources for the specific procedure or adversary action that we are hunting for.

![image](https://user-images.githubusercontent.com/58165365/143844078-8351bc84-0a22-4c1a-974d-4ed0cdf304af.png)

Fortunately, a BAS Detection Library, also provided  detailed information about required data sources to hunt a specific adversary action or procedure. As seen in the screenshot, we can use **"Audit Process Creation"** logs, and we should also enable **"Include Command Line"** option for these logs. So, we know the right log source with the right level of detail now. 

![image](https://user-images.githubusercontent.com/58165365/143844171-87943098-c060-40d0-b55e-3b95c4281db3.png)

The second check is "do we have the required data visibility?", and the third check is "do we have the required historical data for hunting?". 

![image](https://user-images.githubusercontent.com/58165365/143844354-a3856a0f-8d26-42a5-ac15-97b5fcd8e9b3.png)

These checks are related to the collection of required logs. If we don't have the relevant logs, we cannot hunt a threat. The Detection Analytics feature of a BAS tool, helps you to validate that the required logs are collected to hunt the adversary action.

______________

Now, we know the required search query for hunting,and we have the required data visibility, in other words, relevant logs. So, we can start the threat hunt.

Let's remember the components of our search query. We are searching for the "reg.exe" process, registry add operation, "WindowsDefenderUpdate"   as the name of the new entry. 

We can hunt this adversary action in SIEMs and also EDRs, since this action occurs on endpoints. As an example, this query was run on Carbon Black EDR. As shown in the screenshot, the EDR found logs about the search query. Let's look at the first log.

![image](https://user-images.githubusercontent.com/58165365/143845542-58a11109-2abe-4e93-9ff6-b4097a717aeb.png)

Let's look at the first log. According to the log, a new entry was added to the `HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run`  run registry key. The name of the new entry is `"WindowsDefenderUpdater"`. So, we proved our hypothesis. We find a malicious action used by MuddyWater, for persistence. 

If we cannot find any result, in other words, if we cannot prove our hypothesis, we should think about its reasons. Maybe this threat exists in our environment, but we wouldn't find it due to a tool or data constraints. Maybe our search query was wrong. Or, this threat really does not exist in our environment.

![image](https://user-images.githubusercontent.com/58165365/143845312-e432d5b3-5b32-4aec-8213-d629fdd2f398.png)

Until now, we created a hypothesis, investigated with a search query, and find the malicious action used by MuddyWater for persistence. So, we proved our hypothesis. Now, we should pass this information to the Incident Response team.

![image](https://user-images.githubusercontent.com/58165365/143845442-f81a7905-56d2-437d-b814-51eac3e2d15d.png)

# Uncover New Patterns and TTPs

After hypothesis generation and investigation, we found the TTP we were searching for in our environment, but it does not end our threat hunt. We have completed two steps and we must complete two more steps.

The third step is "uncover new patterns & TTPs". If you encounter a malicious pattern or a new TTP, first, you should put a boundary on the hunt. You should not hunt for this TTP. You should document the TTP and open questions and plan a future hunt for this new TTP. 

Moreover, a threat hunt may reveal non-malicious but suspicious or risky configurations or behaviors, such as
- unpatched or misconfigured systems
- logging blind spots.

This information can be passed onto relevant teams, such as SIEM managers, to fill the logging gaps.

________

Let's remember the log the EDR found. We caught a command in the log. We can investigate this command to uncover new TTPs. 

![image](https://user-images.githubusercontent.com/58165365/143849188-dad7acd8-1f7f-4eea-ac93-54cef0a47b19.png)

Let's start with the first step. This command adds a new entry to a registry run key. It includes another command given by the `"d"` parameter, which starts with cmstp.exe. So, this command will run at each system restart. 

Upon system restart, `cmstp.exe` will execute `DefenderService.inf`  file. When we look at the content of the DefenderService.inf file, we found the string starting with `scrobj.dll`,  which you can see in the screenshot.

So, cmstp.exe will execute `Defender.sct` file, which includes an obfuscated `JavaScript`. The main function of the JavaScript code decodes the `Base64` content of another file, `WindowsDefender.ini.` 

WindowsDefender.ini file includes an encoded `PowerShell` script. The JavaScript in the `Defender.sct` file executes the decoded PowerShell script using the command line on the screenshot.

![image](https://user-images.githubusercontent.com/58165365/143849611-c1c61b16-24df-4946-87c4-c4f568fb2a42.png)

So there are other TTPs in the malicious command that we caught in logs during the hunt. As I mentioned before, we should put a boundary on the hunt, which means we shouldn't hunt for these TTPs at the moment. We should document these TTPs and plan future hunts for them.

For example, running a .inf file with CMSTP is a suspicious activity. We can plan a future hunt for it. Another suspicious activity is decoding and running a PowerShell script in a file by using a JavaScript code in another file. We can also plan a future hunt for this action.

![image](https://user-images.githubusercontent.com/58165365/143850583-d0daa276-78b6-4766-99e3-07ceabc9a595.png)

___________

During a threat hunt, we can also uncover logging gaps. For example, we can reveal that some important logs are not collected in SIEMs or EDRs. We can pass these logging gaps to SIEM or EDR managers. It is important to learn logging gaps to increase the efficiency and effectiveness of threat hunting processes. 

Detection analytics feature of Breach and Attack Simulation (BAS) tools like Picus uncovers logging gaps to test the hypothesis and preparing for future hunts.

![image](https://user-images.githubusercontent.com/58165365/143851121-b371ec3c-7dc0-45a0-8a8e-4e6c4268d491.png)

Picus also visualize technique-based logging gaps on the MITRE ATT&CK framework.

![image](https://user-images.githubusercontent.com/58165365/143851309-b9b3a07f-f8ab-4554-85af-93e0348678e2.png)

# Inform and Enrich Analytics

In this last step, we operationalize the current hunting process before starting a new hunt. 

We shouldn't hunt for the same threat over and over. If possible, we should convert search queries of the current hunt into new automated detection rules. Threat hunters can work with detection engineers to detect the hunter threat in the future. In this way, the threat you hunt can now be detected automatically by detection tools, and you won't have to manually hunt for the same threat in the future. So, you can find more time to test new hypotheses.

Even if you cannot convert search queries into automated detection rules, you should save the search query and schedule it to quickly repeat hunting in the future.

Picus Detection Library includes vendor-specific detection rules for SIEM and EDR vendors and vendor-neutral Sigma rules. You can utilize these rules to enrich your analytics.

![image](https://user-images.githubusercontent.com/58165365/143852303-e9a9bf0a-65c7-4b65-b575-bbc48f12aeb6.png)

Moreover, you can validate deployed detection rules with the Detection Analytics feature of the Picus Continuous Security Validation Platform. As you can see in the screenshot, we created a detection rule with a search query used in the threat hunt, and Picus validated that the rule works and creates alerts.

![image](https://user-images.githubusercontent.com/58165365/143852431-e9e28071-9a41-4226-9cf5-d268483a3420.png)

# Threat Hunting Maturity Model

![image](https://user-images.githubusercontent.com/58165365/143852928-808df717-7627-4f93-9812-909f3791c4fc.png)

This is the Threat Hunting Maturity Model, which is also developed by Sqrrl. Your aim should be to increase your level of hunting maturity. 

At the level 0, initial,  there is little or no data collection, and our detection relies on automated alerting.  So, we cannot perform threat hunting at this level. 

At level 1, minimal, we can search for low-level threat indicators, such as file hashes, IP addresses, and domain names. 

At the level 2, procedural, organizations can learn and use procedures created by others on a semi-regular basis, and they can make slight changes, but they are not yet capable of developing entirely new procedures. Organizations at this and higher levels have a high level of routine data collection capabilities,

At the level 3, innovative, at least a few hunters exist in this organization who are familiar with a variety of data analysis tools and can use them to detect malicious activities. These organizations are able to establish their own procedures rather than relying on those provided by others. 

At the level 4, leading, in addition to the level 3 skills, organizations use automation. Any effective hunting procedure will be operationalized and converted into automated detection at this stage. Because of the high level of automation, they may concentrate their efforts on developing a continuous stream of new hunting processes, resulting in continuous improvement of the detection program as a whole. 

As you have seen, a comprehensive BAS tool like Picus can help you reach level 4 with its features such as Threat Library, Detection Library, Detection Analytics. You can fill your data collection gaps and build a high level of routine data collection capability. You can write your own data analysis procedures with the help of TTP details and search queries provided by the BAS threat and detection libraries. You can also turn successful procedures into automated detection rules and validate them using the detection analytics technology of a BAS tool.

However, this does not mean you don't need skilled threat hunters if you're using a BAS tool, Threat hunting is one of the most human dependent activities in cybersecurity. We do not eliminate your threat hunter needs; we aim to empower your threat hunters to do their job better and faster, thus enabling more hypotheses to be tested to increase the level of cybersecurity of your organization.

_____________

In conclusion, threathunting is no longer an option but a necessity. A formal threat hunting model helps threat hunters to conduct thorough and focused threat hunting. 

A comprehensive BAS tool, such  as Picus, helps threat hunters in different steps of the threat hunting loop.

- It provides TTPs and their detailed usage by threat actors to support hypotheses creation.
- It also provides required log sources in detail to detect a TTP, and validates the required data visibility to test a hypothesis. 
- Moreover, a complete BAS tool helps organizations to increase their threat hunting maturity.


# Definations and Abreviations Used:

|Word| Explanantion|
|----|----|
|APT|Advanced Persistent Threats|
|TTP|Tactics,Techniques & Procedures|
|Adversary||
|Threat Actor||
|TH|Threat Hunting|
|CTI|Cyber Threat Intelligence|
|IOC|Indicators of Compromise|
|IOA|Indicators of Attack|
|BAS|Breach & Attack Simulation|

# Resources

[Picus Course - Foundations of Threat Hunting]()
[MITRE ATT&CK®](https://attack.mitre.org/)
[MITRE D3FEND™](https://d3fend.mitre.org/)
[]()
