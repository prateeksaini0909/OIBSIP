# Common Network Security Threats

> **Cyber Security Research Report**  
> **Topic:** Common Network Security Threats  
> **Scope:** DoS/DDoS, Man-in-the-Middle (MITM), IP Spoofing, and DNS Poisoning/Spoofing

---

## Table of Contents

1. Introduction
2. DoS/DDoS Attacks
3. Man-in-the-Middle (MITM) Attacks
4. IP Spoofing
5. DNS Poisoning/Spoofing
6. Comparison Table
7. Key Takeaways for Network Administrators
8. Conclusion
9. References

---

# 1. Introduction

Network security is essential because organizations increasingly depend on interconnected systems, cloud platforms, web applications, remote access, and digital communication. Network attacks can affect the confidentiality, integrity, and availability (CIA) of information and services. Attackers may attempt to overwhelm systems, intercept communications, forge network identities, or manipulate name-resolution services. Among the important network threats are DoS/DDoS attacks, Man-in-the-Middle attacks, IP spoofing, and DNS poisoning/spoofing. These attacks can result in service outages, unauthorized access, information exposure, financial losses, and reputational damage. A strong defense therefore requires a layered approach involving secure protocols, access controls, network segmentation, traffic filtering, monitoring, secure DNS configuration, and incident-response planning.

---

# 2. DoS/DDoS Attacks

## 2.1 What Are DoS and DDoS Attacks?

A **Denial-of-Service (DoS)** attack attempts to make a system, application, or network service unavailable to legitimate users. The attacker may consume network bandwidth, exhaust server resources, or send excessive requests.

A **Distributed Denial-of-Service (DDoS)** attack is similar, but the malicious traffic originates from multiple systems. Attackers may use a botnet or compromised Internet-connected devices, making the traffic volume larger and more difficult to filter.

MITRE ATT&CK classifies Network Denial of Service as a technique intended to degrade or block the availability of targeted resources. Its documented sub-techniques include Direct Network Flood and Reflection Amplification.

## 2.2 How the Attack Works

A simplified DDoS attack can be understood as:

**Attacker-controlled systems → Large volume of traffic/requests → Target network/service → Resources become exhausted → Legitimate users experience disruption**

DDoS attacks can target network bandwidth, DNS services, web servers, network devices, or application resources.

## 2.3 Real-World Case Study — Mirai and the Dyn Attack

In October 2016, the **Mirai botnet** demonstrated the impact of insecure Internet-of-Things devices. Mirai compromised poorly secured IoT devices and used them to generate large-scale DDoS traffic. One major incident targeted **Dyn**, a DNS infrastructure provider, causing access problems for many major Internet services.

The incident showed that compromised consumer devices can become part of a large botnet and that attacks against critical infrastructure providers can create widespread secondary disruption.

## 2.4 Impact

A successful DoS/DDoS attack can:

- Make websites or applications unavailable.
- Interrupt business operations.
- Affect customers and employees.
- Increase infrastructure and mitigation costs.
- Cause loss of revenue and productivity.
- Create secondary disruption when dependent services become unavailable.
- Damage customer confidence and organizational reputation.

## 2.5 Mitigation Strategies

### 1. Use DDoS Protection and Upstream Filtering

Organizations can use specialized DDoS protection services, content delivery networks (CDNs), or ISP-level filtering to absorb and filter malicious traffic before it reaches critical infrastructure.

### 2. Apply Rate Limiting and Traffic Filtering

Firewalls, load balancers, and application controls can limit abnormal request rates and filter traffic patterns that do not match normal business activity.

### 3. Maintain Redundancy and an Incident-Response Plan

Critical services should have redundancy, appropriate capacity planning, monitoring, and a documented DDoS response procedure. Teams should know how to detect, escalate, contain, and recover from an attack.

---

# 3. Man-in-the-Middle (MITM) Attacks

## 3.1 What Is a MITM Attack?

A **Man-in-the-Middle (MITM)** attack, also known as **Adversary-in-the-Middle (AiTM)** in MITRE ATT&CK, occurs when an attacker positions themselves between two communicating systems.

The attacker may attempt to observe, redirect, or manipulate communication. MITRE identifies techniques such as ARP cache poisoning, DHCP spoofing, DNS/name-resolution manipulation, and rogue wireless access points as ways an adversary can establish an interception position.

## 3.2 How the Attack Works

A simplified MITM scenario is:

**User → Attacker-controlled intermediary → Legitimate service**

If communications are not adequately protected, the intermediary may be able to observe or manipulate information being transmitted.

