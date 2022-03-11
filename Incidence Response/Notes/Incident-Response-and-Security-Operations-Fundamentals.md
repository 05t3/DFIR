**_Attack vectors_** are the paths used by attackers to access a vulnerability. In other words, the method used to attack an asset is called a **_Threat Vector_** or **_Attack vector_**. Attack vectors can be analyzed. The analysis is done by studying the attack surfaces like the entry points of an application, APIs, files, databases, user interfaces and so on. When you face a huge number of entries you can divide the modeling into different categories (APIs, Business workflows etc...)

![image](https://user-images.githubusercontent.com/58165365/157685522-3b5d0cad-1dc0-4c19-af60-16c479efc291.png)

## Incident Response Fundamentals

> “Incident response is an organized approach to addressing and managing the aftermath of a security breach or cyberattack, also known as an IT incident, computer incident or security incident. The goal is to handle the situation in a way that limits damage and reduces recovery time and costs.” ~ Source - [TechTarget](https://searchsecurity.techtarget.com/definition/incident-response)

_An event is any observable occurrence in a system or network._ Events include a user connecting to a file share, a server receiving a request for a web page, a user sending email, and a firewall blocking a connection attempt. Incidents are events with a negative consequence, such as system crashes, packet floods, unauthorized use of system privileges, unauthorized access to sensitive data, and execution of malware that destroys data. During incident response operation there are a lot of artifacts resources you need to collect. You can use different artifacts such as:

- IP addresses
- Domain names
- URLs
- System calls
- Processes
- Services and ports
- File hashes


## Incident Response Process

Incident response like any methodological operation goes thru a well-defined number of steps:

1. Preparation: during this phase, the teams deploy the required tools and resources to successfully handle the incidents including developing awareness training.
2. Detection and analysis: this is the most difficult phase. It is a challenging step for every incident response team. This phase includes networks and systems profiling, log retention policy, signs of an incident recognition and prioritizing security incidents.
3. Containment eradication and recovery: during this phase, the evidence pieces are collected and the containment and recovery strategies are maintained.
4. Post-incident activity: discussions are held during this phase to evaluate the team performance, to determine what actually happened, policies compliance and so on.

![image](https://user-images.githubusercontent.com/58165365/157732000-00c8db2d-b6ff-45de-b134-a29eaeced580.png)

## Establishing incident response teams

There are different incident response Teams: 
- Computer Security Incident Response Teams (CSIRT)
- Product Security Incident Response Teams (PSIRT)
- National CSIRTs and Computer Emergency Response Team (National CSIRT)

![image](https://user-images.githubusercontent.com/58165365/157734206-ac759633-6da0-4184-8c73-1663d1f65bdd.png)

## Incident response standards and guidelines:

There are many great standards and guidelines to help you become more resilient and help you to build a mature incident response program. They: 

- Computer Security Incident Handling Guide: (NIST 800-63 Second revision), you can find it here: Computer Security Incident Handling Guide - NIST Page
- ISO 27035: ISO/IEC 27035 Security incident management
- SANS Incident Handler Handbook: Incident Handler's Handbook - SANS.org
- CREST Cyber Security Incident Response Guide: Cyber Security Incident Response Guide - crest


## Security Operation Centers Fundamentals

Wikipedia defines Security Operation Centers as follows: A security operations center is a centralized unit that deals with security issues on an organizational and technical level. A SOC within a building or facility is a central location from where staff supervises the site, using data processing technology.

![image](https://user-images.githubusercontent.com/58165365/157738078-cb1f5a1e-ad5d-4080-bab3-0f8d70e2140b.png)

Security Operation Centers are not only a collection of technical tools. SOCs are people, process and technology.

To help you prepare your mission I highly recommend you to read this guide from [Sampson Chandler : Incident Response Guide](https://www.peerlyst.com/posts/incident-response-guide-sampson-chandler?trk=post_page_recommended_reads)

It is essential to evaluate your SOC maturity because you can’t improve what you cannot measure. There are many maturity models in the wild based on different metrics based on your business needs and use cases. Some of the metrics are:
- Time to Detect (TTD)
- Time to Respond (TDR)

![image](https://user-images.githubusercontent.com/58165365/157738770-e4509f20-6520-49ac-a4c2-2ca27348c812.png)

Your maturity model will be identified using this graph from [LogRythm](https://logrhythm.com/blog/a-ctos-take-on-the-security-operations-maturity-model/): 

![image](https://user-images.githubusercontent.com/58165365/157738862-8aef42f8-5306-430a-a14e-f7985c596c01.png)

# Resources

- [UC Berkeley - Incident Response Planning Guideline](https://security.berkeley.edu/incident-response-planning-guideline)
