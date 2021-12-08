# Fundamentals of Modern Log Management Practices

> This course is the first course of the Proactive Security Operations Center (SOC) learning path. By the end of this course, you will have learned about the Log Management process, primary log sources, prioritization, log management challenges and best practices.

The course is available at [Purple Academy](https://academy.picussecurity.com/course/log-management-proactive-soc) by Picus

## Introduction

A SOC refers to people, processes, and technologies responsible for monitoring, analyzing, maintaining, and improving an organization's cybersecurity. 

![image](https://user-images.githubusercontent.com/58165365/145220552-2a480160-94d4-4d17-bff9-9230a17a01b5.png)

- The first building block of a SOC is People. A SOC consists of different roles, including SOC analyst, incident responder, threat hunter, and SOC manager. Some mature Security Operations Centers also include compliance auditor and security architect roles.
- The second building block is Processes. Defining clear, robust, and repeatable processes brings a good foundation for the actions a SOC member takes.
- The third building block is Technology. An effective SOC incorporates data from various sources and analyzes and manages data. The core technology of a successful SOC is an enterprise-wide data collection, management, detection, and analytics solution.

## Difference between Reactive and Proactive SOC

![image](https://user-images.githubusercontent.com/58165365/145220829-34d2f6fa-6faf-4771-8f29-11178fb2ed13.png)

- The proactive SOC concept defines a transformed Security Operations Center where visibility is enhanced and maintained to contextualize threats and attack surface continuously, instead of unselective data collection to achieve visibility.

- Detection capabilities are constantly updated against the anticipated attacks to filter out noise, and detection capabilities are updated and fixed against the changing adversaries landscape instead of unselective alert triage by triaging as many alerts as possible.

 - And finally, response capabilities allow focusing on dealing with advanced threats by establishing an agile and automated incident response process and driving mitigation on network and endpoint security controls to achieve a more robust defense baseline.

## Key SOC Operations

![image](https://user-images.githubusercontent.com/58165365/145221355-7d35b4f0-0f2c-407e-b846-923116e75ff1.png)

These are the five key SOC operations.

- The first one is **Log Management**. According to the [NIST's Special Publication 800 - 92](https://csrc.nist.gov/publications/detail/sp/800-92/final), _a log is a record of the events occurring within an organization's systems and networks._ Logs are composed of log entries; each entry contains information related to a specific event within a system or network. We correlate events to find the relationship between two or more log entries. Briefly, log management is the process for generating, transmitting, storing, analyzing, and disposing of log data.

- The second one is **Alert Management.** When monitoring tool sends out alerts. It's up to the SOC to examine each one carefully, discard any false positives, and decide how aggressive any real threats are and what they may be targeting. This helps them to appropriately triage emerging threats,resolving the most critical issues first.

- The third key operation is **Prevention and Detection.** Prevention is still more effective than reaction when it comes to cybersecurity. Rather than responding to threats as they occur, a SOC monitors the network 24 hours a day, 7 days a week. As a result, the SOC team can detect malicious activity and prevent it before it causes any damage. When SOC analysts notice anything unusual, they collect as much information as possible to conduct a more detailed investigation. 

- **Incident Management and Response** is another key operation. The SOC analyst analyzes suspicious activity during the investigation stage to assess the nature of the threat. Following the investigation, the SOC team coordinates the response to resolve the issue. The SOC serves as a first responder as soon as an incident is confirmed. The aim is to respond to the extent needed while mitigating the impact on business continuity.

- Finally, **Compliance Management.** Government and industry regulations can change at any time. The SOC must be ready to keep an eye on these issues to ensure that the organization is compliant. This is particularly important given the SOC's use of data, which may be subject to rigorous collection and application standards based on location sector or intended use. The organization's continuing operation depends on compliance with these regulations.

## Why Log Management?

![image](https://user-images.githubusercontent.com/58165365/145223236-c0397e99-59e1-4e74-9e30-3907ad3eebda.png)

We start this learning path with the theme of Modern Log Management Practices for two reasons: 

- Firstly, almost every SOC, small or big, invested in a SIEM platform. But as indicated by many analysts, most of these platforms are significantly underutilized. SIEMs running with years-olddetection rules and creating alert noise is not a rarity.

- Secondly, SOC functions are consequential, and each process's success depends on the success of the preceding ones. For example, if detection is not handled well, and if there are too many alerts and too many false positives, incident response actions will not be effective either. Log Management is the most fundamental SOC function as threat detection and mitigation, monitoring and troubleshooting, incident investigation and forensics, government and industry compliance, auditing, and threat hunting are entirely dependent on internal and external context, which is provided by logs. 

Therefore, If we are to talk about the concept of proactive SOC, SIEM log management is the right place to start as every SOC function primarily depends on log data, and SIEMs took center stage at SOCs.

# Log Sources
## Primary Log Sources

In simple terms, there are four categories of sources we can choose to collect logs from:

![image](https://user-images.githubusercontent.com/58165365/145223935-d83abd98-ec9c-4d47-9592-998f8501d0cb.png)

- The first one is **Security Controls**, which are safeguards or countermeasures to prevent, detect, correct, compensate, or counteract security risks to physical property, information, computer systems, or other assets.

- The second group of log sources is **Network Infrastructure**, the hardware and software resources of an entire network that enable network connectivity, communication, operations, and management of an enterprise network.

- The third one is **Operating Systems** Microsoft Windows, macOS, Linux distributions, and other operating systems are valuable log sources.

- The last group of log sources is **Applications**.

## 1. Security Controls

![image](https://user-images.githubusercontent.com/58165365/145225312-061e9403-e1ff-4c25-b150-5151e63d1d38.png)

To detect or prevent malicious activity, protect systems and data,and support incident response and other efforts, most organizations use a variety of network-based and host-based security controls. As a result,security controls are major sources of security log data. 

- Intrusion Prevention Systems (IPS), Next-Generation Firewalls (NGFW), Network Access Control (NAC) solutions, Email Security Gateways are examples of network-based security controls. Successful and failed connection attempts, connection states, suspicious requests, detected or prevented attacks are some of the log types you can collect from network security devices. 

- Endpoint Detection and Response (EDR) and anti-malware solutions are examples of host-based endpoint security solutions. Malware scan activities, software updates, suspicious activities, and exploitation attempts are some logs of host- based security controls. 

- Other than network and host- based security controls, physical security controls are also essential log sources. For cases involving insider threats, obtaining event logs from physical security devices such as camera systems, biometric card access readers, or alarm system is highly useful. To prove a person's existence at the time of the violation or if their passwords were compromised, you could combine these events with other information gathered from servers, workstations, firewalls, VPNs, and remote access devices. The distinction between the physical security team and the IT security team is one of the most challenging aspects of accessing these logs.

## 2. Network Infrustructure

Network infrastructure refers to hardware and software resources that make network connectivity and communication possible. 

Routers, switches, wireless access points, DNS servers, and DHCP servers are only a few network infrastructure components. Network devices can be set up to monitor  very comprehensive connection activities, but they are normally set up to log only the most basic details. These logs show a lot about what's going on in the network.

Some network devices can also analyze connections and describe the attack type with IP, port, and time details, as shown in the screenshot.

![image](https://user-images.githubusercontent.com/58165365/145228775-4a88b526-ef6c-4be6-ad93-fdc584d75572.png)

## 3. Operating Systems

Operating Systems typically keep track of a variety of security-related logs.

We can organize OS logs as system events and audit records. 
- System events include operational actions performed by the operating system's components, such as service starts and stops, and system startup and shutdown events. 

- Audit records consist of successful and failed authentication attempts, changes in security policies, accounts permissions and privileges, use of privileges, and file accesses. 

Screenshot below show failed authentication events from Microsoft Windows and Ubuntu operating systems.
![image](https://user-images.githubusercontent.com/58165365/145229033-05ec6597-b4c8-4711-bd6b-f730851f7da7.png)

## 4. Applications

Not only security controls, network infrastructure, and operating systems, but also applications provide security related logs. 

Organizations use email, database, file, and web servers and clients to continue their business. Moreover, they use various commercial off-the-shelf (COTS) applications relevant to business requirements such as Supply Chain Management, Customer Relations Management (CRM), Enterprise Resource Planning software. Moreover, some organizations also use custom-developed applications.

All of these applications are a very valuable source of information to detect security issues. They provide various logs such as account and configuration changes, authentication attempts, application failures,client requests,and server responses.

You can see log entries of a database server in the screenshot below.

![image](https://user-images.githubusercontent.com/58165365/145229461-5fc35c12-ed5c-437a-aa5e-6eb16dca0224.png)

## Event Attributes

Log sources provide events and an event's attributes consist of detailed information about the event. Event date and time, event status, name of the application or service, source and destination IPs and ports, URL, source address, user ID, and event type are only a small part of the event attributes. 

SOC teams need to decide on the level of granularity of events.
- If the content is defined too wide, logs can overwhelm the resources unnecessarily and delay the investigation processes.
- If the content is too narrow, it will not be possible to achieve effective alerting, threat hunting, and incident response processes.

![image](https://user-images.githubusercontent.com/58165365/145229776-e8389950-32b4-493b-826b-62129dc19421.png)


## Deciding Log Sources & Details

Given all this complexity, deciding on log sources, event types that will be retrieved from those sources, and type of event attributes is where knowledge and technology should blend to guide SIEMpractitioners. Not every log has the same importance and relevance.

You should select log sources first; then you should decide the event types of the selected log sources. Finally, you should determine which attributes of the selected event types are collected.

![image](https://user-images.githubusercontent.com/58165365/145248728-88ee67a0-c918-4ebf-ac9a-0d2cc4b20bb5.png)

Let me elaborate further on the decision factors of log sources.

- One of the criteria SOC teams use on deciding log sources is based on their impact on the detection, how frequently logs are used to detect malicious activity. You must consider your organization's attack surface, types of threats you are concerned about, possible attack vectors. Impact on alert triage, incident response, threat hunting, and business objectives are also important.It would be best if you ask this question to yourselves: "Am I collecting the right data to detect, respond, investigate, and hunt threats effectively and achieve business objectives. Moreover, some log sources provide necessary context data for other log sources. 

- In terms of integration, ease-of-use is also essential. Whether logs can be easily integrated and parsed in SIEMs are among the factors SIEM practitioners consider.

- Clearly, you should also consider budget constraints. Most  enterprise SIEM components are priced by data velocity in terms of events per second (EPS), the number of users, the sensors deployed, and the assets monitored. 

- Compliance and audit requirements are also crucial for choosing the right data sources. For example, Requirement 10 of the Payment Card Industry (PCI), Data Security Standard (DSS) is _"track and monitor all access to network sources and cardholder data"._ GDPR, HIPAA, and FISMA are some other regulations for picking data sources. Requirements of audit frameworks, such as COBIT, ITIL, and COSO, are also important decision factors.

![image](https://user-images.githubusercontent.com/58165365/145248955-fa2697f1-ba11-4cc2-be53-d3792daba82c.png)

## Prioritising Log Sources

Let's move to log prioritization using the MITRE ATT&CKframework. Prioritization of data sources takes place in three steps:

1. Focus on the prevalent data sources. 
2. Focus on a class of data products, a technology that is prevalent in delivering the data. 
3. Focus on the most relevant attack techniques. By detecting the most relevant TTP's, we can identify threats. 

![image](https://user-images.githubusercontent.com/58165365/145249473-b9a8d27a-09fd-4ad5-9273-6aca4686ff3b.png)

### Focus on the prevalent data sources. 

The MITRE ATT&CK framework helps to identify data sources for techniques. In MITRE ATT&CK, there are about 60 listed data sources. Looking at the data sources considering a technique, MITRE ATT&CK tells us which data sources we need to observe the technique. But we don't need to consume data from all data sources linked to a technique. As you can see in the screenshot below, this is a list of all data sources for a particular technique. Using all data sources would be very resource-intensive. On the contrary, we need to prioritize sources. 

Mapping various sources to ATT&CK can help you to build a deep understanding of the adversary behavior to prioritize data sources and logs. Some data sources happened to be more efficient than others to detect adversary techniques in the MITRE ATT&CK framework. You need to consider a small set of data sources to detect the majority of known techniques.

These are the most relevant sources:
- Process and process command-line monitoring, often collected by Windows event logs and EDR platforms, can help identify almost 70% of MITRE ATT&CK techniques. 
- File and registry monitoring or other powerful and meaningful data sources. Windows event logs also collect file and registry monitoring.
- API monitoring.

![image](https://user-images.githubusercontent.com/58165365/145249962-a7dbbedf-9c9c-41f2-8e6d-24d17eaf3df2.png)

### Focus on a class of data products, a technology that is prevalent in delivering the data. 

When it comes to sources, endpoints are the most prevalent data source. You can collect data from network or cloud devices as well. But collecting data from endpoints allows us to cover more than 50% of known techniques, as you can see from the graph. 

Collecting logs from endpoints has broader coverage than the network or cloud. But, it does not mean that these data sources are not required.

![image](https://user-images.githubusercontent.com/58165365/145250019-b7e6895a-9684-4520-876a-3d0114784b65.png)

### Focus on Prevalent Advesary Techniques

You can optimize log coverage by considering the most used adversary techniques. As Picus, we analyzed thousands of malware at extracted hundreds of thousands of malware behavior. We mapped these behaviors to MITRE ATT&CK techniques and focused on the most prevalent ones. For prioritization, 19% of malware use process injection. So, if you have effective log and detection coverage of process injection, you can detect 19% of malware.

![image](https://user-images.githubusercontent.com/58165365/145250311-5a6509e6-3381-4dce-b43a-d4e770a1b375.png)

## Log Management Policies & Procedures

After identifying the requirements for log collection, you must develop standard processes to perform log management. 

- First, you must find your organization's logging goals. Then, you must define mandatory security requirements for security, regulations, and laws.
- You may also define non-mandatory requirements, which are other data sources that should be logged and analyzed if time and resources permit.
- It would help if you also defined suggested recommendations for log generations, storage, transmission, analysis, disposal, and preservation of originals logs.
- Finally, you must define roles and responsibilities for log management processes.
