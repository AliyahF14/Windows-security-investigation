# Windows Authentication & Security Event Investigation

## Project Highlights

- Investigated Windows Security Event Logs using Event Viewer
- Analyzed Windows Event IDs 4624, 4625, 4648, 4672, 4688, 4720, and 4732
- Performed a controlled failed-authentication test
- Investigated Logon Type, process, failure reason, and source address
- Distinguished benign Windows activity from potentially suspicious behavior
- Documented findings using a SOC-style investigation workflow
- Created sanitized evidence screenshots and a professional incident report

## Project Overview

This project demonstrates a hands-on investigation of Windows Security Event Logs using **Windows Event Viewer**.

The investigation focused on authentication activity, account activity, privilege assignments, and a controlled failed-login event. The objective was to practice identifying relevant Windows Event IDs, analyzing event details, distinguishing legitimate activity from potential security concerns, and documenting findings using a SOC-style investigation process.

The investigation was performed on a personal Windows system using built-in Windows security tools.

---

## Objectives

* Analyze Windows Security Event Logs
* Investigate successful and failed authentication events
* Identify relevant Windows Security Event IDs
* Examine logon types, processes, and source addresses
* Investigate account and privilege-related events
* Distinguish normal Windows activity from potentially suspicious activity
* Document evidence and findings in a structured incident investigation
* Practice security analyst skills applicable to entry-level SOC and cybersecurity roles

---

## Tools Used

* **Windows Event Viewer**
* **Windows Security Event Logs**
* Windows built-in security auditing
* Manual log analysis
* GitHub for documentation and portfolio presentation

---

## Investigation Scope

The investigation examined the following Windows Security Event IDs:

| Event ID | Description                                  | Investigation Result                                 |
| -------- | -------------------------------------------- | ---------------------------------------------------- |
| **4624** | Successful account logon                     | Normal interactive logon identified                  |
| **4625** | Failed account logon                         | Controlled failed-login event investigated           |
| **4648** | Logon attempted using explicit credentials   | Activity associated with `svchost.exe` and localhost |
| **4672** | Special privileges assigned to a new logon   | `SYSTEM` activity observed                           |
| **4688** | New process created                          | No events available in the current log               |
| **4720** | User account created                         | No events identified                                 |
| **4732** | Member added to security-enabled local group | No events identified                                 |

---

## Investigation Methodology

The investigation followed a basic security operations workflow:

1. Identify relevant security events
2. Filter Windows Security Logs by Event ID
3. Examine individual event details
4. Record relevant evidence
5. Evaluate whether activity appeared normal or suspicious
6. Correlate findings with the known system activity
7. Document the final assessment

---

## Key Findings

### Event ID 4624 — Successful Interactive Logon

A successful Windows logon event was identified.

**Observed characteristics:**

* Event ID: `4624`
* Logon Type: `2`
* Account: Normal Windows user account

**Assessment:**

Logon Type 2 represents an interactive logon, such as a user signing into Windows directly at the computer. The event was consistent with normal user activity.

**Result:** Likely benign.

---

### Event ID 4648 — Explicit Credential Use

An Event ID 4648 was identified and investigated.

**Observed characteristics:**

* Event ID: `4648`
* Account: Normal Windows account
* Target: `localhost`
* Process: `svchost.exe`

**Assessment:**

The event involved the local system and the legitimate Windows `svchost.exe` process. No evidence from this event alone indicated malicious activity.

**Result:** Likely benign based on available evidence.

---

### Event ID 4672 — Special Privileges

Multiple Event ID 4672 events were observed.

The investigated event was associated with the Windows `SYSTEM` account and contained multiple special privileges.

**Assessment:**

Highly privileged activity associated with the `SYSTEM` account can be expected during normal Windows operating-system activity. The event was not considered malicious based on the available context.

**Result:** Likely benign.

---

### Event ID 4625 — Controlled Failed Authentication

A controlled failed-login event was intentionally generated as part of this investigation by entering an incorrect Windows password once and then successfully authenticating.

**Observed characteristics:**

* Event ID: `4625`
* Failure Reason: `Unknown user name or bad password`
* Logon Type: `2`
* Process: `svchost.exe`
* Source Network Address: `127.0.0.1`

**Assessment:**

The event represented a failed interactive authentication attempt. The source address `127.0.0.1` is the local loopback address, indicating the activity originated from the local system.

