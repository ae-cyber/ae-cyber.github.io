---
title: "AugustEdtion"
description: 
date: 2023-08-15T21:00:23Z
image: 
math: 
license: 
hidden: false
comments: true
draft: false
categories:
    - Microsoft-PatchTuesday
tags:
    - MS-PatchTueday
toc: true
---

!(Padlock)[content/post/MicrosoftPatchTuesday/SecurityPadlock.png]

Each month Microsoft releases its "Patch Tuesday", the August edition brings 87 vulnerabilities, where 76 have been included as patches, of these 6 are critical, 68 are important and 2 are moderate:

|                         | Moderate | Important | Critical |
| ----------------------- |:--------:|:---------:|:--------:|
| Elevation of privileges |          |    18     |          |
| Denial of service       |          |     8     |          |
| Defence in depth        |    1     |           |          |
| Information Disclosure  |          |    10     |          |
| Spoofing                |          |    12     |          |
| Remote Code Execution   |          |    17     |    6     |
| Security Feature Bypass |          |     3     |          |


An additional 12 Microsoft Edge (Chromium) vulnerabilities were also released, 1 of which was designated as a "Security Feature Bypass" (moderate), the other 11 were not given a designation or severity. These vulnerabilities have been fixed earlier in the month.

Another vulnerability listed as a "Microsoft Office Defence in Depth Update" was also included in the security updates however details of this have not been publicly disclosed so it is not included in the breakdown above. - **ADV230004**

The moderate Defence in Depth listed above is a response to CVE-2023-36884 which is a previously disclosed unpatched vulnerability, this will be explained in the section below. - **ADV230003**

---
## Zero-Day Vulnerabilities

#### ADV230003 (CVE-2023-36884) - Windows Search Remote Code Execution Vulnerability

##### Summary:
CVE-2023-36884 is a critical remote code execution vulnerability which was found in Microsoft Office and Windows HTML. An attacker can execute code which bypasses many system protections using Microsoft Office documents which when opened by a user will trigger a download of a malicious file. This file will contain a script which injects an iframe into the system, subsequently leading to the download of the attackers payload. Due to the requirement for human interaction the attack is often initiated via phishing or other social engineering techniques which can deploy the payload on a users system.

**Attack Vector:**
The vulnerable component of this attack is linked to the network stack, this widens the scope of potential attackers to any threat actor on the internet. This "remotely exploitable attack" can be taken exploited at the network protocol layer from locations which span across multiple routers.

**Complexity:**
The complexity of the attack hinges on factors which are beyond the direct control of the attacker. Achieving a successful attack cannot be accomplished without necessary steps prior to the exploitation, meaning an attacker would need to allocate a vast amount of effort to prepare the execution against the vulnerable component, including; information gathering regarding the target environment, preparation of the target to improve the reliability of the attack and/or inserting themselves into the logical network pathway which connects the target and the resources which are requested by the victim in order to read/modify network communications (via a man-in-the-middle attack).

**Privileges Required**
In order to exploit the vulnerability the attacker does not require any privileges as it is an unauthorised attack which does not require access to settings or files to carry out an attack. However the attack does require user interaction where some action must be performed before the vulnerability can be exploited.

**Scope**
The scope of the attack states that the exploited vulnerability can only affect resources managed by the same security authority. In this scenario, the component that is susceptible to the vulnerability and the component that is affected by it are either identical, or they both fall under the jurisdiction of the same security authority.

**Impact:**
The attacker can achieve total loss of confidentiality, exposing all resources within the affected component, they might gain access to restricted information of which the disclosed data still has a direct and serious impact. The attacker could be capable of modifying all files protected by the impacted component or depending on the system configuration only specific files could be altered, but such tampering would directly and significantly impact the component. The attacker could succeed in completely denying access to resources within the impacted component and this loss of availability might be either sustained, persisting as long as the attacker's attack continues, or it could be persistent, continuing even after the attack concludes. Alternatively, the attacker may possess the ability to partially deny availability, for instance, while the attacker might not disrupt existing connections, they could hinder new ones, or they could repeatedly exploit a vulnerability, causing incremental memory leaks that ultimately result in the complete unavailability of a service.

#### CVE-2023-38180 - .NET and Visual Studio Denial of Service

##### Summary:
CVE-2023-38180 takes advantage of an uncontrolled resource consumptions vulnerability in .NETs Kestrel component. As it is a low complexity attack that does not require any special privileges it is a dangerous DoS attack which is able to be exploited persistently.

**Attack Vector:**
The vulnerable component for this is also linked to the network stack and allowing the scope of potential attacker to anyone placed on the internet. As it is remotely exploitable at the protocol layer, any attacker would be able to perform the attack from multiple network hops away.

**Complexity:**
The complexity does not require specialised network conditions or extenuating circumstances, any attacker would be able to successfully exploit this attack against the vulnerable component.

**Privileges Required**
In order to exploit this vulnerability the attacker does not need any prior access to any settings or files within the network. This attack also does not need any interaction from the user.

**Scope**
The scope of the attack means that it can only affect resources which are the same or managed by the same security authority.

**Impact:**
There is no loss of confidentiality or integrity however there is a total loss of availability, an attacker is able to fully deny access to the impacted components resources. An attacker can consistently deny any availability of existing or new connections, individually the attack will only leak a minor amount of memory but wiht persistent attacks the entire service can become unavailable.

---

## Critical Vulnerabilities

##### CVE-2023-29328 & CVE-2023-29330 (Microsoft Teams RCE Vulnerability)

> CVSS Rating: 8.8

These vulnerabilities are critical remote code executions that affect Microsoft Teams. An attack can trick users into joining a meeting which opens the opportunity to execute code on the target system, it does not require any previous privileges in order to exploit.


##### CVE-2023-35385, CVE-2023-36910 & CVE-2023-36911 (Microsoft Message Queuing Remote Code Execution Vulnerability)

> CVSS Rating: 9.8

These are vulnerabilities which affect the Microsoft Message Queuing (MSMQ) service. The attacker can transmit a MSMQ packet which is specifically crafted to the MSMQ server, this will then allow remote code execution on the targetted server. This vulnerability can be discovered by enumerating the service running on TCP/1801.


##### CVE-2023-36895 (Microsoft Outlook Remote Code Execution Vulnerability)

> CVSS Rating: 7.8

The final critical vulnerability is within Microsoft Outlook, it allows for arbritary code execution however Microsoft has stated that it is less likely to be exploited. It does not require any previous privileges and has a low complexity rating.

---

### Mitigation

In order to mitigate the vulnerabilities which have been disclosed in the latest edition of "Microsoft's Patch Tuesday" it is recommended to perform the latest updates which are released by Microsoft. Every user in an organisation should implement these as soon as possible or else risk an attacker exploiting them prior to patching taking place.

For system administrators it is imperative that a patching strategy is put in place and consistently reviewed to ensure that the security posture of an organisation is improved and maintained.

---
### References

Microsoft MSRC Update Guide - https://msrc.microsoft.com/update-guide/
Lifewire Patch Tuesday - https://www.lifewire.com/patch-tuesday-2625783
Rapid7 Patch Tuesday Review - https://www.rapid7.com/blog/post/2023/08/08/patch-tuesday-august-2023/
