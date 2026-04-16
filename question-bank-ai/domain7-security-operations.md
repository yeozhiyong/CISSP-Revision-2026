Q1. Your SOC has deployed an AI-driven user-behavior analytics (UBA) engine that triggers on “impossible travel” events. Last night the engine alerted that the same user appeared to log in from Toronto and Tokyo three minutes apart, yet the authentication logs show a single successful Kerberos TGT issuance in Toronto and no evidence of credential replay. The user’s mobile device GPS history places them in Toronto the entire time.  
A. Close the ticket; the UBA engine is prone to benign positives when users utilize GPS-spoofing travel apps.  
B. Escalate to incident response; the discrepancy suggests a golden-ticket attack forged with a cloned KRBTGT hash.  
C. Accept the risk; geo-location data from mobile carriers is often delayed, explaining the mismatch.  
D. Tune the UBA rule to suppress alerts when Kerberos logs show only one TGT and mobile GPS corroborates the location.  

Correct Answer: B  
Explanation: A single TGT yet two geo-locations implies the remote session was authenticated without a second AS request—characteristic of a golden ticket created offline with the KRBTGT hash. The attacker can set any timestamp and source IP, producing “impossible travel” without additional Kerberos noise. GPS data from the real device remains in Toronto because the adversary never moved the physical asset. Treat as a Tier 0 breach and activate IR.

---

Q2. During a scheduled tabletop, the incident-response lead asks how to preserve evidence on a mission-critical Windows SQL cluster that CANNOT be taken offline. The CFO reminds the team that every minute of downtime costs USD 18 k.  
A. Run “dd” remotely across the C$ share to image drives while SQL stays live.  
B. Capture a volatile-data snapshot (RAM, network, registry) first, then leverage VSS to take a SAN-level snapshot of underlying LUNs.  
C. Install a FTK agent, push a full disk image to a forensic workstation, and accept the 4 % CPU hit.  
D. Pause SQL services for 90 seconds to unlock the MDF files and copy them to a USB drive.  

Correct Answer: B  
Explanation: Order of volatility rules mandate RAM and network state first. A SAN snapshot via Volume Shadow Copy Service (VSS) is crash-consistent and can be cloned without downtime; the database engine treats the snapshot as a sudden power loss and recovers on mount. This meets both evidentiary (bit-for-bit) and business-continuity requirements.

---

Q3. Your organization uses a single Active Directory forest with fine-grained password policies. A red-team exercise discovers that 11 service accounts are configured with “Password never expires” and are members of Domain Admins. The accounts have SPNs defined and show no failed logins in 400 days. Management refuses to disable them because “legacy billing needs them.”  
A. Convert each account to a group Managed Service Account (gMSA) and force Kerberos delegation restrictions.  
B. Schedule a quarterly 90-character password change and require smart-card pre-authentication.  
C. Document the risk as accepted and add compensating detective controls (SIU alerts on any new interactive logon).  
D. Remove SPNs, lower rights to Domain User, and create new dedicated user accounts for billing.  

Correct Answer: A  
Explanation: gMSAs give automatic, cryptographically random 240-byte passwords managed by the domain, eliminating manual expiry management while retaining the ability to use Kerberos SPNs. gMSAs cannot be used interactively, reducing lateral-movement risk, and can be scoped to specific hosts via msDS-HostServiceAccount. This solves both the “never expires” and the “Domain Admin” issues without breaking the billing service.

---

Q4. A SIEM rule fires: “Multiple AWS Console logins from the same Identity Center user but two different browser fingerprints within 5 min.” The source IPs are both in the AWS-owned EC2 address space and geolocated to us-east-1. The user swears she only uses her corporate laptop with Chrome. CloudTrail shows AssumeRole events with externalId matching the corporate IdP.  
A. Deactivate the user’s SSO account; the account is clearly compromised.  
B. Block all logins from EC2 public IP ranges via IAM policy.  
C. Open an AWS support case; the traffic is likely a proxy misrouting through VPC endpoints.  
D. Create a CloudWatch metric filter to suppress alerts when sourceIPAddress resolves to “ec2-*.compute.amazonaws.com”.  

Correct Answer: C  
Explanation: AWS Console logins from EC2 IPs usually indicate the user launched an in-browser VPC endpoint (AWS Systems Manager Session Manager, AWS CloudShell, or AppStream). The identical externalId and valid IdP signature mean the role assumption is legitimate. Suppressing or blocking would break valid workflows; instead verify proxy routing and, if confirmed, tune the rule to exclude corporate EC2 proxy ranges.

---

Q5. A Tier-1 analyst receives an alert that a production Linux web server executed “chmod 4777 /usr/bin/vi” at 02:13 local time. The change was rolled back four minutes later. The server is fully patched, and AIDE logs show no other file modifications.  
A. Close the alert; the rollback indicates an authorized administrator correcting a mistake.  
B. Escalate to Tier-2; the set-UID bit on vi is a classic backdoor allowing priv-esc by any account.  
C. Add a cron job every minute to reset /usr/bin/vi permissions to 755.  
D. Re-image the server; rootkit behavior is confirmed.  

Correct Answer: B  
Explanation: Setting set-UID root on vi grants any user root when exiting the shell (“:shell”). The four-minute window is enough for an attacker to plant a cron job or add an SSH key and then remove the bit to cover tracks. AIDE would miss in-memory or credential changes. Treat as potential compromise and escalate for timeline analysis, auditd review, and volatile capture.

---

Q6. A hospital uses biometric palm-vein readers at controlled entry points. During a power outage the generators fail, and the UPS lasts only 20 min. Emergency procedures require the security staff to switch to manual keys. A Joint Commission auditor asks how you will maintain “positive identification” of staff entering the NICU.  
A. Issue one-time QR codes via the hospital’s mobile app that do not require network power.  
B. Station two nurses who personally recognize each clinician and log entry/exit on paper.  
C. Use battery-powered handheld scanners synced with an offline copy of the employee DB on a laptop.  
D. Post a security guard with a flashlight and printed employee photo directory.  

Correct Answer: B  
Explanation: Regulatory frameworks (HIPSA & Joint Commission) accept “recognized-by” as a compensating control when electronic authentication is unavailable. Two-person recognition provides dual control and reduces collusion risk. Paper logs satisfy audit trail requirements until systems are restored.

---

Q7. Your company’s SOAR playbook auto-isolates any host that contacts a newly registered domain (age < 24 h) and downloads > 100 kB. Today the playbook isolated 120 sales laptops that auto-updated a legitimate VPN client whose vendor just switched CDN domains. Executives demand the playbook be disabled.  
A. Disable the playbook; business disruption outweighs the risk.  
B. Add a whitelist step that checks the file signature against the vendor’s published SHA-256 before isolation.  
C. Lengthen domain-age threshold to 30 days and raise download size to 5 MB.  
D. Require vendor domains to be pre-submitted through a security-review gate before go-live.  

Correct Answer: B  
Explanation: A cryptographic signature check is an objective control that does not rely on domain reputation and prevents recurrence for this vendor while preserving protection against novel malicious domains. It can be automated in SOAR within seconds, maintaining security with minimal friction.

---

Q8. A DevOps team uses containers orchestrated by Kubernetes. A vulnerability scan finds 14 Critical CVEs inside a base image pulled from Docker Hub. The image is inside a private registry that the CI/CD pipeline copies every night. Pods are ephemeral and live < 2 h.  
A. Patch the base image, push to registry with new tag, update deployment YAML, and perform a rolling update.  
B. Accept the risk; containers exist only two hours—exploitation window is too small.  
C. Add a NetworkPolicy to block egress from those pods and call it compensated.  
D. Re-run the scan with authentication to Docker Hub to confirm the CVEs are not false positives.  

