__What is LSASS?__
*LSASS is an abbreviation for Local security authority subsystem service and it is a service that stores credentials on a windows machine

__Why is LSASS valuable to attackers?__
+LSASS is valuable to attackers because when they get control of a workstation, they want to engage in lateral movement and it can be done by having access to credentials and these credentials are stored in LSASS memory

__What is the difference between Password, Hash and Kerberos ticket?__
*A password is a secret key the user of a machine knows while a hash is a cryptographic representation of data and A kerberos ticket are tickets used for authentication within a domain enviroment

__What is the difference between NTLM and Kerberos? NTLM has credential materials while kerberos stores tickets__


__What does T1003.001 represent?__
It represents LSASS memory attack

__What does Windows Event ID 4624 represent?__
It represents successful logon

__What does Sysmon Event ID 1 represent?__
It represents process creation

__If an EDR detects suspicious access to LSASS, what would be your first three investigation steps?__
1. who launched the process?
2. What command line was used?
3. what account was involved ?
