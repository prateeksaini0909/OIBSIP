# Cyber Security Internship – Task 2

## Basic Firewall Configuration Using UFW

### Author

Prateek Saini

**Track:** Cyber Security
**Task:** Task 2 – Basic Firewall Configuration
**Tool:** UFW (Uncomplicated Firewall)
**Operating System:** Kali Linux

---

## Objective

The objective of this task is to configure a basic firewall using UFW on Kali Linux and control incoming and outgoing network traffic using firewall rules.

---

## Tools Used

* Kali Linux
* UFW (Uncomplicated Firewall)
* Linux Terminal

---

## Firewall Configuration

### 1. Allow SSH

SSH traffic was allowed on port 22.

```bash
sudo ufw allow ssh
```

### 2. Deny Incoming Traffic

Incoming connections were denied by default.

```bash
sudo ufw default deny incoming
```

### 3. Allow Outgoing Traffic

Outgoing connections were allowed.

```bash
sudo ufw default allow outgoing
```

### 4. Enable Firewall

The UFW firewall was enabled.

```bash
sudo ufw enable
```

---

## Verification

The final firewall configuration was verified using:

```bash
sudo ufw status verbose
```

### Final Result

* Firewall Status: Active
* Incoming Traffic: Denied by default
* Outgoing Traffic: Allowed by default
* SSH Port 22: Allowed
* Logging: Enabled at low level

---

## Security Analysis

The default-deny incoming policy helps reduce unauthorized incoming network connections. Only services that are specifically allowed by firewall rules can accept incoming traffic.

SSH on port 22 was allowed for remote administration when required. In a real-world environment, SSH should be properly secured with strong authentication and appropriate security controls.

---

## Project Files

* `README.md` – Project documentation
* `firewall_rules.txt` – Final UFW configuration output
* `screenshots/01_ufw_status.png` – Screenshot showing the active firewall configuration

---

## Project Structure

```text
CyberSecurity-Task2-BasicFirewallConfiguration/
├── README.md
├── firewall_rules.txt
└── screenshots/
    └── 01_ufw_status.png
```

---

## Conclusion

The basic firewall configuration was successfully completed using UFW on Kali Linux.

The firewall was configured with a default-deny incoming policy, default-allow outgoing policy, and an SSH allow rule. The final configuration was verified and documented with the required output file and screenshot.