Correct Answer: A  
Explanation: Short lifetime does not mitigate privilege escalation or lateral movement within the two-hour window. A rolling update with a patched base image is the only durable fix. NetworkPolicies provide defense-in-depth but are not a substitute for patching.

---

Q9. A security guard making night rounds notices a cardboard box labeled “HP Toner” sitting outside the secure print-room door. The next morning the CFO’s printer is found to have a hardware key-logger installed inside the device.  
A. Review CCTV for anyone accessing the printer after toner delivery; treat the box as potential evidence and secure it.  
B. Dispose of the box; it is unrelated to the key-logger found 12 h later.  
C. Scan the box for fingerprints; if none, discard.  
D. Alert procurement; HP must have shipped a counterfeit cartridge.  

Correct Answer: A  
Explanation: The box is physical evidence that may contain fingerprints, DNA, or tracking numbers linking to the adversary. CCTV correlation can establish timeline and attribution. Chain-of-custody must start immediately.

---

Q10. Your SOC uses MITRE ATT&CK mapping. A threat-hunt finds a workstation with “wmiprvse.exe” spawning “powershell.exe” that downloads a JPEG, extracts a base64 blob, and executes via regsvr32. The hunt coincides with a new signature hit on “APT29 – CARBANAK.” Management will fund only ONE additional control this quarter.  
A. Deploy application whitelisting (AppLocker) blocking regsvr32 for standard users.  
B. Disable WMI service across the domain via GPO.  
C. Force all PowerShell to v2 constrained language mode.  
D. Block JPEG downloads at the web proxy.  

Correct Answer: A  
Explanation: The kill-chain relies on regsvr32 to execute arbitrary scriptlets (T1218.010). AppLocker can block regsvr32 unless executed from trusted paths, breaking the technique without impacting legitimate system use. Disabling WMI or blocking JPEGs causes business disruption and does not stop alternate execution vehicles. Constrained Language helps but is bypassable if regsvr32 runs in full language context.
Q1. A global retailer’s SOC is shifting from a 4-tier to a 3-tier follow-the-sun model while simultaneously rolling out an expanded SOAR playbook. During the first weekend, analysts in Manila close 42 % more alerts than the week before, yet the Monday-morning hand-off to the Denver team contains only ticket numbers—no context or run-book links. At 09:12 Denver time, a SIEM rule fires on the same IP range that Manila had already “resolved” as “expected marketing scanner.” Denver re-opens the tickets and escalates them as false-positive tuning requests. Which security-operation metric is MOST directly degraded by this situation?  
A. MTTD (Mean Time to Detection)  
B. MTTR (Mean Time to Respond)  
C. MTTI (Mean Time to Innocence)  
D. MTTC (Mean Time to Contain)  

Correct Answer: B  
Explanation: The Manila team reduced MTTD by closing more alerts, but the lack of context forced Denver to re-validate the same activity, lengthening the overall response cycle (MTTR). MTTI is not a standard operations metric, and containment (MTTC) was never reached because the event was re-classified, not contained.

Q2. Your organization’s incident-response plan requires that every Severity-1 ticket be accompanied by a SHA-256 hash of the suspect binary before the SOC may escalate it to the malware team. During a tabletop exercise, the red-cell facilitator hands the SOC lead a USB drive labeled “ransomware sample” and asks for the hash. The lead plugs the drive into the analysis laptop, mounts it read-only, and runs sha256sum /dev/sdb. A junior analyst points out that this command hashes the entire block device—including slack space—rather than the file. The facilitator rules that the escalation requirement has NOT been satisfied. Which security-operations principle was most clearly violated?  
A. Chain-of-custody documentation  
B. Evidence integrity and repeatable hashing  
C. Least-functionality configuration  
D. Segregation of duties  

Correct Answer: B  
Explanation: An evidence hash must be reproducible by any competent examiner; hashing raw block data instead of the logical file produces a different value and violates integrity. Chain-of-custody (A) is not the primary issue, and least-functionality (C) or segregation (D) are not relevant here.

Q3. A SaaS provider runs a fully containerized micro-services platform on Kubernetes. During a routine image-hardening sprint, engineers replace the base image from ubuntu:20.04 to distroless, rebuild all pods, and push them to the production registry. Two hours later, the SOC notices that the EDR agents no longer report process events from those containers. The EDR vendor confirms that their kernel module cannot attach to the statically linked init process used by distroless images. Which security-operation control has been MOST severely weakened?  
A. Continuous monitoring / visibility  
B. Configuration management  
C. Patch management  
D. Identity and access management  

Correct Answer: A  
Explanation: EDR provides runtime telemetry; its inability to instrument the new image eliminates visibility, a core security-operations control. Configuration (B) and patch (C) processes worked as intended; IAM (D) is unaffected.

Q4. A hospital’s medical-device VLAN is air-gapped except for a weekly one-hour window when a vendor support laptop is connected to push firmware updates. During a quarterly audit, the SOC finds that the laptop’s antivirus pattern file is 14 months old and the OS last patched 18 months ago. The vendor claims the laptop is never online, therefore “unhackable.” Which security-operations concept BEST refutes the vendor’s assertion?  
A. Attack-surface reduction  
B. Island-hopping / pivot risk  
C. Zero-trust architecture  
D. Mean time to failure  

Correct Answer: B  
Explanation: The laptop is a pivot point; even brief connectivity allows malware implanted elsewhere to move into the high-value VLAN. This is classic “island hopping,” a core concern in security operations. Zero-trust (C) is a broader philosophy, not the best rebuttal to the specific claim.

Q5. A SOC manager wants to measure how quickly analysts can triage phishing emails. She configures the mail gateway to inject 10 benign “canary” messages per day that contain known-bad URLs hosted by the security team. After 30 days, only 83 % of the canaries have generated user-reported tickets, and the median user-report time is 4 h 12 m. Which metric is she actually calculating?  
A. Phish-click rate  
B. User-reporting efficacy  
C. Mean time to awareness  
D. Mean time to detect (MTTD) for email-borne threats  

Correct Answer: D  
Explanation: The experiment measures how long it takes the human sensor network to detect and report a phish—i.e., MTTD for that vector. It is not measuring who clicked (A), overall efficacy (B), or awareness (C).

Q6. A Fortune-100 company uses a central log lake with 90-day online retention and 2-year cold-store. A new privacy regulation requires that any EU employee IP address older than 30 days be “forgotten,” yet the SOC still needs to detect long-term attack campaigns. Which security-operations solution BEST balances compliance and detection?  
A. Crypto-shred all logs older than 30 days  
B. Pseudonymize the IP field with a salted hash and destroy the salt after 30 days  
C. Drop every log entry that contains an EU IP  
D. Move EU logs to an isolated, access-controlled bucket  

Correct Answer: B  
Explanation: Pseudonymization preserves the ability to correlate events by hashed IP for 30 days, after which the salt is destroyed, making re-identification computationally infeasible and satisfying “forgetting.” Crypto-shred (A) eliminates detection value, while dropping (C) or isolating (D) does not truly “forget” the data.

