# Kerberos Investigation Challenge

## 1. Lab Overview

**Category:** Blue Team / SOC Investigation  
**Topic:** Kerberos Authentication and Potential Kerberoasting  
**MITRE ATT&CK Technique:** T1558.003 — Kerberoasting  
**Investigation Type:** Authentication Log Correlation  
**Status:** Completed — Investigation remains inconclusive

### Objective

Investigate an unusual burst of Kerberos service-ticket requests followed by an external HTTPS connection from the same workstation. Determine whether the activity warrants further investigation, identify the evidence required, and recommend appropriate next steps.

> **Note:** This is a scenario-based investigation exercise. The events described are not presented as telemetry collected from a live Active Directory environment.

---

## 2. Scenario

A workstation associated with a user account, John, generates an unusual burst of Kerberos service-ticket requests. Shortly afterwards, the same workstation makes an external HTTPS connection.

The activity raises concerns about possible Kerberoasting or another abnormal authentication pattern.

However, the available scenario information does not establish whether the ticket requests were malicious, whether the external connection was related, or whether the account or workstation was compromised.

### Initial Observations

- An unusual volume of Kerberos service-ticket requests was reported.
- Event ID 4769 is relevant because it records Kerberos service-ticket requests.
- An external HTTPS connection occurred afterwards.
- Further correlation is required before reaching a conclusion.

---

## 3. Investigation Questions and Answers

### Q1. What might multiple Kerberos ticket requests indicate?

**Answer:** Multiple ticket requests may indicate normal authentication activity or potentially suspicious behaviour. The number of requests alone is insufficient to determine whether an attack occurred.

The analyst should examine request frequency, targeted services, encryption details, timestamps, account behaviour and the environment's normal baseline.

### Q2. Which Windows Event ID is important when investigating Kerberos service-ticket requests?

**Answer:** Event ID **4769** records a Kerberos service-ticket request.

The analyst should examine the available event fields, including the requesting account, client address, target service/SPN, encryption information and timestamps.

### Q3. Does an external connection after multiple ticket requests confirm an attack?

**Answer:** No. The combination increases the need for investigation but does not confirm an attack.

The analyst must establish whether the external connection is suspicious and whether it can be linked to the relevant account, process or authentication activity. The two events may be unrelated.

### Q4. What evidence should be examined during endpoint investigation?

**Answer:** Relevant evidence includes:

- Parent and child processes.
- Process creation events and process trees.
- Event IDs and timestamps.
- User and service accounts.
- Source workstation and destination information.
- DNS, proxy, firewall and EDR telemetry.
- Relevant authentication and account-management events.

A process tree is particularly useful when endpoint telemetry links a suspicious process to the activity being investigated.

### Q5. Which evidence sources should be correlated?

**Selected evidence sources:**

- **Event ID 4768:** Kerberos Ticket Granting Ticket (TGT) requests.
- **Event ID 4624:** Successful Windows logon sessions.
- **DNS, proxy, firewall or EDR network telemetry:** To investigate external communications and potentially suspicious destinations.

**Additional sources required for a complete investigation:**

- **Event ID 4688 or Sysmon Event ID 1:** Process-creation telemetry.
- **Active Directory account and group-change events:** To identify relevant account creation, enablement or privilege changes.
- Other relevant Kerberos events, including Event ID 4771 where applicable.

**Lesson learned:** Correlating identity, endpoint and network evidence provides stronger investigative context than relying on Event ID 4769 alone.

### Q6. What is the MITRE ATT&CK technique ID for Pass the Ticket?

**Answer:** **T1550.003 — Pass the Ticket.**

This is distinct from **T1558.003 — Kerberoasting**, which involves requesting service tickets associated with SPN-backed accounts and attempting to crack ticket-derived material offline.

Multiple Event ID 4769 records do not, by themselves, confirm Kerberoasting.

### Q7. Should the endpoint be isolated?

**Answer:** Endpoint isolation may be appropriate if corroborating evidence indicates that the workstation is compromised.

The analyst should follow the organisation's incident-response procedures, identify the affected endpoint and obtain appropriate authorisation. A domain controller should not be isolated merely because it recorded Kerberos requests.

### Q8. What should the analyst do before disabling the account?

**Answer:** Investigate the account's normal behaviour, source workstation, service-ticket targets, privileges, recent logons and whether the activity was authorised.

Account disabling or other containment actions should be based on the evidence, risk and incident-response procedures rather than the presence of Event ID 4769 alone.

---

## 4. Final Analyst Reasoning

The unusual burst of Kerberos service-ticket requests raises suspicion. The subsequent external HTTPS connection provides additional context that warrants investigation.

However, the available information does not establish that the connection was caused by the same account activity or that either event was malicious.

The next step is to correlate the authentication events with endpoint processes, network telemetry, account privileges and the user's normal behaviour before determining whether the activity represents Kerberoasting or another security incident.

---

## 5. Final Analyst Assessment

**Assessment:** Suspicious activity — further investigation required.

**Confidence:** Preliminary. The available information is insufficient to confirm Kerberoasting or account compromise.

### Recommended Investigative Actions

1. Review Event ID 4769 details, including target SPNs, client addresses, encryption information and request frequency.
2. Compare the activity with John's normal authentication behaviour and the workstation's baseline.
3. Correlate Events 4768, 4624, 4688 or Sysmon Event ID 1, and relevant account-management events.
4. Review DNS, proxy, firewall and EDR telemetry to investigate the external HTTPS connection.
5. Determine whether the destination is suspicious and whether the connection can be linked to a particular process or user session.
6. If corroborating evidence supports compromise, escalate the incident and consider authorised containment measures under the incident-response plan.

### Analyst Conclusion

The available evidence supports further investigation of a possible Kerberoasting attempt or another abnormal authentication pattern. Neither attack execution nor account compromise has been confirmed.

The investigation should remain open until sufficient corroborating evidence supports a defensible conclusion.

---

## 6. Relevant Event IDs and ATT&CK Techniques

| Identifier | Meaning |
|---|---|
| Event ID 4768 | Kerberos TGT request |
| Event ID 4769 | Kerberos service-ticket request |
| Event ID 4771 | Kerberos pre-authentication failure |
| Event ID 4624 | Successful Windows logon |
| Event ID 4688 | Process creation |
| Sysmon Event ID 1 | Process creation |
| T1558.003 | Kerberoasting |
| T1550.003 | Pass the Ticket |

*Event availability and recorded fields depend on the Windows version, audit configuration and telemetry source.*

---

## 7. Key Lessons Learned

- A suspicious event is an investigative lead, not proof of compromise.
- Multiple Kerberos service-ticket requests can be legitimate.
- Event ID 4769 is important but must be interpreted in context.
- External connections must be linked to relevant processes or sessions before attributing them to an account.
- Correlating identity, endpoint and network telemetry strengthens an investigation.
- Kerberoasting and Pass the Ticket are different techniques with different ATT&CK identifiers.
- Incident reports should clearly separate observations, hypotheses and confirmed findings.


```

**Completion status:** Challenge reviewed and documented. Further technical investigation would be required to confirm or rule out malicious activity in a real environment.
