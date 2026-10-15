
# Lab 06 — Active Directory Fundamentals

## Objectives
- Explain the role of Active Directory and a Domain Controller.
- Distinguish users, computer accounts, security groups, OUs and GPOs.
- Explain how DNS and Kerberos support domain environments.
- Identify security-relevant directory changes.
- Practise separating observed facts from assumptions.

## Key Concepts
- **Active Directory (AD):** Microsoft's directory service for managing domain identities, computers, groups and related resources.
- **Domain Controller (DC):** A server running Active Directory Domain Services that provides directory and authentication services.
- **User account:** An identity used by a person or service.
- **Computer account:** An identity representing a domain-joined computer.
- **Security group:** A group used to assign permissions to members.
- **Organizational Unit (OU):** A directory container used for organisation, delegation and Group Policy linking.
- **Group Policy Object (GPO):** A collection of supported settings applied to users or computers.
- **DNS:** Helps domain clients locate domain controllers and services.
- **Kerberos:** A ticket-based authentication protocol commonly used in Active Directory.

## Enterprise Scenario
A SIEM reports that account `ACME\svc-deploy` added
`ACME\temp-admin` to the `Domain Admins` group at 02:14.

This is simulated training evidence.

## Investigation Questions
1. Was the group change authorised?
2. Is the actor expected to modify privileged group membership?
3. Was the new account recently created or enabled?
4. Were there unusual logons before the change?
5. Did the account authenticate to other systems afterward?
6. What additional logs would help confirm or refute compromise?

## Relevant Windows Event IDs
- **4624:** Successful logon.
- **4625:** Failed logon.
- **4720:** User account created.
- **4722:** User account enabled.
- **4728:** Member added to a security-enabled global group.
- **4732:** Member added to a security-enabled local group.
- **4740:** Account locked out.
- **4768:** Kerberos TGT request.
- **4769:** Kerberos service-ticket request.

Event availability depends on audit configuration and environment.
An event alone does not prove malicious activity.

## Hands-on Activity
On my own Windows computer, use Command Prompt:

```bat
whoami - desktop-hgbjjka\chidi
whoami /all - desktop-hgbjjka\chidi S-.-.-.-32.........................
echo %USERDOMAIN% - DESKTOP-HGBJJKA
echo %LOGONSERVER% - \\DESKTOP-HGBJJKA
systeminfo | findstr /B /C:"Domain" - Domain:                    WORKGROUP
```

The result above is because it is a local account and not a DC

My personal computer is not domain-joined and I dont expect to have the result of a DC

## Findings
- Environment:
- Account type:
- Domain/workgroup result:
- Interesting group or privilege observations:
- Evidence collected:
- Limitations:

## Analyst Assessment
Separate:
- **Facts:** What the commands or logs directly show.
- **Inferences:** What those observations may mean.
- **Unknowns:** What requires additional evidence.

## Common Pitfalls
- Treating every privileged group change as malicious.
- Assuming successful authentication means the user is authorised to access every resource.
- Confusing an OU with a security group.
- Assuming a personal workstation is domain-joined.
- Attributing account activity to a person without corroborating evidence.
- Publishing sensitive account or domain details in a public repository.

## Lessons Learned
- Active Directory centralises identities and access-related administration.
- Privileged group changes deserve contextual investigation.
- DNS, authentication logs, endpoint telemetry and change records can complement one another.
- A defensible conclusion must reflect the available evidence.

## Questions for Further Study
- How does a computer locate a Domain Controller?
- How are user and computer accounts different?
- How do OUs differ from security groups?
- How can a SOC detect unexpected privileged group changes?