Q7. During a ransomware outbreak, the IR team decides to activate “isolation” playbooks that cut off the affected site by black-holing its /16 in BGP. The network-ops center reverts the change 45 minutes later, stating that the black-hole also stopped VoIP emergency phones and violated the safety SLA. Which security-operations document should be updated first to prevent recurrence?  
A. Incident response run-book  
B. Business Continuity Plan (BCP)  
C. Change-management policy  
D. Memorandum of Understanding (MOU) with the ISP  

Correct Answer: A  
Explanation: The IR run-book must contain pre-approved isolation options that consider safety and voice dependencies. BCP (B) is too high-level, change-mgmt (C) already existed but was overridden, and MOU (D) is irrelevant to internal safety systems.

Q8. A managed-security-service provider (MSSP) offers a 24×7 SOC to a small bank. The contract stipulates that the MSSP will maintain a 15-minute SLA for critical alert acknowledgment. After a firewall fails-open during a holiday weekend, the bank’s on-call CISO receives an email alert—but no MSSP call—for 3.5 hours. The post-mortem shows the ticketing system clock was 4 hours behind due to an unpatched NTP drift bug. Which security-operations concept is the ROOT cause of the SLA miss?  
A. Log-integrity failure  
B. Time-synchronization failure  
C. Escalation-path failure  
D. Monitoring-tool failure  

Correct Answer: B  
Explanation: The underlying issue is incorrect time, which broke the SLA measurement and acknowledgment logic. Log integrity (A) is not the primary issue, escalation (C) was triggered late, and the monitoring tool (D) fired correctly.

Q9. A DevOps pipeline uses Infrastructure-as-Code (Terraform) to spin up AWS environments. A developer accidentally commits an access-key ID and secret to a public GitHub repo. AWS GuardDuty generates a “CredentialExfiltration” finding 11 minutes later. The SOC disables the key via Lambda automation within 3 minutes, but the red-team later shows that the key was already used to launch 200 c5.4xlarge instances in another region. Which security-operations process should be implemented to reduce the probability that a future key can be abused within the 14-minute exposure window?  
A. Just-in-time (JIT) provisioning with automatic expiration  
B. Mandatory code-signing on every Terraform plan  
C. Region-lock IAM condition keys  
D. AWS Organizations SCP to deny ec2:RunInstances  

Correct Answer: A  
Explanation: JIT provisioning ensures the key does not exist long enough to be abused, directly shrinking the exposure window. Region-lock (C) and SCP (D) are useful but do not address the root issue of persistent credentials; code-signing (B) is unrelated.

Q10. A global manufacturing firm uses operational-technology (OT) controllers that can only log over Syslog UDP and cannot tolerate packet loss. The SOC wants to send these logs to the cloud SIEM, but the network team refuses to allow UDP/514 through the firewall, citing best-practice restrictions. Which security-operations architecture is the MOST secure compromise?  
A. Deploy a local log aggregator in the OT DMZ that converts UDP to TCP/TLS and forwards to the cloud  
B. Enable UDP/514 with stateful-inspection and rate-limiting  
C. Mirror the OT switch SPAN port to a cloud-connected collector  
D. Ask the vendor to upgrade firmware to support TCP  

Correct Answer: A  
Explanation: A local aggregator preserves the UDP requirement inside the plant while adding encryption and stateful forwarding, minimizing firewall exposure. Simply opening UDP/514 (B) is insecure; SPAN (C) is one-way but offers no log integrity; firmware upgrades (D) are often impossible on legacy OT gear.
Q1. Your SOC has deployed an AI-powered user-behavior analytics (UBA) engine that baselines every employee’s keyboard cadence, file-touch volume, and VPN-connect times. On a Saturday at 02:14 local time, the model alerts that the CFO’s credentialed session just exfiltrated 3.2 GB of compressed files to an IP in Moldova—something the CFO has never done. The SIEM shows no malware alert, and the EDR platform marks the endpoint “clean.” Which FIRST action best follows the SANS PICERL incident-handling continuum?  
A. Isolate the CFO laptop from the network to preserve evidence integrity.  
B. Immediately call the CFO on her registered phone to verify the transfer.  
C. Create a hash of the endpoint drive before the user returns on Monday.  
D. Escalate the alert to law-enforcement because a nation-state is suspected.  
Correct Answer: B  
Explanation: The alert is anomalous but not yet confirmed malicious (no malware, no failed auth). Per PICERL “Identification” phase, the first goal is to classify the event while avoiding disruption that could destroy evidence or business function. Calling the data owner (the CFO) is the least-intrusive, fastest way to determine if the activity is legitimate (e.g., emergency board presentation) without tipping off an intruder or destroying volatile evidence. Isolation (A) would be correct only after confirmation of compromise; imaging (C) is premature; external escalation (D) skips internal verification.

Q2. A DevOps pipeline that builds container images for a public-facing micro-service suddenly starts failing code-signing validation. The checksums of the last three images differ from the signed manifest even though the Git commit hashes are unchanged. The build servers are fully patched, and AV scans are negative. Which detective control would have MOST effectively uncovered the attack vector?  
A. FIM (File-Integrity Monitoring) on the compiler binary and libraries.  
B. DLP inspection of outbound traffic from the build subnet.  
C. NAC enforced 802.1X for every build-server NIC.  
D. SIEM correlation of failed login attempts against build accounts.  
Correct Answer: A  
Explanation: Unsigned or altered images with unchanged source point to tampering of the build toolchain—aka “build-phase” supply-chain attack. FIM would detect replacement or patching of the compiler, linker, or libraries that inject malicious code while keeping the source repo pristine. DLP (B) would see exfil only after the fact; NAC (C) limits network access but not host compromise; brute-force monitoring (D) is irrelevant because creds were not abused.

Q3. A hospital’s medical IoT VLAN segments patient monitors from the rest of the network via ACLs on a core switch. During a penetration test, the tester plugs into a vacant RJ-45 in a patient room and receives an IP address in the monitor VLAN, then successfully transmits spoofed vital-sign packets to the central telemetry server. Which security operations failure is PRIMARY?  
A. Lack of network-based IPS on the switch backplane.  
B. Missing MACsec encryption on switch-to-switch trunks.  
C. Improper network access control (NAC) and port-level authentication.  
D. Absence of code-signing on monitor firmware.  
Correct Answer: C  
Explanation: The tester achieved unauthorized layer-2 access and was placed in the wrong VLAN, indicating the switch port did not authenticate the device or assign it to a proper quarantine/employee VLAN. NAC with 802.1X/MAC-auth or dynamic VLAN would have prevented the connection. IPS (A) would not block a legitimate-looking packet; MACsec (B) encrypts trunks but not edge admission; firmware signing (D) is unrelated to network admission.

Q4. Your organization uses a fully managed DNS provider. Yesterday the provider’s name servers began returning 127.0.0.1 for your apex domain, causing a 6-hour customer outage. Post-mortem shows the provider fell victim to a credential-stuffing attack that changed your DNS A records. Which operational control would BEST have reduced the likelihood of this incident?  
A. DNSSEC with 2-factor-authentication on registrar locks.  
B. Secondary authoritative DNS on a different provider with hidden primary.  
C. Client-side DNS-over-HTTPS to prevent ISP spoofing.  
D. Continuous zone-transfer monitoring to detect changes within 5 minutes.  
Correct Answer: A  
Explanation: The root cause was unauthorized modification of records via compromised provider credentials. DNSSEC prevents tampering with integrity but does not stop account takeover; however, registrar-level locks coupled with 2FA on the provider portal would have blocked the attacker even with valid passwords. Secondary DNS (B) adds resilience but not authentication; DoH (C) protects only end-user lookups; zone-transfer monitoring (D) is detective, not preventive.