Strong TLS/HTTPS authentication helps reduce this risk because it allows the client to verify the identity of the intended service and protects data in transit.

## 3.3 Real-World Case Study — Sea Turtle DNS Hijacking Campaign

The **Sea Turtle** campaign demonstrated how DNS manipulation could be combined with man-in-the-middle activity. Security researchers reported that attackers compromised organizations involved in domain infrastructure and redirected traffic intended for legitimate services.

The attackers could redirect traffic through attacker-controlled infrastructure, enabling interception of sensitive communications and credentials.

## 3.4 Impact

MITM attacks can result in:

- Exposure of sensitive communications.
- Theft of authentication information or session data.
- Manipulation of transmitted information.
- Redirection to malicious destinations.
- Credential theft.
- Loss of confidentiality and integrity.

## 3.5 Mitigation Strategies

### 1. Use Strong Encryption and Certificate Validation

Use properly configured HTTPS/TLS and other secure protocols. Users and systems should not ignore certificate warnings because they can indicate an interception or authentication problem.

### 2. Secure Wireless and Network Infrastructure

Use authenticated wireless networks, strong security configurations, and monitoring for unauthorized access points or unexpected network configuration changes.

### 3. Use Network Segmentation and Secure Authentication

Separate sensitive systems from less-trusted networks and use strong authentication rather than relying only on network location or IP addresses.

---

# 4. IP Spoofing

## 4.1 What Is IP Spoofing?

**IP spoofing** occurs when an attacker sends network packets with a forged source IP address. The destination system may therefore see a packet as coming from an address that does not represent the attacker's actual location.

IP spoofing can be used to conceal the origin of traffic, exploit poorly designed IP-based trust relationships, or support reflection/amplification attacks.

## 4.2 How the Attack Works

A simplified example is:

**Attacker → Packet with forged source IP → Intermediate service → Response sent toward victim**

In reflection attacks, the attacker can make third-party systems send responses toward the spoofed address. This can increase the amount of unwanted traffic reaching the victim.

## 4.3 Real-World Case Study — Reflection and Amplification DDoS

IP spoofing has been repeatedly used as an enabling technique in reflection/amplification DDoS attacks. In such attacks, packets are sent toward third-party services with the victim's IP address forged as the source. The third-party systems then send their responses toward the victim.

This technique is documented by MITRE ATT&CK under **Network Denial of Service: Reflection Amplification**. NIST's BGP security guidance also discusses the use of spoofed IP addresses in large-scale DDoS attacks.

## 4.4 Impact

IP spoofing can:

- Hide the apparent source of malicious traffic.
- Support reflection/amplification DDoS attacks.
- Complicate incident investigation.
- Bypass weak IP-based trust controls.
- Contribute to network disruption.

## 4.5 Mitigation Strategies

### 1. Apply Ingress and Egress Filtering

Network operators should filter traffic whose source addresses are not valid for the network from which the traffic originates. This reduces the ability of systems to send packets with obviously invalid source addresses.

### 2. Do Not Treat an IP Address as Authentication

An IP address should not be the only factor used to establish trust. Use strong authentication and authorization controls.

### 3. Improve Routing Security

Network operators can use measures such as **RPKI, Route Origin Authorization (ROA), route-origin validation, and prefix filtering** to improve routing security and resilience.

---

# 5. DNS Poisoning/Spoofing

## 5.1 What Is DNS?

The **Domain Name System (DNS)** translates human-readable domain names into IP addresses. For example, when a user enters a website address, DNS helps determine which server should receive the request.

Because DNS is fundamental to Internet communication, manipulation of DNS information can have a large impact.

## 5.2 What Is DNS Poisoning/Spoofing?

**DNS poisoning** or **DNS spoofing** occurs when an attacker causes a system to receive incorrect DNS information. A user may believe they are connecting to a legitimate service while being redirected to an attacker-controlled destination.

MITRE ATT&CK includes **Name Resolution Poisoning** as an Adversary-in-the-Middle sub-technique and explains that name-resolution manipulation can be used to redirect communication or collect authentication material.

## 5.3 How the Attack Works

A simplified flow is:

**User requests domain → Malicious/incorrect DNS response → User is directed to unintended IP address → Traffic reaches attacker-controlled or incorrect service**

DNS manipulation can occur at different points, including compromised DNS infrastructure, registrar accounts, or local network name-resolution mechanisms.

## 5.4 Real-World Case Study — Sea Turtle DNS Hijacking

