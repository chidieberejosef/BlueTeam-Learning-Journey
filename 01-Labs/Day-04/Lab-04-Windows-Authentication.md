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