Q5. A SIEM rule fires when five failed logins on a Windows server are followed within ten minutes by a successful login from a new country. The SOC receives 30–50 such alerts nightly, and every investigated case so far has been a valid VPN user on holiday. Management asks the SOC to “tune out the noise.” Which tuning approach BEST preserves security value while reducing false positives?  
A. Raise the failure threshold to 20 and require the country to be on a “high-risk” list.  
B. Add a contextual enrichment check: suppress if user’s registered MFA device successfully authenticated from the same foreign IP within the prior 24 h.  
C. Remove the “new country” condition entirely and rely only on failure count.  
D. Disable the rule and create a new one that triggers only on impossible travel >3000 km in <2 h.  
Correct Answer: B  
Explanation: The false positive stems from legitimate travel. By correlating with MFA history (something the user has), the rule keeps detecting real takeovers while suppressing alerts when the user’s phone or token has already proven presence in that location. Raising failure count (A) ignores low-slow brute force; removing geo condition (C) discards a valuable signal; impossible travel (D) misses slow, distributed attacks.

Q6. A cloud-native e-commerce site runs in AWS. A Lambda function triggered by S3 “PUT” events suddenly begins executing 100× normal volume, driving 50 TB/month of data-transfer charges. CloudTrail shows the calls originate from 4,000 unique access keys that do NOT belong to your AWS account. Which detective mechanism would have identified the issue FIRST?  
A. GuardDuty finding for “S3 API requests from IPs on custom threat list.”  
B. Config rule detecting S3 bucket policy change that grants public “PutObject.”  
C. CloudWatch metric alarm on “NumberOfObjects” in the bucket.  
D. Cost-explorer budget alert set at 120 % of forecast.  
Correct Answer: B  
Explanation: The attacker is uploading objects into your bucket, causing Lambda invocations. The root cause is a bucket policy (or ACL) that allowed public writes—detectable by a Config rule evaluating policy JSON. GuardDuty (A) is second-line; CloudWatch (C) is lagging; cost alert (D) is too late and purely financial.

Q7. A manufacturing plant’s safety instrumented system (SIS) is air-gapped, but the data-diode that sends read-only sensor data to the business LAN was replaced during maintenance with a bi-directional serial cable. A month later, ransomware on the corporate side pivots into the SIS network and halts production. Which security-operations FAILURE is MOST critical?  
A. Lack of network segmentation inside the SIS zone.  
B. Inadequate change-management and configuration-control process.  
C. Missing antivirus on the SIS Windows HMIs.  
D. Absence of a hot-standby SIS controller for failover.  
Correct Answer: B  
Explanation: The data-diode was swapped for a bi-directional cable—a clear configuration change that broke the “air-gap.” A robust change-management process with security review and rollback testing would have caught the violation before go-live. Segmentation (A) helps but the root breach was the bidirectional path; AV (C) is secondary for legacy HMIs; failover (D) is continuity, not security.

Q8. A SOC analyst is building a playbook for “credential-stuffing against customer portal.” Which metric BEST measures the EFFECTIVENESS of the playbook’s containment step?  
A. Mean time to acknowledge (MTTA) the alert.  
B. Percentage of abused accounts disabled within 15 min of first successful login.  
C. Number of IPs added to the block-list per hour.  
D. Percentage of playbook steps executed without human intervention.  
Correct Answer: B  
Explanation: Effectiveness is outcome-based: reducing fraudulent access. Disabling compromised accounts quickly stops attacker lateral movement. MTTA (A) is responsiveness, not containment; block-list size (C) is activity, not impact; automation ratio (D) is efficiency, not effectiveness.

Q9. A red-team exercise reveals that help-desk staff routinely accept “I forgot my password” requests via personal Gmail accounts because the corporate VPN was down. No ticket exists in the ITSM system. Which security operations control is MOST appropriate to prevent recurrence?  
A. Publish a policy requiring password resets to occur only in person with government ID.  
B. Implement an out-of-band communications tool with pre-shared certificates and integrated workflow that enforces ticket creation before any reset.  
C. Deploy a redundant ISP and BGP path to ensure VPN is never down.  
D. Force all users to enroll in self-service password-reset with MFA questions.  
Correct Answer: B  
Explanation: The gap is unverified, undocumented out-of-band requests. A secure chat/phone app with mutual crypto authentication and built-in ticketing enforces traceability and identity proof even when primary VPN is unavailable. In-person (A) is impractical for remote staff; ISP redundancy (C) is good but does not address process failure; self-service (D) helps users but not help-desk policy violations.

Q10. A global company runs a 24×7 SOC with follow-the-sun staffing. After a major breach, auditors criticize the SOC for “lack of measurable continuous improvement.” Which KPI pair BEST demonstrates a maturing security-operations program?  
A. Number of phishing emails received and percentage reported by users.  
B. Mean time to containment and percentage of incidents with root-cause remediated within 30 days.  
C. Number of firewall rule changes and percentage approved within SLA.  
D. Percentage of servers fully patched and number of vulnerabilities per host.  
Correct Answer: B  
Explanation: A SOC’s maturity is judged by both speed (MTTC) and quality of fix (root-cause closure). Tracking containment shows operational agility; tracking root-cause remediation shows lessons-learned and avoidance of repeat incidents. Phishing metrics (A) are user-focused; firewall changes (C) are change-management; server patching (D) is vulnerability management—each adjacent but not direct SOC-process improvement metrics.
Q1. A global retailer’s SOC has been running a legacy SIEM that cannot parse JSON logs from the company’s new cloud-native payment application. During the first week of deployment, an attacker makes 200,000 micro-refund requests that individually fall below the dollar limit that would trigger the rule-based fraud engine. The SIEM shows “unknown log format” alerts, but analysts discard them as noise. Which security-monitoring principle has MOST clearly failed?  
A. Non-repudiation  
B. Asset identification  
C. Timely patching  
D. Visibility  
Correct Answer: D  
Explanation: Visibility is the ability to collect, normalize, and interpret relevant security data in real time. Because the SIEM could not parse the JSON logs, the malicious traffic was effectively invisible to the SOC, allowing the fraud to proceed unnoticed. None of the other choices describe the root cause; non-repudiation is about proof of action, asset identification is inventory-focused, and patching is unrelated to log-format support.

Q2. A manufacturing plant uses a safety instrumented system (SIS) that shuts down turbines when vibration exceeds 4 mm/s. The OT-security team wants to add a network IDS tap on the same span port that carries SIS traffic, but the plant engineer refuses, citing safety-critical latency. The CISO insists the IDS is necessary to detect Stuxnet-like malware. Which security-operations concept should the CISO cite FIRST to justify a compensating control that satisfies both parties?  
A. Risk-based patching cycle  
B. Segmentation with passive out-of-band monitoring  
C. Dual-control safe hand procedure  
D. Layered defense with fail-open sensors  
Correct Answer: B  
Explanation: Passive out-of-band monitoring (tap-only, no TCP reset) adds zero in-line latency, preserving the deterministic timing the SIS requires while still giving security visibility. This is a textbook compensating control when a primary control (inline IDS) conflicts with safety. Dual-control is procedural, not technical; patching is irrelevant to real-time latency; fail-open sensors still add microseconds and do not address the engineer’s core objection.

