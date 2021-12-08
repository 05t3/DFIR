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
