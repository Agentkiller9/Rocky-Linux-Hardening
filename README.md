# 💻 Rocky Linux OS Hardening & Penetration Testing

## 🛡️ Project Overview
This project focused on the complete OS hardening of a **Rocky Linux 9** system, following industry best practices to significantly reduce the attack surface. The effectiveness of these controls was rigorously validated through a **dual-VM comparative analysis** and simulated penetration tests from a Kali Linux machine.

### Key Objectives
* **Attack Surface Reduction:** Disable and remove all unnecessary and insecure services (e.g., Telnet, FTP, Samba, MySQL).
* **Strong Policy Enforcement:** Implement comprehensive password policies (min length 12, complexity, and aging) via `/etc/login.defs` and PAM modules.
* **Perimeter Defense:** Configure and enforce strict packet filtering using the **Firewalld** service.
* **Penetration Testing:** Use **Metasploit Framework** and **Nmap Scripting Engine (NSE)** to actively test and confirm the exploitation resistance of the system.
* **Continuous Auditing:** Deploy and automate security auditing tools (**Lynis** and **Rkhunter**) using `cron` for daily checks.

---

## ⚙️ Methodology & Implementation

### Comparative Architecture
The project utilized a comparative testing model:

* **Rocky-Vuln:** The baseline system with default, unhardened configurations.
* **Rocky-Secure:** The system with all security measures applied.
* **Kali Linux:** Attacker machine used for reconnaissance and exploitation.

### Key Hardening Measures Implemented
1.  **Service Disablement:** Insecure services like Telnet and FTP were permanently disabled. **OpenSSH** was configured as the only remote shell access, with **root login prohibited**.
2.  **Firewall Control:** `Firewalld` was configured to drop or filter over 150 ports that were exposed by default, significantly reducing the system's attack surface.
3.  **Audit & Integrity:** **Lynis** was used to achieve a high Hardening Index score, and **Rkhunter** was implemented to perform rootkit and file integrity monitoring. Both tools were automated for daily, routine scans.

---

## 🔎 Testing & Validation Results

### Nmap Scan Results

| Target | Initial Scan Result | Post-Hardening Scan Result |
| :--- | :--- | :--- |
| **Rocky-Vuln** | Multiple open ports (21/FTP, 23/Telnet, 80/HTTP, 139/SMB, 3306/MySQL, etc.) | N/A |
| **Rocky-Secure** | N/A | Only **SSH (22/tcp)** and **HTTP (80/tcp)** ports open; all others filtered or blocked. |

### Penetration Testing with Metasploit
* **Vulnerability Confirmation:** Exploitation modules (e.g., FTP login brute-force) succeeded against the **Rocky-Vuln** machine, often yielding a shell in seconds.
* **Mitigation Validation:** The exact same brute-force and exploitation attempts failed entirely against the **Rocky-Secure** machine, validating the strength of the new security configurations.

**Key Takeaway:** The successful resistance of the hardened system to Metasploit exploits demonstrated the critical role of proactive OS hardening in mitigating complex threats, providing empirical proof of resilience.