Q3. A SaaS provider runs a red-team exercise against its on-call rotation. At 03:17 local time, the red team triggers a high-severity alert in the customer-support portal. The automated call tree pages the L1 analyst in Singapore, who VPNs in, sees the alert is “red-team,” and immediately closes the ticket without further analysis. The red team then escalates to disk-wiper malware simulation, which the same analyst also ignores. Which security-operations metric is MOST directly undermined?  
A. MTTD (Mean Time to Detect)  
B. MTTR (Mean Time to Respond)  
C. False-positive rate  
D. Alert fatigue  
Correct Answer: B  
Explanation: The analyst detected the alert (so MTTD is near zero) but failed to respond appropriately; therefore MTTR is effectively infinite. Closing a ticket without analysis is a response failure, not a detection failure. False-positive rate measures incorrect alerts, whereas here the alert was correct (red-team activity). Alert fatigue may be a root cause, but the question asks which metric is undermined, and MTTR is the direct measure of response performance.

Q4. A hospital’s medical-device VLAN is air-gapped except for a one-way diode that exports syslog UDP packets to the SOC’s log lake. During an unannounced audit, the assessor plugs a laptop into the diode’s receive port and successfully sends SNMP set commands back to an MRI machine, changing its field-strength calibration. Which security-operations control has MOST clearly failed?  
A. Data integrity of logs  
B. Unidirectional security gateway enforcement  
C. Media sanitization  
D. Continuous vulnerability management  
Correct Answer: B  
Explanation: A true data-diode hardware enforces unidirectional flow at the physical layer (optical or electrical). The fact that the auditor could send commands back proves the diode was misconfigured or was actually a bidirectional bridge, defeating the control. Log integrity, media sanitization, and vulnerability management are not relevant to the failure of enforced one-way traffic.

Q5. A cloud-first company uses infrastructure-as-code (IaC) to spin up staging environments every night. A developer accidentally commits an AWS security-group rule that opens 0.0.0.0/0 on TCP 3389. The change is auto-applied at 02:00. At 07:00 the SOC receives an AWS GuardDuty alert “RDP brute force from 86 IP addresses.” The company wants to prevent recurrence. Which security-operations activity BEST breaks the error chain?  
A. Run nightly penetration tests  
B. Implement a pull-request check with Open Policy Agent that blocks high-risk rules  
C. Increase GuardDuty sensitivity  
D. Rotate AWS access keys every 90 days  
Correct Answer: B  
Explanation: Blocking the bad IaC template before it is ever merged removes the vulnerability at the source, aligning with “shift-left” secure-devOps practices. Pen-testing is detective/after-the-fact, GuardDuty sensitivity does not stop the rule deployment, and key rotation is unrelated to security-group misconfiguration.

Q6. A SOC manager is building a runbook for “possible DNS-tunneling.” The organization has 40,000 endpoints and uses a recursive DNS resolver that logs every RR to Kafka. Which KPI should be used FIRST to tune the detection so that analysts are not flooded with false positives?  
C. Ratio of NXDOMAIN responses to total queries per domain  
D. Percentage of queries longer than 52 characters that resolve to non-routable IPs  
Correct Answer: C  
Explanation: Legitimate software rarely causes a high NXDOMAIN ratio; DNS tunnels generate many non-existent subdomains to exfiltrate data. Measuring this ratio provides a high-signal, low-noise first filter before deeper inspection. Query length alone can be high in CDNs, and non-routable IPs are not necessarily suspicious. Counting unique domains per IP is secondary and more computationally expensive.

Q7. A financial regulator requires that trading firms keep “immutable logs” for seven years. A firm implements WORM (write-once-read-many) S3 buckets with object-lock in compliance mode for 2,555 days. Six months later, an attacker compromises a cloud admin account and creates a new bucket lifecycle rule that moves objects to Glacier Deep Archive, then deletes the bucket policy. The firm argues the logs are still immutable because object-lock is intact. Which security-operations concern BEST refutes the firm’s claim?  
A. Availability of logs for regulatory inquiry  
B. Confidentiality impact due to Glacier encryption  
C. Integrity hash algorithm collision risk  
D. Non-repudiation of administrative actions  
Correct Answer: A  
Explanation: While object-lock preserves the bytes, moving logs to Glacier Deep Archive can delay retrieval for weeks, impeding a regulator’s request for timely access. This violates the spirit of “readily producible” evidence. Confidentiality is not at issue (Glacier encrypts), hash collision is theoretical, and non-repudiation is unrelated to storage tier.

Q8. A small SOC has two analysts on the night shift. A worm propagates at 01:48, generating 1,800 new alerts per minute. The SIEM auto-creates tickets, but the analysts spend 30 minutes trying to suppress the alert storm instead of containing the worm. After-action review shows the top three alert types were identical except for source IP. Which SOAR playbook component would BEST optimize future response?  
A. Alert deduplication with sliding-window correlation  
B. Threat-hunting hypothesis library  
C. Manual approval step for firewall changes  
D. Full packet-capture retention for 30 days  
Correct Answer: A  
Explanation: Deduplication collapses identical alerts into a single ticket with a count, freeing analysts to act on the incident rather than wade through noise. A hunting library is proactive, manual approval slows response, and packet retention is forensic storage, none of which address alert volume.

Q9. A company uses a managed DNS provider that offers a 5-minute TTL. During an incident, the SOC wants to sinkhole a malware domain by redirecting it to a internal honeypot web server. However, the provider’s API is throttled to 10 requests per minute and the domain has 200 A records. The SOC also fears that sudden global DNS changes might impact remote workers’ split-tunnel VPN. Which security-operations procedure BEST balances speed and safety?  
A. Lower the TTL to 30 seconds for all zones first, then update records incrementally  
B. Create a RPZ (Response Policy Zone) feed and push it to internal recursive resolvers  
C. Ask the ISP to null-route the domain at the BGP level  
D. Use the provider’s bulk-edit GUI during the next maintenance window  
Correct Answer: B  
Explanation: RPZ allows instant, local redirection of the domain for internal users without touching external DNS or rate limits, and it affects only the company’s resolvers, avoiding global impact. Lowering TTL first still faces API throttling and external propagation delays. BGP null-route is overkill and affects availability beyond the company. Waiting for a maintenance window violates incident-response timeliness.

Q10. A security operations center has deployed an EDR solution that hashes every executable on endpoints and compares SHA-256 values to a cloud reputation service. A red-team operator launches a custom Cobalt Strike beacon that re-compiles itself with a 4-byte NOP sled every execution, producing a unique hash each time. The EDR allows the process because the hash is unknown but not explicitly malicious. Which security-operations countermeasure BEST closes this gap without adding excessive false positives?  
A. Block all unsigned binaries  
B. Enable behavioral detection that scores process injection, named-pipe creation, and outbound POST to non-standard TLDs  
C. Increase the frequency of full-disk hash sweeps  
D. Whitelist hashes for all approved software  
Correct Answer: B  
Explanation: Behavioral detection looks at runtime actions rather than static hashes, making it resilient to polymorphic code. Blocking all unsigned binaries would break legitimate scripts and open-source tools. Full-disk sweeps are retrospective and do not prevent execution. Whitelisting hashes is exactly what the red team is bypassing.
Q1. During a routine SIEM review, a SOC analyst notices that a single user account has generated 15 failed-logon events from three different source IP addresses in the last 10 minutes, followed by a successful logon from a fourth IP address. The organization’s incident-response plan labels this pattern as “Suspicious—Possible Credential Stuffing.”  
A. Immediately disable the user account and request a password change at the next help-desk call.  
B. Leave the account active but silently increase SIEM polling to every 30 seconds and notify the user’s manager.  
C. Close the ticket because the logon ultimately succeeded, indicating the correct password was used.  
D. Escalate to tier-2 analysts for containment while leaving the account enabled to preserve potential live attacker activity.  