The **Sea Turtle** campaign is a documented example of DNS hijacking. Attackers compromised organizations involved in DNS and domain infrastructure and changed DNS information so that traffic intended for legitimate organizations could be redirected through attacker-controlled servers.

The campaign affected organizations in multiple countries and demonstrated why DNS infrastructure and registrar accounts are high-value security targets.

## 5.5 Impact

DNS poisoning/spoofing can:

- Redirect users to fraudulent or malicious websites.
- Interrupt access to legitimate services.
- Support credential theft.
- Enable malicious traffic redirection.
- Undermine trust in organizational services.
- Affect multiple users or systems simultaneously.

## 5.6 Mitigation Strategies

### 1. Use DNSSEC Where Appropriate

**DNSSEC** provides mechanisms that allow DNS information to be validated for authenticity and integrity. It helps reduce the risk of accepting forged DNS records.

### 2. Secure DNS and Registrar Accounts

Restrict administrative access, use strong authentication, protect registrar accounts, keep DNS software updated, and monitor DNS configuration and domain-record changes.

### 3. Monitor DNS Activity

Monitor for unexpected DNS servers, unusual DNS responses, suspicious record changes, and abnormal query behavior. Alerts should be investigated promptly.

---

# 6. Comparison Table

| Threat | Attack Vector | Who Is at Risk? | Difficulty to Execute | Ease of Mitigation | Primary Security Goal Affected |
|---|---|---|---|---|---|
| **DoS/DDoS** | Traffic or request flooding | Websites, businesses, online services, infrastructure providers | Medium–High | Medium | Availability |
| **MITM** | Interception or manipulation of communication | Users and organizations on vulnerable networks | Medium | Medium | Confidentiality & Integrity |
| **IP Spoofing** | Forged source IP addresses | Networks, services, and DDoS targets | Medium | Medium | Integrity & Availability |
| **DNS Poisoning/Spoofing** | Manipulation of DNS information/responses | Organizations, websites, and Internet users | Medium | Medium–High | Integrity & Availability |

> **Note:** Difficulty and mitigation ratings are qualitative. They depend on the target environment, available security controls, network architecture, and attacker capabilities.

---

# 7. Key Takeaways for Network Administrators

### 1. Protect Availability

Prepare for DoS/DDoS attacks using traffic filtering, rate limiting, upstream protection, redundancy, monitoring, and an incident-response plan.

### 2. Protect Communications

Use strong encryption, secure authentication, network segmentation, and certificate validation to reduce the risk of MITM attacks.

### 3. Protect Core Network Services

Secure DNS, routing infrastructure, firewalls, and network configurations. Continuously monitor for unusual traffic, DNS changes, and unauthorized network devices.

---

# 8. Conclusion

Network security threats can affect all three major security objectives: **confidentiality, integrity, and availability**. DoS/DDoS attacks primarily threaten availability, while MITM attacks can compromise the confidentiality and integrity of communications. IP spoofing can conceal the apparent source of traffic and support reflection attacks, while DNS poisoning/spoofing can redirect users and undermine trust in Internet services.

The most effective defense is not a single security product but a **layered security strategy**. Organizations should combine secure protocols, strong authentication, firewalls, traffic filtering, network segmentation, DNS security, continuous monitoring, regular updates, and incident-response planning. By understanding how these attacks work and implementing preventive controls, network administrators can significantly reduce the likelihood and impact of network-based attacks.

---

# 9. References

1. NIST — Border Gateway Protocol Security and Resilience, SP 800-189 Rev. 1  
   https://csrc.nist.gov/pubs/sp/800/189/r1/ipd

2. NIST — Secure Domain Name System (DNS) Deployment Guide, SP 800-81  
   https://csrc.nist.gov/publications/detail/sp/800-81/rev-3/final

3. MITRE ATT&CK — Network Denial of Service (T1498)  
   https://attack.mitre.org/techniques/T1498/

4. MITRE ATT&CK — Adversary-in-the-Middle (T1557)  
   https://attack.mitre.org/techniques/T1557/

5. MITRE ATT&CK — Name Resolution Poisoning (T1557.001)  
   https://attack.mitre.org/techniques/T1557/001/

6. MITRE ATT&CK — DHCP Spoofing (T1557.003)  
   https://attack.mitre.org/techniques/T1557/003/

7. WIRED — Sea Turtle DNS Hijacking Campaign  
   https://www.wired.com/story/sea-turtle-dns-hijacking/

8. WIRED — The Mirai Botnet and the Dyn Attack  
   https://www.wired.com/story/mirai-untold-story-three-young-hackers-web-killing-monster/

---


