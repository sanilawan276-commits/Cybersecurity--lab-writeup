# Cybersecurity--lab-writeup

This project documents my hands-on cybersecurity practice using Kali Linux and Nmap in an authorized lab environment. The goal was to identify open ports, discover network services, and investigate potential security weaknesses.

Tools Used

- Kali Linux
- Nmap 7.99
- Linux command line

Commands Used

1. Network Scanning

nmap 10.0.2.2

2. Vulnerability Assessment

nmap --script vuln 10.0.2.2

Scan Findings

Port| Service| Observation
22/tcp| SSH| Open
135/tcp| MSRPC| Open
445/tcp| Microsoft-DS/SMB| Open

Some SMB vulnerability checks returned connection-negotiation errors. These errors do not confirm that the target is vulnerable.

Screenshot Evidence

The screenshot below shows the Nmap vulnerability assessment performed in my lab.

"Nmap Vulnerability Scan" (nmap-vulnerability-scan.jpg)

Exploitation and Validation

I performed additional testing in the lab. The exact vulnerability and evidence of successful exploitation will be documented after the finding has been confirmed.

Lessons Learned

- Open ports are not automatically vulnerabilities.
- Vulnerability scan results must be investigated and validated.
- Findings should be supported by evidence.
- Security testing must be authorized.

Disclaimer

This project is for cybersecurity education and authorized lab testing.


## Week 7: SQL Injection (DVWA)

I compared DVWA's SQL Injection module at Low, Medium, and High, using the same normal input (`1`) each time.

- **Low:** free text box. Input `1` returned the admin record.
- **Medium:** the free text box was replaced with a dropdown. Input `1` returned the admin record.
- **High:** input is entered in a separate popup window, then the result is shown on the main page. Input `1` returned the admin record.

**What I learned:** the security level changes how input is submitted, but the same query behaviour can remain. A dropdown or popup is not a real defence on its own. The real fix is parameterized queries on the server, so user input is treated as data, not as SQL code.