Correct Answer: A  
Explanation: Multiple failed logins from disparate IPs followed by success is a textbook credential-stuffing indicator. The first duty is to stop further abuse by disabling the compromised account and forcing a controlled password reset. Leaving the account active (B, D) risks lateral movement or data exfiltration, while closing the ticket (C) ignores the clear attack pattern.

---

Q2. A manufacturing plant’s safety instrumented system (SIS) is air-gapped from the corporate network. A junior engineer brings a personal laptop from home, connects it to the SIS engineering workstation via USB, and accidentally introduces ransomware that halts production.  
A. Re-image the engineering workstation and resume operations; no further action is needed because the SIS is air-gapped.  
B. Sanction the engineer, then update the air-gap policy to prohibit personal devices and enforce USB blocking via endpoint controls.  
C. Restore the SIS from last night’s network backup stored on the corporate SAN.  
D. Update the firewall rules between the corporate network and the SIS to block ransomware command-and-control traffic.  

Correct Answer: B  
Explanation: The root cause is policy failure—air-gap security was undermined by human behavior. Re-imaging alone (A) ignores recurrence risk; the SIS has no network path so firewall changes (D) are irrelevant; corporate SAN backups (C) are useless because the SIS was never backed up there. A policy control coupled with technical enforcement (B) is the only sustainable fix.

---

Q3. A company uses a cloud-based CASB to enforce DLP. An employee uploads 200 GB of customer PII to a personal Google Drive from a corporate laptop while connected to the office guest Wi-Fi. The CASB logs the event but does not block it.  
A. Tune CASB policies from “monitor” to “block” for file uploads > 50 MB containing PII.  
B. Disable guest Wi-Fi because it bypasses the corporate proxy that the CASB relies on.  
C. Re-image the employee laptop to eradicate shadow-IT software.  
D. Revoke the employee’s domain admin privileges.  

Correct Answer: A  
Explanation: The policy gap is the CASB’s enforcement level, not the Wi-Fi segment (B). Guest Wi-Fi still routes through the same NAT gateway where the CASB API integration can function. Re-imaging (C) is overkill and doesn’t fix policy, and the employee is unlikely to need domain admin (D) for this leak. Switching from monitor to block (A) closes the DLP hole.

---

Q4. A SOC runs a 24/7 follow-the-sun model with three regional teams. A critical privilege-escalation CVE is published at 08:00 UTC. The APAC team has already finished its shift, EMEA is mid-shift, and the Americas team is not yet online. Management wants “virtual patching” via WAF rules within 2 hours.  
A. Wait for the Americas team to start its shift in 4 hours; they own the WAF.  
B. Grant the EMEA team temporary WAF admin rights and document the change in the shift-turnover log.  
C. Email the vendor for an official hotfix and defer WAF changes until it arrives.  
D. Escalate to the CISO and schedule an emergency change-advisory-board meeting in 24 hours.  

Correct Answer: B  
Explanation: The goal is to meet the 2-hour SLA. Temporary access with full logging (B) respects least-privilege while enabling timely mitigation. Waiting (A) or CAB bureaucracy (D) blows the SLA; relying on vendor hotfixes (C) ignores virtual-patch options.

---

Q5. A security guard making night rounds notices a laptop in the conference room is projecting a fake Outlook login page. The room was booked by a visitor who left 30 minutes earlier.  
A. Power off the projector, confiscate the laptop, and call the on-call incident lead.  
B. Unplug the laptop’s network cable to stop data exfiltration.  
C. Take photos for evidence, leave everything untouched, and notify the SOC.  
D. Confront the visitor in the parking lot and demand identification.  

Correct Answer: C  
Explanation: Physical evidence integrity is paramount. Powering off (A) or unplugging (B) alters volatile memory that may contain indictors. Confrontation (D) is unsafe and outside a guard’s authority. Preserving the scene and alerting the SOC (C) maintains chain of custody and allows forensic imaging.

---

Q6. A DevOps team uses containers orchestrated by Kubernetes. A runtime security tool detects that a pod is executing /bin/sh with a newly spawned reverse-shell process. The image hash matches the approved golden image, but the PID tree shows the shell descended from an Apache worker.  
A. Delete the pod, rebuild the image from Dockerfile, and push to the registry with a new hash.  
B. Isolate the node with a network policy, snapshot the pod for forensics, and restart the workload on a clean node.  
C. Update the image vulnerability scanner to block future Apache images.  
D. Add a seccomp profile blocking /bin/sh to the deployment YAML and roll out the change.  

Correct Answer: B  
Explanation: The golden-image hash match indicates runtime compromise, not build-time flaw. Immediate isolation and forensic snapshot (B) preserves evidence while restoring service. Deleting the pod (A) destroys artifacts; updating scanner (C) won’t catch runtime-only exploits; seccomp (D) is preventive but too late for the active incident.

---

Q7. A SIEM rule fires on “impossible travel” when a user logs in from New York and then from Sydney five minutes later. Investigation shows the user is a developer who scripted an API call from a Sydney VPS listed on a major cloud provider.  
A. Disable the user account and treat the event as account takeover.  
B. Update the SIEM rule to exclude logins from known cloud-provider IP ranges.  
C. Require mandatory MFA re-enrollment for the developer.  
D. Add a note to the ticket: expected behavior; no further action.  

Correct Answer: D  
Explanation: The developer’s explanation is plausible and verifiable; the rule is too noisy. Closing with documentation (D) avoids alert fatigue. Disabling (A) or forcing MFA (C) punishes legitimate activity; globally excluding cloud IPs (B) could blind the SOC to real takeover using those same ranges.

---

Q8. A forensic analyst is asked to image a Windows laptop that may contain evidence of IP theft. The laptop is BitLocker-encrypted and powered on. The user is on vacation and unreachable.  
A. Pull the plug, transport the laptop to the lab, and use a bootable imager.  
B. Use the live system’s administrator account to suspend BitLocker, then run dd over the network.  
C. Capture volatile memory first, then use manage-bde to create a backup key package, and image decrypted volumes.  
D. Ask HR to reset the user’s password, log in, and disable BitLocker permanently.  

Correct Answer: C  
Explanation: Volatile memory may contain encryption keys or running malware. Capturing RAM first, then leveraging manage-bde with a forensic key package (C), preserves evidence integrity. Cold-boot imaging (A) loses RAM and risks TPM lockout. Suspending BitLocker while live (B) tampers the system; disabling it permanently (D) alters state and is legally risky without court order.

---

Q9. A DLP solution flags an e-mail sent by the CFO to a public webmail domain containing an attachment labeled “Q4_Financials_Encrypted.xlsx” that is password-protected. The DLP engine cannot inspect the attachment contents.  
A. Block the e-mail and require the CFO to use the secure file-transfer appliance instead.  
B. Allow the e-mail because the file is encrypted and therefore safe.  
C. Ask the CFO for the password, decrypt the file, inspect it, then re-send.  
D. Log the event but take no action; executives are exempt from DLP policies.  

Correct Answer: A  
Explanation: Encryption and password protection defeat content inspection, creating a data-exfiltration vector. A secure file-transfer appliance provides audit trails and encryption without exposing data to public webmail. Executives are never exempt (D), and requesting passwords (C) is intrusive and unscalable.

---

