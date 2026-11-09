# Course investigations and remediation

This is the practical work the home lab supported during the cybersecurity lab course. The detailed writeups live in the [coursework portfolio](https://github.com/RDMRock/cybersecurity-lab-portfolio). The table connects each exercise to the evidence and investigation skills it developed.

| Work | Concrete result | Interpretation |
| --- | --- | --- |
| Discovery and assessment | Three lab hosts discovered. SYN, connect, and full TCP scans identified the same 14 open ports on the Windows target. | Network inventory and service exposure, followed by more specific SMB OS identification and vulnerability triage. |
| Remote execution | An authenticated auxiliary SMB run returned SYSTEM identity; a separate exploit opened a Meterpreter session. | Scan output and proof of execution are different evidence levels. The authenticated run's prerequisite matters. |
| Process and privilege analysis | Checked process identity after migration and a successful local escalation following an unsuccessful `getsystem` attempt. | Architecture, access rights, and the running account affect what a session can do. |
| Persistence | A Startup-folder method connected after user login. A separate service method connected after reboot before login. | Payload placement and startup configuration required a later callback to establish persistence. |
| Credential analysis | Distinguished account identities and hash fields, recovered a lab password, and verified a changed hash when a tool's long-candidate behavior interfered. | Tool limits must be separated from operating-system limits. No password or hash values are reproduced here. |
| Packet and TLS inspection | HTTP form data was readable in capture. HTTPS traffic was protected. A trusted lab proxy produced readable HTTPS flows and a proxy-issued certificate. | The interception result depended on deliberately changing the lab browser's trust. |
| DNS and controlled phishing | Observed lab name redirection and one controlled campaign's sent/opened/clicked/submitted sequence with dummy fields. | Send logs alone did not establish client acceptance; one recipient is not an awareness-study success rate. |
| Browser behavior | Diagnosed certificate trust, CSP, Private Network Access, and malformed HTML separately. | A fetched script, an executed script, and an online hooked browser are distinct observations. |
| Web remediation | Repeated normal and previously malicious requests after four focused route patches. | Preserved normal behavior and checked the specific unsafe path that each patch addressed. |
| MCP hardening | Replaced unsafe database, Git, and file operations. Ten standalone regression tests are published. | Tests support those exercised code paths. Per-caller authorization and deployment hardening require additional work. |

## Strong examples to review

- [Windows post-exploitation investigation](https://github.com/RDMRock/cybersecurity-lab-portfolio/blob/main/case-studies/03-windows-post-exploitation-and-ai-authorization.md)
- [Browser troubleshooting and MCP defenses](https://github.com/RDMRock/cybersecurity-lab-portfolio/blob/main/case-studies/06-browser-security-and-mcp-hardening.md)
- [Web fixes with original before/after observations](https://github.com/RDMRock/cybersecurity-lab-portfolio/blob/main/case-studies/07-web-vulnerabilities-and-remediation.md)

The AI-bank and RAG exercises were deliberately vulnerable teaching applications. Their observed disclosures are course results, separate from the ongoing Shopify research. No finding against a production bank is claimed.

## Next development step

The existing experience gives me attack and remediation context. My next lab step is to build a repeatable defensive telemetry workflow: collect events, preserve a benign comparison, write a detection, test expected matches and nonmatches, and document an investigation. That continuous monitoring pipeline is planned, not a completed deployment in this repository.