Most importantly, the event was intentionally generated during the investigation. Therefore, it was determined to be a **controlled and benign security event**, rather than evidence of an external attack.

**Result:** Benign — controlled test event.

---

## Account Activity Investigation

The Security log was also checked for events associated with account creation and local security group membership.

### Event ID 4720

No Event ID 4720 events were identified.

**Assessment:** No evidence of a newly created user account was found within the available Security log data.

### Event ID 4732

No Event ID 4732 events were identified.

**Assessment:** No evidence was found of an account being added to a security-enabled local group within the available Security log data.

---

## Process Creation Investigation

Event ID 4688 was investigated to determine whether Windows was recording process creation events.

No Event ID 4688 events were available in the current Security log.

**Assessment:**

The absence of Event ID 4688 events does not prove that no processes were created. It indicates that process-creation auditing data was not available in the portion of the Security log examined during this investigation.

This distinction is important when interpreting security logs.

---

## Evidence

Sanitized screenshots from the investigation are included in the `screenshots` directory.

The screenshots demonstrate:

* Windows Event Viewer Security logs
* Event ID 4625
* Failed authentication details
* Logon Type 2
* Failure reason
* Process information
* Local source address

Sensitive system information such as the Windows username, computer name, and Logon ID has been removed from the screenshots before publication.

---

## Security Analysis

The investigation did not identify evidence of unauthorized access, account creation, privilege escalation, or suspicious external authentication activity.

The most significant event examined was Event ID 4625. Although failed authentication events can be indicators of brute-force attempts or unauthorized access, the event in this investigation was intentionally generated and originated from the local system.

This demonstrates an important security-analysis principle:

> **An individual security event should be evaluated within its context rather than automatically classified as malicious.**

Analysts should consider the event type, account, logon type, source, process, timing, and surrounding activity before determining whether an alert represents a genuine security incident.

---

## MITRE ATT&CK Relevance

The investigation focused primarily on Windows authentication and account activity.

Relevant MITRE ATT&CK concepts include:

* **T1078 — Valid Accounts:** Authentication events can be examined for potential misuse of legitimate credentials.
* **T1110 — Brute Force:** Repeated failed authentication events can be investigated for potential password attacks.
* **T1098 — Account Manipulation:** Account and group membership events can help identify unauthorized privilege or account changes.

No malicious execution of these techniques was identified during this controlled investigation.

---

## Skills Demonstrated

This project demonstrates practical experience with:

* Windows Event Viewer
* Windows Security Event Logs
* Event ID analysis
* Authentication log analysis
* Logon Type interpretation
* Failed authentication investigation
* Account activity monitoring
* Privilege-event analysis
* Basic incident investigation
* Evidence collection
* Security event correlation
* False-positive identification
* Security documentation
* GitHub portfolio development

---

## Lessons Learned

This investigation reinforced several important cybersecurity concepts:

1. **Context matters.** A failed login does not automatically indicate an attack.
2. **Event IDs provide useful investigative clues.** Understanding Windows Event IDs helps analysts quickly identify relevant activity.
3. **Source information is important.** Local and remote authentication events can have very different security implications.
4. **Legitimate Windows processes can appear in security events.** Processes such as `svchost.exe` should be investigated in context rather than automatically flagged.
5. **Missing logs are also findings.** The absence of Event ID 4688 data may indicate that the relevant auditing information is not currently being collected.
6. **Evidence should drive conclusions.** Security analysts should avoid making claims that cannot be supported by available evidence.

---

## Conclusion

This project provided hands-on experience investigating Windows authentication and security events using native Windows tools.

The investigation identified several normal Windows security events and included a controlled failed-authentication test. The available evidence did not indicate unauthorized access or malicious activity.

The project demonstrates the ability to collect security evidence, interpret Windows event data, investigate authentication activity, identify potential false positives, and document findings in a structured format.

---

## Repository Structure

```text
windows-security-investigation/
│
├── README.md
│
├── incident-report.pdf
│
├── screenshots/
│   ├── project2_4625_sanitized_1.png
│   ├── project2_4625_sanitized_2.png
│   └── project2_4625_sanitized_3.png
│
└── evidence/
    └── event-analysis.md
```

---

## Disclaimer

This project was conducted in a controlled environment on a personal Windows system for educational and portfolio purposes.

The failed authentication event documented in this project was intentionally generated as part of the investigation. It should not be interpreted as evidence of a real-world compromise.