Q10. A company’s disaster-recovery plan specifies a 4-hour RTO and 30-minute RPO for its customer portal. During the annual drill, the restore from incremental snapshots takes 5.5 hours, and the last snapshot was 45 minutes old.  
A. Accept the result; the plan is “close enough” and still within industry norms.  
B. Increase snapshot frequency to every 15 minutes and pre-stage warm standby VMs to meet the 4-hour RTO.  
C. Lower the documented RTO/RPO to match actual performance.  
D. Switch from incremental to full nightly backups to speed recovery.  

Correct Answer: B  
Explanation: The drill revealed a gap against contractual RTO/RPO. Tightening snapshot cadence and using warm standbys (B) directly addresses both metrics. Revising targets downward (C) hides the problem; full backups (D) would lengthen, not shorten, restore times due to larger data volume.
Q1. A global SaaS provider’s SOC has deployed an AI-driven user-behavior analytics (UBA) platform. Over a 7-day period the engine alerts on a sales rep who normally works 09:00-17:00 ET but whose account is now generating API calls from IP space registered in Romania at 03:00 ET. The first three alerts are investigated and closed as “false positive—user on vacation using personal VPN.” On the eighth night the same credential pair issues 4 000 API calls that exfiltrate 3 TB of CRM data to the same Romanian ASN. Which flaw in security-operation **process** is MOST to blame?  
A. Lack of a formal incident-response playbook for geo-impossible travel  
B. Missing digital rights management (DRM) on the CRM records  
C. Inadequate secure coding practices in the SaaS application  
D. Absence of network micro-segmentation for the API tier  

Correct Answer: A  
Explanation: The UBA detected anomalous behavior, but the SOC dismissed it without updating the user-risk profile or building a pattern that would auto-escalate. A playbook that forces MFA re-challenge, account suspension, or manager confirmation when “impossible travel” re-occurs within a sliding window would have broken the attack chain. DRM, secure coding, and micro-segmentation are useful controls, but they do not address the operational failure to act on repeated, high-fidelity alerts.

---

Q2. Your organization’s on-premises SIEM forwards syslog messages to a new managed SOC that operates in a different time zone (UTC+2). After the cut-over, analysts complain that forensic timelines are “off” by four hours, causing root-cause analyses to be rejected by auditors. Which security-operation task should be performed **first** to restore evidentiary integrity?  
A. Re-issue NTP keys and enforce TLS syslog transport  
B. Normalize all log sources to a single time reference (e.g., UTC)  
C. Increase the SIEM retention license to 365 days  
D. Enable hash chaining (write-once-read-many) on the log storage  

Correct Answer: B  
Explanation: Time synchronization is foundational for correlation and court admissibility. Until every sensor, OS, and middleware device agrees on the clock, other controls (encryption, retention, WORM) will not fix timeline drift. UTC is the accepted forensic standard because it removes ambiguity introduced by regional daylight-saving rules.

---

Q3. A manufacturing plant uses 24×5 operations. Saturday morning the facility manager powers down non-critical PLCs so maintenance can replace relays. On Monday the CISO discovers that one of the PLCs re-booted with firmware three versions older than the Friday image, and the attacker tunnelled into the corporate ERP through the PLC’s back-door account. Which security-operation maturity gap BEST explains the compromise?  
A. Absence of change-control review for operational technology (OT)  
B. Missing next-generation antivirus on Windows HMIs  
C. Inadequate firewall rule complexity between Level 2 and Level 3  
D. Lack of a redundant hot-site data center  

Correct Answer: A  
Explanation: The root cause is an unauthorized firmware rollback that occurred outside the change window. A mature OT change-management process would have required cryptographic hash validation, version whitelisting, and security-team sign-off before allowing the PLC to rejoin the network. Antivirus and firewall rules are secondary; the hot-site is irrelevant to this causal chain.

---

Q4. A cloud-first retailer runs a serverless checkout flow in AWS Lambda. During a flash-sale event the SOC notices that 5 % of payment transactions trigger the “Invoke-From-Unknown-Region” CloudWatch alarm. The Lambda execution role has `s3:GetObject` privileges to a bucket that stores full credit-card magnetic-stripe images for troubleshooting. Which **FIRST** responder action is MOST aligned with ISC²’s “contain, eradicate, recover” philosophy?  
A. Revoke the Lambda role’s `s3:GetObject` permission with an inline SCP  
B. Snapshot the S3 bucket for chain-of-custody before any changes  
C. Increase the Lambda concurrency limit to reduce queue time  
D. Open a Sev-1 ticket with AWS Support to roll back API Gateway  

Correct Answer: A  
Explanation: Immediate containment is achieved by removing the excessive privilege that allows Lambda to access sensitive card data (violating PCI DSS 3.2.1 Req. 7). Snapshots come after the attack surface is closed; concurrency and API Gateway changes do not address the data-exposure vector.

---

Q5. The SOC has implemented a threat-hunting hypothesis: “If a red-team tool such as Cobalt Strike is present, then we will find unregistered Windows services with random 4-byte service names.” The hunters run the query across 12 000 endpoints and receive 47 hits. After removing known false positives, three assets remain. Which **NEXT** step BEST demonstrates adherence to the “analyst-centric” hunting model?  
A. Automatically quarantine the three endpoints and open an incident  
B. Create an STIX/TAXII feed and push the IoCs to all perimeter proxies  
C. Manually triage each endpoint to confirm beaconing and collect volatile artifacts before containment  
D. Re-image the endpoints during the next patching window  

Correct Answer: C  
Explanation: Hunting is a human-driven process that emphasizes understanding the environment. Automated containment (A) or re-imaging (D) could destroy evidence and miss lateral movement. Pushing IoCs (B) is useful but premature until the artifacts are validated. Manual triage preserves volatile memory and establishes scope.

---

Q6. A hospital’s medical device network is air-gapped except for a one-way diode that exports HL7 messages to the billing VLAN. During a ransomware event the MRI controllers display the ransom note, yet the diode logs show zero outbound packets. Which security-operation principle is MOST likely violated?  
A. Network segmentation failure—diode is actually bidirectional  
B. Least-functionality baseline—SMB shares were left enabled on MRI  
C. Patch-management gap—WannaCry exploited EternalBlue  
D. Media sanitization—old patient records were not cryptographically erased  

Correct Answer: A  
Explanation: A true unidirectional diode cannot carry return traffic; therefore the presence of the ransom note implies the “air-gap” is bridged. The immediate operational failure is architectural—either the diode is misconfigured or a covert channel (e.g., USB, RF) exists. While SMB and EternalBlue are plausible attack vectors, the question asks which principle is violated by the diode’s behavior, not the exploit itself.

---

Q7. A SaaS company’s incident-response retainer requires the MSSP to meet a 4-hour SLA from ticket open to containment. During a credential-stuffing attack the on-call analyst is stuck in a countryside area with only 2G data service and cannot VPN into the jump host. Thirty minutes later the customer’s single-sign-on (SSO) is breached, leading to 6-hour downtime. Which **BEFORE-the-fact** security-operation control would have BEST reduced the likelihood of SLA breach?  
A. Deploy an out-of-band cellular console server with 2-factor auth on the jump host  
B. Move the SSO architecture to a zero-trust model  
C. Increase the retainer to include 24×7 phone-based escalation  
D. Implement rate-limiting on the SSO login endpoint  

