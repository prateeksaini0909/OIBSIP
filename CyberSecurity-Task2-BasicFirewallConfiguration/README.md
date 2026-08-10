# Basic Firewall Configuration Using UFW

## Author

**Prateek Saini**

**Track:** Cyber Security
**Task:** Task 2 – Basic Firewall Configuration
**Tool:** UFW (Uncomplicated Firewall)
**Operating System:** Kali Linux

---

## Objective

The objective of this task is to configure a basic firewall using UFW (Uncomplicated Firewall) on Kali Linux. The firewall is used to control incoming and outgoing network traffic by allowing required services and denying unwanted traffic.

---

## Tools Used

* Kali Linux
* UFW (Uncomplicated Firewall)
* Linux Terminal
* VirtualBox

---

## What is a Firewall?

A firewall is a security mechanism that monitors and controls network traffic based on predefined rules. It can allow trusted connections and block unwanted or unauthorised connections.

A firewall helps reduce the attack surface of a system by limiting access to network services that are not required.

---

## UFW Installation

UFW stands for **Uncomplicated Firewall**. It provides a simple command-line interface for managing firewall rules on Linux.

UFW was installed using:

```bash
sudo apt install ufw
```

The installation was verified before configuring the firewall.

---

# Firewall Configuration

## 1. Allow SSH Traffic

SSH traffic on port 22 was allowed. SSH is commonly used for secure remote administration of Linux systems.

```bash
sudo ufw allow ssh
```

### Security Reason

SSH access may be required for remote administration. Only trusted users should be allowed to access SSH, and strong authentication should be used.

---

## 2. Deny HTTP Traffic

Incoming HTTP traffic on port 80 was denied.

```bash
sudo ufw deny http
```

### Security Reason

HTTP is unencrypted and may expose web traffic to interception. Since HTTP was not required for this task, incoming traffic on port 80 was blocked.

---

## 3. Allow HTTPS Traffic

HTTPS traffic on port 443 was allowed.

```bash
sudo ufw allow https
```

### Security Reason

HTTPS provides encrypted communication between clients and web servers. It was allowed as an example of a commonly required secure web service.

---

## 4. Allow DNS Traffic

DNS traffic on port 53 was allowed.

```bash
sudo ufw allow 53
```

### Security Reason

DNS is used to resolve domain names into IP addresses. The rule was added as an additional firewall rule for normal network name-resolution traffic.

---

## 5. Configure Default Incoming Policy

Incoming connections were denied by default.

```bash
sudo ufw default deny incoming
```

### Security Reason

A default-deny incoming policy blocks unsolicited incoming connections unless they are specifically allowed by a firewall rule.

---

## 6. Configure Default Outgoing Policy

Outgoing connections were allowed by default.

```bash
sudo ufw default allow outgoing
```

### Security Reason

Allowing outgoing connections permits normal applications and system services to communicate with external resources while incoming access remains restricted.

---

## 7. Enable UFW

The firewall was enabled using:

```bash
sudo ufw enable
```

The firewall status was then verified.

---

# Firewall Rules Summary

| Port / Service | Protocol | Action | Purpose                        |
| -------------- | -------- | ------ | ------------------------------ |
| 22 / SSH       | TCP      | ALLOW  | Secure remote administration   |
| 80 / HTTP      | TCP      | DENY   | Block unencrypted HTTP traffic |
| 443 / HTTPS    | TCP      | ALLOW  | Allow secure web traffic       |
| 53 / DNS       | TCP/UDP  | ALLOW  | Allow DNS traffic              |

The default firewall policy is:

* **Incoming:** Deny
* **Outgoing:** Allow

---

# Verification

The active firewall configuration was verified using:

```bash
sudo ufw status verbose
```

The final configuration showed:

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)

22/tcp    ALLOW IN    Anywhere
80/tcp    DENY IN     Anywhere
443       ALLOW IN    Anywhere
53        ALLOW IN    Anywhere
```

IPv6 equivalents of the configured rules were also automatically created by UFW.

---

# Testing Denied HTTP Traffic

A check was performed to determine whether a service was listening on port 80:

```bash
sudo ss -lntp | grep ':80'
```

No service was listening on port 80 during the test.

The UFW configuration was then verified using:

```bash
sudo ufw status verbose
```

The output confirmed that incoming traffic to port 80 has an explicit deny rule:

```text
80/tcp    DENY IN    Anywhere
```

Because no web service was running on port 80 during the test, a direct HTTP connection test could not independently demonstrate packet blocking. Therefore, the firewall rule was verified through the active UFW configuration.

---

# Security Analysis

The firewall configuration reduces the system's exposure to unwanted incoming connections.

The **SSH allow rule** permits remote administration when required. SSH should be protected using strong authentication and should not be unnecessarily exposed.

The **HTTP deny rule** prevents incoming connections to port 80, reducing exposure to an unencrypted web service.

The **HTTPS allow rule** permits secure web traffic when required.

The **DNS allow rule** permits DNS-related network traffic for domain-name resolution.

The **default-deny incoming policy** provides an additional layer of security because new incoming connections are blocked unless explicitly permitted.

---

# Firewall Configuration Script

The firewall rules were also stored in a runnable script named:

```text
ufw_configuration.sh
```

The script applies the configured rules in sequence and verifies the firewall status.

The script contains:

```bash
#!/bin/bash

sudo ufw allow ssh
sudo ufw deny http
sudo ufw allow https
sudo ufw allow 53
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
sudo ufw status verbose
```

The script was made executable using:

```bash
chmod +x ufw_configuration.sh
```

---

# Project Files

* `README.md` – Complete project documentation
* `firewall_rules.txt` – Final UFW configuration output
* `ufw_configuration.sh` – Runnable firewall configuration script
* `screenshots/01_ufw_status.png` – Screenshot showing the active firewall configuration

---

# Project Structure

```text
CyberSecurity-Task2-BasicFirewallConfiguration/
├── README.md
├── firewall_rules.txt
├── ufw_configuration.sh
└── screenshots/
    └── 01_ufw_status.png
```

---

# Conclusion

The basic firewall configuration was successfully completed using UFW on Kali Linux.

The firewall was configured with a default-deny incoming policy and default-allow outgoing policy. SSH traffic on port 22 was allowed, HTTP traffic on port 80 was denied, and additional rules were added for HTTPS and DNS.

The final firewall configuration was verified using `sudo ufw status verbose` and documented through the configuration output, runnable script, README, and screenshot.

This task demonstrates how a host-based firewall can be used to control network traffic and reduce the exposure of a Linux system to unwanted incoming connections.
