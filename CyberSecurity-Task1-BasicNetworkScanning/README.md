# Task 1: Basic Network Scanning with Nmap

## Overview

This project demonstrates the use of Nmap (Network Mapper) to perform
basic network scanning on a locally controlled Kali Linux virtual
machine.

The objective is to identify the status of common TCP ports, attempt
service and version detection, perform operating system detection, and
document the security observations obtained from the scans.

> Ethical Notice: This scan was performed only on a locally controlled
> Kali Linux virtual machine for educational and internship purposes.

---

## Objective

The main objectives of this task are:

- Verify the installation of Nmap.
- Identify the network address of the local Kali Linux VM.
- Perform a basic Nmap scan.
- Perform service and version detection.
- Perform operating system detection.
- Identify open, closed, or filtered ports.
- Analyze the security implications of the findings.
- Document the results and screenshots in a structured format.

---

## What is Nmap?

Nmap (Network Mapper) is an open-source network discovery and security
auditing tool.

It can be used to:

- Discover hosts on a network.
- Identify open and filtered ports.
- Detect network services.
- Determine service versions.
- Attempt operating system detection.
- Assist security professionals during authorized security assessments.

Nmap is widely used for network administration, troubleshooting,
security auditing, and penetration testing with proper authorization.

---

## Why Network Scanning Matters

Network scanning is an important part of network security because it
helps administrators understand what services are accessible on a
system.

Identifying exposed services can help organizations:

- Detect unnecessary network services.
- Review firewall configurations.
- Reduce the attack surface.
- Identify potentially outdated services.
- Improve overall network security.

Scanning should always be performed with proper authorization.

---

## Lab Environment

| Component | Details |
|---|---|
| Operating System | Kali Linux |
| Virtualization | Oracle VirtualBox |
| Network Mode | NAT |
| Target IP | 10.0.2.15 |
| Nmap Version | 7.99 |
| Scan Type | Local VM security testing |

The target IP address belongs to the local Kali Linux virtual machine
used for this educational exercise.

---

## Nmap Installation / Verification

Kali Linux used for this project already had Nmap available.

The installation was verified using:

    nmap --version

The command confirmed:

    Nmap version 7.99

This confirms that Nmap was installed and ready to use in the Kali Linux
environment.

---

## Scans Performed

### 1. Basic Network Scan

Command:

    nmap 10.0.2.15

Purpose:

The basic scan checks the default set of common TCP ports and reports
their accessibility.

Result:

- Host was detected as up.
- 1000 common TCP ports were scanned.
- All 1000 scanned ports were reported as filtered.
- No open TCP ports were identified.

Observed result:

    All 1000 scanned ports on 10.0.2.15 are in ignored states.
    Not shown: 1000 filtered tcp ports (no-response)

---

### 2. Service and Version Detection

Command:

    nmap -sV 10.0.2.15

Purpose:

The `-sV` option attempts to identify services running on accessible
ports and determine their versions.

Result:

- Host was detected as up.
- All 1000 scanned TCP ports were filtered.
- No service or service version could be identified.

This occurred because Nmap did not receive sufficient responses from
accessible open ports.

---

### 3. Operating System Detection

Command:

    sudo nmap -O 10.0.2.15

Purpose:

The `-O` option attempts to identify the target operating system by
analyzing network responses and OS fingerprints.

Result:

Nmap reported:

    Too many fingerprints match this host to give specific OS details

The exact operating system could not be determined.

The filtered ports limited the network responses available for reliable
OS fingerprinting.

---

## Port Analysis

### Open Ports

No open TCP ports were identified during the default scan.

### Filtered Ports

All 1000 scanned TCP ports were reported as filtered.

A filtered port means that Nmap did not receive a response that allowed
it to determine whether the port was open or closed.

This can occur because of firewall rules, packet filtering, or network
address translation (NAT) behavior.

Since no open ports were identified, no specific exposed service was
available for open-port risk analysis in the default scan.

---

## Security Analysis

The scan did not identify an exposed TCP service on the tested VM.

This is generally a positive observation because fewer accessible
services can reduce the network attack surface.

However, filtered ports do not necessarily mean that a service does
not exist. Firewall or NAT rules may prevent Nmap from receiving the
responses required to classify the ports.

Therefore, the results should be interpreted within the context of the
VirtualBox NAT environment used for this laboratory exercise.

---

## Limitations

The target was a Kali Linux virtual machine operating behind VirtualBox
NAT networking.

The scan results showed all default scanned TCP ports as filtered.
Because of this:

- No open TCP service was identified.
- Service/version detection could not identify a service.
- OS fingerprinting could not determine a specific operating system.

These limitations are important when interpreting automated network scan
results.

---

## Evidence

The `screenshots` directory contains screenshots documenting:

1. Nmap version verification.
2. Kali Linux IP address.
3. Basic Nmap scan.
4. Service/version detection scan.
5. OS detection scan.

The `results` directory contains the text output generated by Nmap:

- `basic_scan.txt`
- `service_scan.txt`
- `os_detection.txt`

---

## Ethical Use Guidelines

Nmap must only be used against systems and networks that you own or
have explicit permission to test.

For this project, scanning was performed only against a locally
controlled Kali Linux virtual machine.

Do not scan third-party, external, or production systems without
proper authorization.

Unauthorized network scanning may violate organizational policies,
terms of service, or applicable laws.

---

## Conclusion

This task successfully demonstrated basic network scanning using Nmap.

The target Kali Linux VM was confirmed to be reachable. However, all
1000 default TCP ports scanned by Nmap were reported as filtered.

Because no open ports were identified, Nmap could not determine any
running service or service version. OS detection was also inconclusive
because the filtered ports limited the available fingerprinting data.

The results demonstrate how network configuration, NAT, and filtering
can affect the visibility of services during a network scan.

---

## Author

**Prateek Saini**

Cybersecurity Internship - Task 1

Basic Network Scanning with Nmap