Correct Answer: A  
Explanation: An out-of-band console provides a non-Internet path for responders when primary ISP or VPN fails, ensuring the 4-hour SLA remains attainable regardless of the analyst’s location. Zero-trust and rate-limiting are preventive but do not guarantee the **response** SLA can be met; phone escalation helps but still requires the analyst to gain access.

---

Q8. A security team subscribes to a commercial threat-intel feed that delivers SHA-256 hashes of ransomware binaries within 30 minutes of sample discovery. The SOC’s SOAR platform is configured to auto-block these hashes on the enterprise EDR. During a post-mortem the CISO notes that the same ransomware still successfully executed on 42 workstations. Hash-mismatch analysis shows the malware re-packed itself every 45 minutes. Which security-operation improvement is MOST effective?  
A. Switch from hash-based to behavioral YARA rules delivered via the same feed  
B. Increase the SOAR poll frequency to every 10 minutes  
C. Add a second feed to cross-reference hashes  
D. Enable application whitelisting with publisher-based rules  

Correct Answer: A  
Explanation: Hash agility defeats static IoCs; behavioral signatures (e.g., YARA) targeting core ransom functionality (file entropy spike, rapid rename, shadow-copy deletion) remain effective across packer mutations. Faster polling or additional feeds still rely on the flawed hash indicator, whereas publisher rules may break legitimate unsigned tools.

---

Q9. A federal agency uses a continuous-diagnostics-and-mitigation (CDM) dashboard that displays the average time to patch critical vulnerabilities across 50 000 endpoints. The CIO rewards IT teams whose CDM score improves month-over-month. Over two quarters the mean time drops from 28 days to 3 days, yet the number of incident-response activations for malware **increases** by 40 %. Which security-operation metric dysfunction BEST explains the paradox?  
A. Gaming—teams patch low-risk workstations first to improve the average while deferring high-value servers  
B. Lack of asset criticality weighting in the CDM risk algorithm  
C. Absence of a formal security-awareness program  
D. Over-reliance on CVE-based scanning instead of agentless discovery  

Correct Answer: A  
Explanation: When KPIs are tied to simple arithmetic means, staff optimize the metric rather than the risk. Patching 1 000 lab laptops in one day dramatically improves the average while mission-critical domain controllers remain unpatched, leading to higher compromise rates. Criticality weighting (B) is a fix, but the immediate dysfunction is the incentive structure that encourages gaming.

---

Q10. A DevOps pipeline uses Infrastructure-as-Code (Terraform) to spin up ephemeral Kubernetes clusters in GCP. During a security exercise the red team compiles a custom kernel module that sniffs inter-pod traffic and exfiltrates TLS session keys. The SOC wants to prevent **future** compilations in production containers. Which security-operation control is the MOST operationally sustainable?  
A. Enable the GCP Shielded VM integrity monitor and enforce secure boot  
B. Add a Terraform sentinel policy that blocks images containing gcc, make, or kernel headers  
C. Deploy a sidecar container with Falco to alert on `ptrace` or `insmod` syscalls  
D. Re-write all micro-services in a memory-safe language such as Rust  

Correct Answer: B  
Explanation: Preventing build toolchains from entering production is a deterministic, policy-as-code control that eliminates the attack vector at build time without runtime overhead. Shielded VMs (A) protect the host, not the container userland. Falco (C) is detective, not preventive. Rewriting code (D) is a long-term development goal, not a quick security-operation fix.
Q1.  
Your SOC has deployed a new behavioral-analytics engine that baselines every workstation’s outbound TLS fingerprinting.  
On Monday at 09:12 UTC the engine alerts: “Host WS-0147 established 4,311 outbound TLS sessions in 10 minutes to 1,177 unique IPs, all with the JA3 client-fingerprint 4d41c7c3079c5140e5468a8b9e5f7f9f; certificate chain CN=*.cdn-edge[.]com; no associated user-agent or SNI mismatch.”  
Simultaneously, NetFlow shows each flow transferred 22–36 bytes outbound and ≈ 1.8 MB inbound—an inversion of normal web-browsing ratios.  
The host’s EDR shows the parent process as C:\Windows\System32\svchost.exe -k netsvcs -p -s Schedule, but the scheduled-task XML has a creation time of 09:08 UTC from an account that is not on the local SAM.  

Which of the following incident-response steps is MOST likely to contain the root cause while preserving evidence for civil litigation?  

A. Immediately isolate WS-0147 from the network by disabling the switch port, then snapshot its RAM via the EDR console.  
B. Create a firewall rule to block the destination AS, then run “schtasks /delete /tn *” on WS-0147 to remove attacker tasks.  
C. Use the EDR to quarantine the svchost.exe process, then take a full disk image to a forensic workstation over the production LAN.  
D. Snapshot the memory first, then use the hypervisor to power-off the VM and clone its disk to a WORM repository before isolating it.  

Correct Answer: A  
Explanation:  
The alert describes a classic reverse-shell beaconing pattern: a rogue scheduled task (lateral-movement persistence) spawning from a trusted Windows binary, performing TLS floods with fixed JA3 fingerprints to a CDN domain that is most likely attacker-controlled. The byte-ratio inversion (tiny outbound, large inbound) indicates data exfiltration or command downloads.  
Choice A preserves volatile memory (which will contain encryption keys, network buffers, and the injected shellcode) while immediately stopping further exfiltration or lateral movement. It also keeps the disk intact for later imaging.  
B leaves the host powered on and deletes task artifacts—destroying evidence and possibly crashing the malware before memory capture.  
C quarantines the wrong process—svchost is only the parent, not the malicious thread, and imaging across the production LAN risks contaminating evidence.  
D powers the machine off, losing memoryresident IoCs (scheduled-task encryption keys, live C2 sessions) and is therefore less forensically sound than A.  

Q2.  
Your global SaaS company runs a 24×7 follow-the-sun SOC.  
Last quarter the MTTR for P1 incidents averaged 42 minutes, but the new board metric requires ≤ 20 minutes by year-end.  
A post-incident review shows that 65 % of the delay occurs between “alert generation” and “first human triage,” because the on-call engineer in the relevant time zone must be woken up, VPN in, and manually open the ticket.  
You have already tuned detection logic to reduce false positives by 40 % and hired two extra tier-1 analysts per shift.  

Which single Security-Operations improvement will BEST meet the ≤ 20-minute target while maintaining segregation of duties?  

A. Implement automatic containment playbooks that isolate any host matching high-confidence IoCs, then notify engineers.  
B. Replace e-mail-based on-call with a cloud SOAR platform that auto-creates tickets, enriches alerts with threat-intel, and escalates via push-notification to the primary/secondary on-call analyst in under 3 minutes.  
C. Deploy a redundant SIEM in each region so that alerts are generated twice, guaranteeing at least one successful notification path.  
D. Authorize tier-1 analysts to perform full remediation without secondary approval for all P1 alerts, cutting escalation time to zero.  

Correct Answer: B  
Explanation:  
The bottleneck is human latency between alert birth and first eyeball; everything after triage already meets the 20-minute window.  
B directly attacks that gap: SOAR immediately opens the ticket, enriches the alert (reduces research time), and simultaneously pages the correct analyst’s phone/watch, cutting the 65 % delay to ≈ 3 minutes while preserving human judgment for later containment decisions.  
A shaves minutes but introduces unapproved auto-containment risk (possible business outage) and does not shorten triage itself.  
C adds redundancy but does not speed human response; duplicate alerts may even increase confusion.  
D violates segregation-of-duties and introduces high risk of erroneous remediation; it may shorten MTTR but fails on governance and could increase MTTI (mean time to innocence) for false positives.
