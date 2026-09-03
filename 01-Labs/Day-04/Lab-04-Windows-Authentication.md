# Day 04 — Windows Authentication & LSASS

## Objectives

## 1. What is LSASS?

## 2. What is NTLM?

## 3. What is Kerberos?

## 4. NTLM vs Kerberos

## 5. Password vs Hash vs Kerberos Ticket

## 6. Windows Event Logs

### Event ID 4624

### Logon Types

## 7. Sysmon

## 8. MITRE ATT&CK

## 9. Lab Observations

### LSASS

Process:
PID:
Path:
Company:
Version:

### Event 4624

Logon Type:
Account:
Authentication Package:
Source Network Address:

## 10. Analyst Challenge

### What concerned me?

### IOCs

### IOAs

### ATT&CK Techniques

### Evidence to collect

### Containment recommendations

## 11. Lessons Learned

## 12. Questions I Still Have







What is LSASS? *LSASS is an abbreviation for Local security authority subsystem service and it is a service that stores credentials on a windows machine

Why is LSASS valuable to attackers? +LSASS is valuable to attackers because when they get control of a workstation, they want to engage in lateral movement and it can be done by having access to credentials and these credentials are stored in LSASS memory

What is the difference between Password, Hash and Kerberos ticket? *A password is a secret key the user of a machine knows while a hash is a cryptographic representation of data and A kerberos ticket are tickets used for authentication within a domain enviroment

What is the difference between NTLM and Kerberos? NTLM has credential materials while kerberos stores tickets

What does T1003.001 represent? It represents LSASS memory attack

What does Windows Event ID 4624 represent? It represents successful logon

What does Sysmon Event ID 1 represent? It represents process creation

If an EDR detects suspicious access to LSASS, what would be your first three investigation steps?

who launched the process?
What command line was used?
what account was involved ?




## Analyst Challenge — Investigation Timeline

| Time | Event | Assessment |
|------|------|------------|
| 02:13 | PowerShell executed | Suspicious in context |
| 02:14 | update.exe created | Suspicious |
| 02:14 | update.exe accessed LSASS | Potential credential access |
| 02:15 | DNS query | Potential C2 indicator |
| 02:15 | Connection to 185.221.10.4:443 | Potential C2 |
| 02:17 | John authenticated to FILE-SERVER | Possible lateral movement |
| 02:21 | John authenticated to DC01 | Requires investigation |

## Hypothesis

FINANCE-PC-04 may have been compromised, with evidence indicating
potential credential-access activity involving LSASS, suspicious
PowerShell execution, and possible external C2 communication.

Authentication activity involving the John account requires further
investigation to determine whether credential compromise and lateral
movement occurred.

## IOCs

- 185.221.10.4
- update-secure-login.com
- update.exe

## IOAs

- Suspicious PowerShell execution
- Suspicious LSASS access
- Unexpected external communication
- Potential abnormal authentication activity

## Potential MITRE ATT&CK Techniques

- T1059.001 — PowerShell
- T1003.001 — LSASS Memory
