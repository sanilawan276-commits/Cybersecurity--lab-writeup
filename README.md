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

Week 5

sudo nmap -sV -p 80,3306 127.0.0.1: Port 80 open, running Apache httpd 2.4.68 (Debian). Port 3306 open, identified as MariaDB (nmap marks it with "?" because its identification is uncertain).



## Week 10: Hydra on a Local Test Account

I tested password guessing against an SSH service on my own machine (127.0.0.1), using a test account I created for this exercise. The account was deleted and the SSH service was stopped afterwards.

**What I did**
- Created a test account on my Kali machine and set its password.
- Started the SSH service and confirmed it was listening on port 22.
- Built a small wordlist of common passwords and wrong guesses.
- Ran Hydra with `hydra -l testuser -P ~/wordlist.txt -t 4 -V ssh://127.0.0.1`.

**Result**
- Hydra tested the wordlist and reported "0 valid password found." The test password was not in the list, so Hydra could not match it.

**Mistakes I made and fixed**
- My first run used `-p` (one password) instead of `-P` (a wordlist file), so it did not test the list.
- The wordlist had a typo (`adminin` instead of `admin`), so one common password was never tested.

**What I learned**
- Hydra only finds passwords that appear in its list. A "not found" result is only as reliable as the test that produced it, so check your flags and input files first.
- Weak, common passwords are the first guesses attackers try, so they must never be used on real accounts.
- Defences such as strong unique passwords, account lockout after repeated failures, and two-factor authentication stop guessing attacks.

### Screenshot
- Hydra output showing six wrong guesses and the final "0 valid password found" line.
