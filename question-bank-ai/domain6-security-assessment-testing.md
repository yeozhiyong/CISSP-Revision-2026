Q1. A global retailer is preparing for its first ISO 27001 certification audit. The CISO wants to validate that every control in Annex A has a corresponding test that can be repeated by the external auditor. Which of the following deliverables BEST demonstrates the organization’s readiness and provides the most complete evidence set?  
A. The latest vulnerability-scan report showing all “critical” issues closed  
B. A matrix mapping each Annex-A control to a documented test procedure, frequency, owner, and last-pass/fail result  
C. A penetration-test report that gained domain-admin access but was subsequently remediated  
D. The prior year’s risk-register heat map with all reds reduced to yellow or green  

Correct Answer: B  
Explanation: ISO 27001 auditors look for repeatable, documented evidence that each control is operating effectively. Choice B supplies a single artifact (the test-to-control matrix) that links every control to an auditable test procedure, evidence of execution, and accountability. Vulnerability scans (A) and pen-test reports (C) cover only a subset of technical controls, while a risk heat map (D) shows risk posture, not control effectiveness.

Q2. A bank runs a red-team exercise against its new mobile-banking platform. The red team successfully performs an account-takeover attack by replying on an outdated 2FA API that the blue team thought had been decommissioned. Which part of the security-assessment program MOST clearly failed?  
A. Security-metrics selection  
B. Configuration-management and change-control verification  
C. Incident-response tabletop exercise  
D. Static code review coverage  

Correct Answer: B  
Explanation: The 2FA API was presumed decommissioned but was still live—indicating a gap in configuration management or change-control validation. Security metrics (A) might have shown the gap had they existed, but the root cause is operational visibility, not measurement. Incident response (C) is reactive, and static code review (D) would not surface an API that should already be offline.

Q3. An organization uses a balanced scorecard to track security performance. The KPI “% of critical findings older than 30 days” has remained below 5 % for two quarters, yet an internal audit finds that six critical findings were re-categorized as “moderate” without supporting evidence. Which security-assessment principle is MOST compromised?  
A. Independence  
B. Accuracy  
C. Objectivity  
D. Relevance  

Correct Answer: C  
Explanation: Objectivity requires that findings be rated without undue influence. Arbitrary re-categorization to keep the KPI green compromises objectivity. Independence (A) relates to organizational reporting lines, accuracy (B) to correct data, and relevance (D) to whether the metric matters—none of which are the primary issue here.

Q4. A SaaS provider’s SOC 2 Type II report is due for renewal. Management wants to reduce audit cost by leveraging continuous-monitoring tooling. Which approach BEST satisfies the “availability” trust-service criteria while lowering auditor workload?  
A. Provide the auditor with 12 months of automated uptime dashboards exported from the SaaS platform with tamper-evident hashes  
B. Offer the auditor the last quarter’s incident tickets tagged “availability”  
C. Schedule quarterly manual fail-over tests observed by the auditor  
D. Replace the SOC 2 with a self-assessment questionnaire signed by the CTO  

Correct Answer: A  
Explanation: Continuous monitoring with verifiable, tamper-evident data gives the auditor substantive evidence that controls operated throughout the period, directly supporting the availability criteria. Incident tickets (B) are reactive evidence, quarterly tests (C) are point-in-time, and a self-assessment (D) lacks independence and rigor.

Q5. During a control self-assessment workshop, the facilitator asks business-unit owners to rate fraud-detection controls as “adequate” or “inadequate.” Historically, 95 % are marked “adequate,” but external audit findings repeatedly cite fraud-control gaps. Which facilitation technique would BEST reduce this rating bias?  
A. Replace the binary rating with a 1–5 Likert scale  
B. Introduce anonymous, electronic voting with pre-work that includes actual fraud-incident data  
C. Invite the internal audit team to present last year’s findings at the start of the workshop  
D. Require every “adequate” vote to be accompanied by a compensating control narrative  

Correct Answer: B  
Explanation: Anonymous voting plus data-driven pre-work minimizes groupthink and social-desirability bias, producing more honest self-assessments. A Likert scale (A) still allows inflated scoring, merely with more granularity. While IA presentations (C) and control narratives (D) help, they do not eliminate the pressure to conform that anonymity addresses.

Q6. A company relies on a third-party cloud encryption service. The contract mandates an annual right-to-audit clause. Which testing method provides the STRONGEST assurance that encryption keys are properly segregated from customer data?  
A. Review the provider’s latest SOC 2 report for the “logical access” control  
B. Perform an on-site visit and observe key-management HSM configurations under NDA  
C. Request a penetration-test report performed by the provider’s internal team  
D. Ask the provider to fill out the Cloud Security Alliance CAIQ questionnaire  

Correct Answer: B  
Explanation: Direct observation (on-site inspection) of HSM segmentation provides first-hand evidence that cannot be fully corroborated by a third-party report (A), an internal pen-test (C), or a self-reported questionnaire (D). The right-to-audit clause makes this feasible.

Q7. A security team runs a purple-team exercise against its on-prem Active Directory. After the exercise, the red team produces a 200-page findings report, the blue team submits remediation metrics, and the sponsor declares “mission accomplished.” Six months later, a similar attack succeeds. Which continuous-improvement activity was MOST likely skipped?  
A. Regression testing of remediated controls  
B. Executive summary creation  
C. Attack-path visualization  
D. Threat-intel feed ingestion  

Correct Answer: A  
Explanation: Without regression testing, there is no assurance that fixes remained effective or were not undone by later changes. Executive summaries (B) and attack-path diagrams (C) are useful but do not validate fix durability. Threat intel (D) informs new attacks, but the issue here is failure of previously “fixed” controls.

Q8. An organization develops an internal web application using an agile DevOps pipeline. Security intends to embed automated testing so that every merge request fails the build if security tests do not pass. Which security-assurance activity BEST complements dynamic testing in the pipeline without creating excessive false positives?  
A. Run a full manual code review for each user story  
B. Trigger interactive application security testing (IAST) that correlates runtime data with code context  
C. Schedule a quarterly external penetration test  
D. Import OWASP Top 10 awareness slides into the sprint retrospective  

Correct Answer: B  
Explanation: IAST instruments the running code and correlates runtime findings with source context, producing higher-fidelity results than pure DAST and fewer false positives than SAST alone. Manual reviews (A) are too slow for per-merge gating, quarterly pen tests (C) are point-in-time, and awareness slides (D) do not provide automated assurance.

Q9. A hospital’s medical-device network is air-gapped except for a vendor-support laptop that is periodically connected for software updates. Which testing approach BEST validates that malware cannot traverse the gap via the laptop while still meeting clinical uptime requirements?  
A. Perform a red-team social-engineering test against the biomedical staff  
B. Conduct a static analysis of the device firmware binary  
C. Execute a controlled “dirty laptop” test in a sandbox environment that mirrors the production VLAN and monitor for lateral movement  
D. Interview the vendor about their secure-development lifecycle  

Correct Answer: C  
Explanation: A sandboxed “dirty laptop” test simulates the real update process and observes whether malware can bridge the air-gap, providing direct evidence without risking production uptime. Social engineering (A) tests people, not the bridging vector. Static firmware analysis (B) misses runtime propagation, and vendor interviews (D) are hearsay.

Q10. A CISO commissions a continuous control-monitoring dashboard that pulls logs from firewalls, IAM, and vulnerability scanners. After launch, the number of open “critical” findings spikes from 30 to 300, triggering board concern. An independent review finds that the new data sources use different severity taxonomies. Which security-assessment foundational step was missed?  
A. Control mapping  
B. Data normalization  
C. Threat-modeling update  
D. Key-risk-indicator baselining  

Correct Answer: B  
Explanation: Combining data without normalizing severity scales produces an apples-to-oranges aggregation that invalidates the metric. Control mapping (A) relates controls to frameworks, threat modeling (C) identifies new risks, and baselining (D) sets reference points, but none address the immediate comparability problem.
Q1. A global retailer’s CISO has mandated that every new mobile-point-of-sale (mPOS) application pass an independent security assessment before production release. The assessors are given only the compiled application package, a production-like device, and the public API documentation—no source code or design documents. Which type of assessment is being performed?  
A. White-box  
B. Gray-box  
C. Black-box  
D. Crystal-box  

Correct Answer: C  
Explanation: The testers have zero internal knowledge (no source, no design); they must discover vulnerabilities solely through external interaction. This is the definition of black-box testing. White-box (A) and crystal-box (D) both imply full source access, while gray-box (B) would supply partial internal detail.

Q2. A hospital’s internal audit department wants to verify that the newly deployed radiology picture-archiving system (PACS) enforces the same “need-to-know” access rules that are documented in the HIPAA security policy. Which control-testing approach will give the auditors the highest assurance that the policy is effective for every active user account?  
A. Interviewing the PACS administrator about how role-based access is configured  
B. Inspecting the vendor’s white paper on embedded RBAC functionality  
C. Selecting a random sample of user IDs and attempting to access restricted DICOM files  
D. Reviewing the quarterly vulnerability-scan report for missing patches  

Correct Answer: C  
Explanation: Only option C is a substantive test of operational effectiveness—auditors physically try to violate the policy and observe whether the system blocks them. Interviews (A) and vendor documents (B) are inquiry/inspection procedures that do not prove the control is working. Vulnerability scans (D) test patch state, not access control.

Q3. A SaaS provider runs a multi-tenant platform on AWS. Management wants a continuous-testing program that can detect when a new customer tenant is inadvertently granted excessive S3 bucket permissions. Which combination of tools and frequency best meets the “continuous” requirement while minimizing false positives?  
A. Weekly manual console audits using AWS Trusted Advisor  
B. Nightly EventBridge-triggered Lambda that queries AWS IAM Access Analyzer and posts anomalies to Slack  
C. Quarterly penetration-test engagement with a third party  
D. Annual certificate-based audit against ISO 27001  

Correct Answer: B  
Explanation: Automating IAM Access Analyzer via Lambda driven by EventBridge provides near-real-time detection of resource policies that grant public or cross-account access. It is continuous, programmatic, and far more frequent than weekly (A), quarterly (C), or annual (D) activities.

Q4. A financial regulator requires the bank’s red-team reports to be accurate, complete, and reproducible by another qualified team. Which attribute of the report is PRIMARILY being emphasized?  
A. Verifiability  
B. Objectivity  
C. Timeliness  
D. Clarity  

Correct Answer: A  
Explanation: Verifiability means a different competent team could replicate the findings using the same methodology and data. Objectivity (B) is related but focuses on bias-free presentation. Timeliness (C) and clarity (D) are desirable but do not address reproducibility.

Q5. A company’s bug-bounty program has paid multiple researchers for the same SQL-injection flaw in a legacy PHP application. The security team discovers the root cause is a single shared library used by three different customer-facing sites. Which security-testing key-performance indicator (KPI) is MOST directly affected by this situation?  
A. Mean time to detect (MTTD)  
B. Defect duplication rate  
C. False-positive ratio  
D. Patch latency  

Correct Answer: B  
Explanation: Duplicate submissions of the same underlying flaw inflate bounty costs and skew metrics. Defect duplication rate (B) measures how often the same vulnerability is reported multiple times. MTTD (A) gauges detection speed, false positives (C) measure incorrect findings, and patch latency (D) measures fix speed—none capture the “same bug, many reports” problem.

Q6. A critical Windows domain controller is scheduled for its monthly patch cycle. The security team runs an unauthenticated Nessus scan before maintenance windows and again after reboot. The second scan shows the same “Critical” plugin ID that was present before patching. Which conclusion is MOST defensible?  
A. The plugin is a false positive because Microsoft patches cannot be rolled back.  
B. The plugin may be a false positive if the scanner was not supplied domain credentials to verify the patch level accurately.  
C. The plugin definitively proves the patch failed to install.  
D. The plugin indicates a zero-day vulnerability for which no patch exists.  

Correct Answer: B  
Explanation: Unauthenticated scans check banner information that can be misleading if the service did not update its version string or if the scanner lacks privileges to confirm the actual file versions. Without credentials, the scanner cannot reliably determine whether the patch is installed, making a false positive the most defensible explanation.

Q7. A DevOps team embeds a static-application-security-testing (SAST) gate in the CI pipeline. Over the first sprint, 42 high-severity findings are flagged, but after manual review 40 are ruled “not exploitable.” Senior management fears the tool is worthless. Which FIRST step best aligns with NIST SP 800-53 SA-11 recommendation for static-tool deployment?  
A. Disable the SAST gate and return to manual code review  
B. Tune the tool’s rules to the organization’s custom frameworks and re-baseline  
C. Purchase a competing SAST product  
D. Lower the severity threshold to “Critical” only  

Correct Answer: B  
Explanation: NIST SA-11 stresses that static tools must be configured for the target environment to reduce noise. Tuning rules to recognize internal libraries, safe wrappers, and custom frameworks will shrink the false-positive pile and retain true positives. Dumping the tool (A, C) or hiding issues (D) does not improve security.

Q8. A nuclear facility’s safety engineer must validate that the reactor-control network remains isolated from the corporate LAN. Which testing method provides the STRONGEST evidence that the isolation is effective against both malicious and accidental bridging?  
A. Reviewing the layer-3 switch configuration printouts  
B. Observing a network technician draw the network diagram in Visio  
C. Performing packet injection on the corporate VLAN and confirming packets never appear on the control VLAN  
D. Interviewing the network architect about firewall rule design  

Correct Answer: C  
Explanation: Active testing (packet injection) empirically proves that no forwarding path exists. Configuration reviews (A) and interviews (D) are useful but cannot guarantee the running state matches the intended design. Diagram observation (B) is purely documentary.

Q9. A cloud-native company tags every workload with a “data-classification” label (Public, Internal, Confidential, Restricted). The CISO wants to validate that the runtime encryption controls ( KMS keys, TLS versions, S3 encryption flags) match the label. Which technique BEST scales to thousands of ephemeral containers?  
A. Configuration-management-database (CMDB) comparison once per quarter  
B. Agentless CSPM (Cloud Security Posture Management) API polling that triggers on label change events  
C. Weekly manual console spot-checks  
D. Social-engineering calls to developers asking which keys they use  

Correct Answer: B  
Explanation: CSPM tools consume cloud APIs to retrieve resource configurations in real time and can be event-driven, giving immediate feedback when a container with “Restricted” data lacks the required encryption settings. CMDB (A) lags behind ephemeral assets, manual checks (C) do not scale, and social engineering (D) is irrelevant.

Q10. A payment-card processor’s QSA must verify PCI DSS Req. 11.3.4 (segmentation validation). The processor uses micro-segmentation enforced by host-based firewalls inside a VMware NSX environment. Which test approach provides the QSA with the MOST persuasive evidence that segmentation controls are operating effectively across the entire in-scope population?  
A. Examining the NSX manager policy export from one randomly chosen day  
B. Running Nmap from an out-of-scope jump host against a 5 % sample of in-scope VMs  
C. Reviewing vendor white papers that claim micro-segmentation works  
D. Using an automated policy-validation platform that queries every ESXi vswitch and host firewall rule daily and maps attempted flows  

Correct Answer: D  
Explanation: Automated, population-wide validation of every vswitch and host rule against actual flow attempts proves that no unauthorized path exists. Sampling (B) or one-time exports (A) can miss misconfigurations, while white papers (C) are marketing artifacts, not evidence of operational effectiveness.
Q1. A global retailer is preparing for its annual ISO 27001 surveillance audit. The CISO wants to validate that every control listed in the Statement of Applicability (SoA) is both “implemented” and “effective” before the external auditors arrive. Which of the following internal test activities provides the STRONGEST evidence that a control is effective?  
A. Policy review and interview with the control owner  
B. Walk-through of the procedure with sample artifacts  
C. Re-performance of the control by an independent tester  
D. Vulnerability-scan report showing no critical findings  

Correct Answer: C  
Explanation: Re-performance (also called “re-performance testing”) is the highest-grade evidence because the evaluator independently executes the same steps the control owner performs and measures the actual outcome. Policy review (A) and walk-throughs (B) are persuasive but not conclusive; they rely on documentation and narration rather than observable results. A clean scan (D) only proves a momentary technical state, not the ongoing effectiveness of the managerial or operational control described in the SoA.

Q2. A hospital’s medical-device network is air-gapped from the corporate LAN. The security team runs quarterly Nessus scans against the corporate network but has never scanned the medical segment. During a recent incident response, malware is discovered on a patient monitor. Executive leadership now wants an “authoritative snapshot” of exposure on the medical network without risking service disruption to life-critical devices. Which approach BEST satisfies both objectives?  
A. Credentialed active scanning during scheduled maintenance windows  
B. Passive network monitoring with asset-discovery and version-profiling sensors  
C. Full-knowledge penetration test with exploit attempts on representative devices  
D. Requesting device vendors to supply internal security-test reports  

Correct Answer: B  
Explanation: Passive sensors read network traffic without generating probe packets that could reboot or brick sensitive devices. This yields an authoritative inventory and version map (exposure snapshot) with near-zero risk of disruption. Credentialed active scans (A) still send packets that some legacy medical stacks cannot tolerate; pentesting (C) is far too invasive; vendor reports (D) are useful but give a point-in-time view for only the models tested and are not an “authoritative snapshot” of the hospital’s own deployment.

Q3. A SaaS provider that stores EU customer data in AWS Ireland has just adopted the CIS AWS Foundations Benchmark. Management wants a dashboard that turns the 41-page benchmark into measurable KPI traffic-lights (red/amber/green). Which AWS service supplies the most turnkey mapping of configuration items to the CIS controls while allowing custom exemptions with auditor commentary?  
A. AWS Config with conformance packs  
B. CloudTrail Insights  
C. GuardDuty findings  
D. Trusted Advisor  

Correct Answer: A  
Explanation: AWS Config conformance packs contain pre-written rules that map 1-to-1 to CIS Benchmark items. Config allows “override” annotations where an auditor can exempt a finding and attach justification, turning the result into a KPI metric. CloudTrail (B) is API logging, not configuration compliance scoring. GuardDuty (C) is threat detection, not baseline hardening. Trusted Advisor (D) has some overlap but is not benchmark-specific and lacks granular exemption workflow.

Q4. A Fortune 500 company runs an agile DevOps pipeline with 300 micro-service deployments per day. The security team wants each build to produce evidence that can later be presented to auditors to prove “security controls were validated in the release process.” Which pipeline feature BEST supplies this evidentiary requirement?  
A. Dynamic application security testing (DAST) HTML report archived in the artifact repository  
B. Cryptographically signed SBOM (software bill of materials) generated at build time  
C. Container-runtime firewall logs forwarded to the SIEM  
D. Post-deployment penetration-test report signed by the red-team lead  

Correct Answer: B  
Explanation: A cryptographically signed SBOM, generated automatically in the pipeline, is tamper-evident and demonstrates that the company knows exactly what code and libraries were shipped—an essential control for supply-chain security. Auditors can later compare the SBOM to vulnerability databases to verify ongoing control effectiveness. DAST (A) is useful but only covers one layer (running app). Runtime firewall logs (C) are operational, not build-time evidence. A post-deployment pentest (D) is manual, point-in-time, and cannot scale to 300 daily releases.

Q5. A regional bank is required by regulators to perform an “independent security review” of its new mobile-banking app before go-live. The development budget is tight, and the same small security team that wrote large portions of the app’s authentication module is available to test. Which course of action BEST preserves independence without blowing the budget?  
A. Have the security team test the app, then ask internal audit to review the test documentation  
B. Engage an external certified firm to perform a black-box assessment but limit scope to OWASP Mobile Top 10  
C. Rotate developers from unrelated LOBs to perform peer review, then document results  
D. Use the security team but require two senior managers from different divisions to sign off on the report  

Correct Answer: B  
Explanation: Regulatory language for “independent” customarily means organizational independence from the team that built the system, which an external certified firm satisfies. Limiting scope to the Top 10 keeps cost contained while still meeting the letter and spirit of the requirement. Option A leaves the actual testing in the hands of the interested party; internal audit review is better than nothing but is not technically independent testing. Peer review (C) and dual sign-off (D) are good practices but do not constitute an independent security assessment in the regulatory sense.

Q6. A critical ICS (industrial-control) network employs a data diode to ensure one-way flow from the plant to the corporate historian. During a control-framework gap analysis, the auditor claims the diode itself must be penetration-tested annually. The plant manager refuses, arguing any “test packets” could cause physical damage to the $50 M furnace. Which reference BEST supports the manager’s position of NOT testing the diode in situ?  
A. NIST SP 800-53 control CA-8 (Penetration Testing)  
B. ISA/IEC 62443-3-3 SR 3.3 (Unidirectional Gateways)  
C. NIST SP 800-82 (Guide to ICS Security)  
D. ISO 27001:2022 A.8.8 (Information Deletion)  

Correct Answer: C  
Explanation: NIST SP 800-82 specifically cautions that active security testing of live ICS can induce safety incidents and recommends that security assessments of unidirectional devices be performed offline or via vendor-supplied certification evidence. While CA-8 (A) mandates penetration testing, 800-82 provides the contextual exception for safety-critical systems. ISA 62443 (B) describes unidirectional gateways but does not exempt them from testing. ISO 27001 A.8.8 (D) is irrelevant to the issue.

Q7. A cloud-native company wants to adopt continuous compliance monitoring for PCI DSS 4.0. The QSA recommends they map each PCI requirement to one or more automated test scripts that run at least daily. Which additional step is MOST important to ensure the scripts themselves are reliable?  
A. Version-control the test scripts and require peer review before merge  
B. Run the scripts only in production to ensure they see real data  
C. Store script outputs in an object-storage bucket with “write-only” ACL  
D. Encrypt the scripts with AES-256 at rest  

Correct Answer: A  
Explanation: Version control with peer review is the cornerstone of script integrity; otherwise logic errors or malicious changes could silently invalidate compliance evidence. Running tests only in production (B) is risky and may violate PCI segregation of duties. Write-only ACL (C) and encryption (D) protect confidentiality and immutability but do not address correctness or trustworthiness of the script logic.

Q8. An e-commerce site has experienced three successive breaches traced to insecure code libraries. Executive leadership mandates that every build pipeline include a “quality gate” that fails if any component has a CVSS score ≥ 7. After one month, the gate is disabled because it blocks 90 % of releases. Which metric should the security team FIRST analyze to right-size the gate without abandoning the control?  
A. Mean time to remediate (MTTR) for high-severity findings  
B. Percentage of flagged libraries actually exploitable in the app’s context  
C. Number of new commits per day  
D. Ratio of true-positive incidents to false-positive alerts  

Correct Answer: B  
Explanation: A large number of high-CVSS findings are often not exploitable in a given deployment context (e.g., library loaded but vulnerable function never called). Analyzing exploitability (reachable code path) allows the team to tune the gate to block only real risk, restoring developer productivity while maintaining security. MTTR (A) is important later but doesn’t explain why the gate is over-blocking. Commits/day (C) is a velocity metric unrelated to risk filtering. TP/FP ratio (D) is SIEM-centric and not directly applicable to library vulnerabilities.

Q9. A multinational corporation is adopting zero-trust architecture. The security team must choose a testing methodology that validates “never trust, always verify” enforcement across 40,000 endpoints in 60 countries. Which combination of test approaches gives the MOST comprehensive evidence with the least operational disruption?  
A. Red-team full-scope compromise simulation plus quarterly compliance checklist  
B. Purple-team collaborative exercises augmented by continuous control-validation sensors  
C. Blue-team tabletop scenarios followed by external certification audit  
D. Annual black-box penetration test and monthly phishing simulations  

Correct Answer: B  
Explanation: Purple-team exercises combine attack creativity (red) with defensive visibility (blue) while the continuous sensors (e.g., AttackIQ, Verodin) safely automate exploit techniques to verify that each zero-trust control (micro-segmentation, conditional access, MFA, etc.) fires as expected—producing evidence at scale without outages. Full red-team (A) is valuable but too sporadic. Tabletop (C) is discussion-only. Annual pentest (D) is point-in-time and cannot keep pace with zero-trust drift.

Q10. A government agency’s security policy states that “cryptographic modules shall be validated to FIPS 140-2 level 2 or higher.” An internal assessment finds that the new cloud-based password manager vendor claims “FIPS-compliant encryption” but the vendor’s certificate shows a level 1 validation for the underlying module. Additionally, the module runs in a shared multitenant environment without physical tamper-evidence. Which type of finding is MOST appropriate for the assessor to record?  
A. A deficiency in an administrative control  
B. A deficiency in a technical control  
C. A deficiency in a physical control  
D. A false-positive; level 1 is sufficient for password managers  

Correct Answer: B  
Explanation: The policy mandates level 2, which adds physical tamper-evidence and role-based authentication; level 1 provides only the cryptographic algorithm validation. Because the module is used to protect stored passwords, the failure to meet the higher level is a shortfall in a technical (cryptographic) control, not administrative or purely physical. It is not a false-positive (D) because the explicit requirement is level 2.
Q1. A global retailer is preparing for its annual PCI-DSS assessment. The QSA has requested evidence that the internal vulnerability-scanning program is “sufficiently independent” of the infrastructure team. Currently, scans are launched from an engineer’s laptop that is domain-joined to the same Active Directory forest that runs the card-holder data environment (CDE).  
A. Provide the QSA with the engineer’s job description showing a dotted-line reporting relationship to Security.  
B. Move the scanning laptop into a separate OU and apply a GPO that removes local-admin rights from the engineer.  
C. Purchase a managed scanning service operated by a different company and have that vendor attest independence.  
D. Configure the existing laptop to use a local account that is not joined to the domain and document the separation in the procedure guide.  

Correct Answer: C  
Explanation: PCI-DSS requires that “personnel who conduct the internal vulnerability scans have organizational independence.” A dotted-line report (A) or GPO restrictions (B) do not remove the conflict of interest inherent in the same AD forest. Using a local account (D) still leaves control of the scanning platform inside the same team. Retaining an external managed service (C) provides true third-party independence that satisfies both DSS v4.0 requirement 11.3.1 and the QSA’s expectation.

Q2. A medical-device manufacturer embeds a hard-coded AES-128 key in every insulin pump to secure firmware updates. During a pre-market security assessment, the tester successfully extracts the key from a single device and uses it to sign malicious firmware. Which type of test finding should be reported first?  
A. Weakness in the random-number generator used for key generation.  
B. Inadequate protection of a cryptographic secret (key exposure).  
C. Improper certificate-validation logic during update installation.  
D. Buffer-overflow vulnerability in the update installer.  

Correct Answer: B  
Explanation: The root issue is that a single compromised device reveals a global secret (the hard-coded key). This is a classic “inadequate protection of cryptographic material” finding (B). The key was not generated on the device (A is irrelevant), and no mention is made of certificates (C) or memory corruption (D).

Q3. A penetration-testing firm delivers a red-team report that contains five critical findings. The CISO wants to validate that the fixes actually block the attack paths before the report is accepted. Which security-testing concept is MOST appropriate to apply next?  
A. Regression testing  
B. Re-testing (verifying fixes)  
C. Post-implementation review  
D. User-acceptance testing  

Correct Answer: B  
Explanation: The question describes the need to confirm that remediation measures neutralize the identified vulnerabilities. This is precisely “re-testing” (B), sometimes called “fix validation.” Regression testing (A) would ensure new code did not break existing functionality, while a post-implementation review (C) is broader and not attack-focused. User-acceptance testing (D) is concerned with business requirements, not security controls.

Q4. An organization uses a risk-based approach to determine how often critical servers are scanned for vulnerabilities. Last quarter the vulnerability-management team discovered that a critical Apache Struts flaw was patched on only 30 % of servers within the SLA window. Management has now mandated more frequent scanning. Which metric BEST justifies the additional resources being requested?  
A. Mean time to remediate (MTTR)  
B. Percentage of high-risk findings open longer than SLA  
C. Number of assets scanned per week  
D. CVSS average score of vulnerabilities discovered  

Correct Answer: B  
Explanation: The failure to meet the patching SLA is directly captured by the percentage of high-risk findings open longer than SLA (B). MTTR (A) is a time-based average but does not show compliance with policy. Scanning more assets (C) or the average CVSS (D) does not measure remediation performance.

Q5. A bank runs a bug-bounty program that pays up to $30 000 for remote-code-execution flaws in its mobile-banking app. A researcher demonstrates a crash triggered by a malformed JWT but cannot achieve code execution. The bank declines the submission. Two months later, an internal security tool identifies the same crash during fuzz testing and the bank silently patches it. Which guideline of responsible disclosure has the bank MOST likely violated?  
A. Failure to provide public credit to the researcher  
B. Failure to coordinate disclosure timing with the researcher  
C. Failure to award a monetary bounty for a denial-of-service issue  
D. Failure to include the finding in the annual loss-estimate report  

Correct Answer: B  
Explanation: Responsible-disclosure frameworks (e.g., ISO 29147) require coordinated disclosure—both parties agree on publication timing. By silently patching and not communicating, the bank undercuts the researcher’s ability to publish or receive credit, violating coordination (B). The program scope limited payouts to RCE, so declining a bounty (C) is within policy. Credit (A) is secondary to coordination, and the loss-estimate report (D) is unrelated to disclosure ethics.

Q6. A cloud SaaS vendor provides a SOC-2 Type II report to prospective customers. The report covers the period 01 Oct 2023 – 30 Sep 2024 and was issued on 15 Dec 2024. A prospective enterprise customer’s CISO wants assurance that encryption key management is still effective as of 01 Mar 2025. Which approach provides the STRONGEST evidence?  
A. Request the vendor’s most recent penetration-testing report dated 20 Jan 2025.  
B. Demand a fresh SOC-2 Type I report covering key-management controls.  
C. Obtain the vendor’s 2025 ISO-27001 certificate.  
D. Rely on the SOC-2 Type II report because the auditor opinion is still “unqualified.”  

Correct Answer: A  
Explanation: The SOC-2 Type II report is historical (ended 30 Sep 2024) and gives no visibility into control effectiveness after that date. A penetration test conducted after the report period (A) provides up-to-date evidence that key-management controls are still functioning. A Type I report (B) would only give point-in-time design evidence, while ISO-27001 certification (C) is annual and not necessarily focused on key management. Relying on the old SOC-2 (D) ignores the four-month gap.

Q7. During a control self-assessment workshop, the identity-team rates the AD password policy as “adequate” because it enforces 14-character minimum and complexity. The audit team challenges the rating, citing that the policy still allows passwords to be changed only every 24 hours and lacks breached-password screening. Which control assessment principle has the identity team overlooked?  
A. Control accuracy  
B. Control completeness  
C. Control existence  
D. Control effectiveness  

Correct Answer: D  
Explanation: The team documented that the control exists (C) and is configured (accuracy, A), but they did not evaluate whether it actually mitigates modern password attacks (effectiveness, D). The absence of breached-password screening and the 24-hour window reduce real-world protection, demonstrating ineffectiveness.

Q8. A government agency is required to conduct red-team exercises against its citizen-services portal every two years. After the 2023 exercise, the agency migrated 60 % of workloads to containers on Kubernetes. The 2025 exercise scope statement copies the 2023 scope verbatim and does not mention containers. Which risk is MOST likely to be missed?  
A. Misconfiguration of container runtime security controls  
B. Cross-site scripting in the citizen-facing web forms  
C. Weak TLS cipher suites on the external load balancer  
D. SQL injection in the legacy mainframe tax database  

Correct Answer: A  
Explanation: The unchanged scope ignores the new technology stack (containers), so tests will omit runtime-security issues such as privileged pods, network policies, or image vulnerabilities (A). Legacy issues (B, C, D) were already in scope in 2023 and would continue to be tested.

Q9. A company performs daily automated configuration-compliance scans of its AWS accounts using the CIS AWS Foundations Benchmark. The security team receives alerts for any rule marked “FAIL.” Over a 30-day period, the number of daily FAIL alerts drops from 120 to 5, yet an internal audit discovers that S3 bucket policies still allow unauthorized Amazon-authenticated users to read sensitive data. Which measurement gap BEST explains the false sense of improvement?  
A. The benchmark does not include tests for S3 bucket ACLs.  
B. The scanner lacks credentials to inspect S3 access-control lists.  
C. The benchmark rules were written for the old AWS standard partition.  
D. The alert threshold was tuned to suppress low-severity findings.  

Correct Answer: A  
Explanation: The CIS AWS Foundations Benchmark v1.5 contains only a handful of S3-related controls (e.g., block-public-access setting) but does not evaluate every bucket policy or ACL for “authenticated-users” grants. Therefore, the metric improved (fewer FAILs) while real risk remained (A). If the scanner lacked creds (B), the findings would have been “ERROR,” not “PASS.” Partition issues (C) or threshold tuning (D) would not selectively hide authenticated-user grants.

Q10. A manufacturer’s secure-development policy mandates that threat modeling must be performed during the design phase and then “re-evaluated when significant changes occur.” A development team adds a new REST endpoint that accepts file uploads and pushes the code to production via a standard CI/CD pipeline. A subsequent security review labels the change “minor” and skips threat modeling. Three months later, the endpoint is found to be vulnerable to deserialization attacks. Which assessment activity would have BEST detected the policy deviation?  
A. Secure-code review of the pull request  
B. Static analysis scan gated in the CI pipeline  
C. Process audit of the change-management records  
D. Dynamic scanning of the production endpoint  

Correct Answer: C  
Explanation: The failure is procedural—threat modeling was required but skipped. A process audit (C) comparing change tickets to policy would reveal that the “minor” classification was inappropriate. Code review (A) or static analysis (B) might find the vulnerability but would not confirm whether threat modeling occurred. Dynamic scanning (D) is too late and may not pinpoint deserialization without tailored payloads.
Q1. A global retailer is preparing for its first-time ISO 27001 certification. The CISO wants to pre-validate that the Statement of Applicability (SoA) accurately reflects every control that is both applicable and excluded. Which type of assessment activity BEST satisfies this objective?  
A. A vulnerability scan of the DMZ to confirm patching levels  
B. A supplier security questionnaire sent to all third-party vendors  
C. A comprehensive control design assessment (gap analysis) against Annex A  
D. A red-team exercise that attempts to exfiltrate customer credit-card data  

Correct Answer: C  
Explanation: ISO 27001 requires that the SoA list every Annex A control and justify inclusion or exclusion. A control design assessment (gap analysis) systematically compares each control’s intended design with the standard, revealing missing or incorrectly scoped controls before the certification audit. Vulnerability scans (A) and red-team tests (D) evaluate technical effectiveness, not design coverage, while supplier questionnaires (B) address third-party risk, not the retailer's own SoA.

Q2. A hospital’s internal audit department wants to verify that medical devices running embedded Windows still receive timely security patches even though they are “black boxes” to the IT staff. Which testing approach will provide the MOST reliable evidence without violating vendor warranty?  
A. Credentialed network vulnerability scan while devices are in standby mode  
B. Review of manufacturer SBOMs and patch-release notes plus spot checks of device firmware versions  
C. Full-knowledge penetration test that installs a local agent on each device  
D. Social-engineering test against biomedical technicians to see if they will share device passwords  

Correct Answer: B  
Explanation: Because the devices are black boxes and under vendor warranty, intrusive testing (A or C) could void support or disrupt clinical operations. The safest, most reliable evidence comes from comparing the manufacturer’s software bill of materials (SBOM) and published patches against actual firmware versions observed on randomly sampled devices—an accepted non-invasive audit technique.

Q3. A SaaS provider that stores EU customer data in AWS Ireland has implemented a data-retention policy requiring deletion of backups within 30 days of contract termination. During a SOC 2 Type II engagement, the auditor needs to test operational effectiveness of this policy. Which test procedure BEST validates the commitment?  
A. Inspect AWS KMS key-rotation logs for the past 12 months  
B. Select a sample of customer terminations and examine backup-deletion tickets and AWS S3 lifecycle-rule execution logs  
C. Re-run the application’s unit-test suite in the staging environment  
D. Review the annual risk-register entry for “data over-retention”  

Correct Answer: B  
Explanation: SOC 2 Type II requires evidence that controls operate effectively throughout the period. Selecting terminated customers and tracing their backup-deletion evidence (tickets plus automated S3 lifecycle logs) directly tests whether the 30-day retention control is working. KMS rotation (A) concerns key management, not deletion timing; unit tests (C) are developmental; and a risk-register review (D) is design-only.

Q4. A financial regulator requires banks to perform “continuous control monitoring.” The bank’s security team proposes replacing its quarterly manual access-review spreadsheets with an IAM dashboard that reconciles user privileges to HR termination feeds every four hours. Before approving, the internal auditor wants assurance that the new dashboard itself is reliable. Which assurance activity is MOST appropriate?  
A. Benchmark the dashboard against NIST SP 800-53 rev 5 control AC-2  
B. Perform a parallel-run (dual-review) for two cycles and measure reconciliation accuracy  
C. Contract an external red-team to exploit dashboard APIs  
D. Validate that the dashboard vendor is ISO 27001 certified  

Correct Answer: B  
Explanation: Continuous monitoring tools must first be proven accurate. A parallel-run compares the new automated reconciliation with the existing trusted manual process for the same population, quantifying false positives/negatives before full adoption. Benchmarking (A) or vendor certification (D) addresses design or supply-chain risk, not operational accuracy. Red-teaming APIs (C) evaluates security of the tool, not its data integrity.

Q5. A company runs a bug-bounty program that has received over 500 valid submissions in the last year. The CISO wants to integrate vulnerability data into the annual risk assessment. Which step is MOST critical to ensure the data is suitable for risk-scoring?  
A. Map each bug to the affected asset in the CMDB and re-calculate likelihood based on exploitability  
B. Publish the top-ten researchers on the corporate web site to encourage participation  
C. Cross-reference each bounty submission with internal penetration-test findings and discard duplicates  
D. Request that researchers provide a CVSS v4 environmental score  

Correct Answer: A  
Explanation: Risk assessment requires asset-centric, likelihood, and impact data. Mapping bounties to configuration items in the CMDB and adjusting likelihood with real-world exploitability converts raw bug data into risk input. Publicizing researchers (B) is marketing; de-duplication (C) is good hygiene but insufficient for risk scoring; and researchers cannot realistically provide environmental scores (D) without inside knowledge.

Q6. An organization uses a DevSecOps pipeline with mandatory static application security testing (SAST) gating any merge to the main branch. The security team discovers that high-severity SAST alerts are being disabled en masse by developers who mark them “Won’t Fix.” Senior management wants an independent check. Which test provides the BEST evidence that production code remains secure despite disabled alerts?  
A. Dynamic application security testing (DAST) performed on the nightly build  
B. A manual secure-code review of a statistically significant sample of merged commits  
C. A dependency-check scan for known CVEs in open-source libraries  
D. Stress-testing the pipeline by submitting malicious merge requests  

Correct Answer: B  
Explanation: Disabled SAST alerts may hide systemic code-level flaws. A manual secure-code review by an independent party (e.g., internal security team) can identify true positives that were improperly dismissed, providing direct evidence of code security. DAST (A) finds runtime issues but misses many code-level flaws; dependency scans (C) address third-party rather than first-party code; stress-testing the pipeline (D) evaluates process security, not code security.

Q7. A cloud-native company wants to validate that its AWS VPC flow logs are actually being sent to the SIEM and triggering alerts when suspicious port-scan activity occurs. Which test is MOST efficient while minimizing production impact?  
A. Run a scripted port-scan from a bastion host against a test EC2 instance and observe SIEM alerts  
B. Inspect Terraform templates to ensure VPC flow-log blocks are present  
C. Execute a table-top exercise with the SOC team  
D. Enable AWS GuardDuty and compare findings with SIEM dashboards  

Correct Answer: A  
Explanation: An end-to-end test (generate event → log → SIEM alert) provides operational assurance. A controlled scan from a known bastion host against a non-critical test instance produces real flow logs and verifies alert firing without harming production workloads. Terraform inspection (B) is design-only; table-top exercises (C) are discussion-based; GuardDuty (D) uses threat-intel, not flow-log ingestion, so it does not test the company’s custom SIEM alerting logic.

Q8. A multinational manufacturer must comply with both ISO 27001 and NIST SP 800-171 for defense contracts. The internal audit team has limited resources and needs to rationalize testing efforts. Which approach BEST reduces duplication while still satisfying both frameworks?  
A. Map ISO 27001 Annex A controls to 800-171 CUI requirements and perform a single integrated audit with a combined control matrix  
B. Conduct ISO 27001 first, then create a separate 800-171 checklist and re-audit the same systems  
C. Outsource ISO 27001 to a certification body and self-assess only 800-171  
D. Align to ISO 27017 (cloud security) instead of 800-171 to simplify scope  

Correct Answer: A  
Explanation: There is substantial overlap between Annex A and 800-171. Creating a combined control matrix allows one set of test procedures to generate evidence acceptable for both standards, conserving resources while still meeting each framework’s unique requirements. Separate audits (B) double the workload; outsourcing (C) is cost-effective but does not reduce test duplication; and ISO 27017 (D) is cloud-specific and not a substitute for 800-171 CUI protections.

Q9. A retail chain performs quarterly PCI DSS wireless scans at all 800 stores. The QSA discovers that two new pop-up stores were opened for the holiday season but were not scanned. Which control failure MOST contributed to this gap?  
A. Lack of an updated asset inventory that triggers inclusion in the scan schedule  
B. Use of WPA3 encryption instead of WPA2  
C. Absence of an intrusion-detection system on the pop-up store network  
D. Failure to rotate default SNMP community strings  

Correct Answer: A  
Explanation: PCI DSS req. 11.1 mandates a quarterly wireless scan of all in-scope facilities. An accurate, up-to-date asset inventory (including new pop-up stores) is the trigger that ensures these sites are added to the scan schedule. Without it, the stores were simply overlooked. Encryption choice (B), IDS (C), or SNMP strings (D) are unrelated to scan coverage.

Q10. A government agency’s red-team exercise successfully obtained domain-admin rights by combining a phishing email with a zerologon vulnerability. The CISO asks for a metric to track remediation progress across the enterprise. Which metric BEST indicates that the agency is reducing the risk of the same attack path?  
A. Percentage of privileged accounts that have disabled phishing awareness training modules  
B. Mean time to detect (MTTD) for phishing emails  
C. Percentage of domain controllers that have passed an authenticated scan for the zerologon patch  
D. Number of red-team findings rated “critical”  

Correct Answer: C  
Explanation: The attack path combined phishing (initial access) with zerologon (privilege escalation). Patching domain controllers against CVE-2020-1474 directly breaks the escalation phase. Tracking the patch coverage via authenticated scans provides a clear, objective metric that the vulnerability is being eliminated. MTTD (B) measures detection speed but not remediation; disabled training modules (A) are irrelevant; and a raw count of findings (D) does not specify whether the particular attack path is fixed.
Q1. A global retailer is about to begin its first fully-remote PCI-DSS assessment because auditors are not allowed on-site due to a pandemic travel ban. The QSA firm proposes using video-conference walk-throughs, screen-share configuration reviews, and a couriered “evidence-collection laptop” that will be shipped back encrypted. Which of the following findings should concern the retailer’s CISO the MOST before the assessment begins?  
A. The QSA will rely on screenshots provided by internal IT staff instead of direct console access.  
B. The couriered laptop uses a consumer-grade cloud backup service that is not in the retailer’s approved vendor list.  
C. The video-conference sessions will be recorded and stored on the QSA’s European servers, potentially violating the retailer’s data-residency policy.  
D. The QSA contract does not require the firm to maintain an attestation that all original video evidence was destroyed after the report is issued.  

Correct Answer: A  
Explanation: Screenshot evidence that is collected and curated by the staff being audited breaks the basic audit principle of independence and reliable evidence (PCI DSS Req. 11.3.4 and ISA 500). Options B, C, and D introduce secondary risk (vendor management, privacy, retention), but the inability to obtain objective, first-hand evidence directly under the QSA’s control is the most fundamental threat to the validity of the assessment.

Q2. During a continuous-monitoring program, the security team feeds every Nessus scan result into a SIEM and opens a Sev-1 incident for every CVSS 9+ vulnerability within one hour of detection. After six months the mean-time-to-remediate (MTTR) has actually increased. Which control-gap BEST explains this counter-intuitive result?  
A. Lack of a threat-model-based prioritization that considers exploitability and asset value.  
B. Absence of a formal change-management process for emergency patches.  
C. Insufficient vulnerability-scan frequency (only weekly).  
D. Missing service-level agreement (SLA) with the patching team.  

Correct Answer: A  
Explanation: Treating every CVSS 9+ finding as Sev-1 creates alert fatigue; analysts waste cycles on vulnerabilities that may be unreachable or have no public exploit. A risk-based scoring approach (e.g., combining CVSS, asset criticality, threat intel) would shrink the true “critical” list and accelerate real fixes. Option B and D are operational issues, but the root cause is poor prioritization logic.

Q3. A SaaS provider’s customer demands a right-to-penetrate clause in the new contract. The provider’s data-center is hosted in AWS, and the customer wants to run unrestricted “Red Team” exercises including brute-force, DDoS, and social-engineering against production. Which of the following is the PRIMARY control the provider should insist upon BEFORE authorizing the test?  
A. A signed “rules of engagement” document that includes emergency contacts, escalation paths, and a “get-out-of-jail-free” letter.  
B. Proof that the customer maintains a standalone cyber-insurance policy with a minimum limit of USD 5 million.  
B. (duplicate) A requirement that the customer use only (ISC)²-certified testers.  
D. A clause that any findings must be reported within 24 hours under NDA.  

Correct Answer: A  
Explanation: A formal rules-of-engagement (RoE) document is the primary safeguard to prevent collateral damage, define scope, and provide legal authorization (sometimes called “get-out-of-jail-free”). Insurance (B) is secondary, certification (C) is not required by CISSP best practice, and timely reporting (D) is good but does not mitigate operational/legal risk during the test.

Q4. A company is adopting NIST SP 800-53A for assessment of its federal contract. The assessor states she will use “OA-2 (2) – Interview, Examination, Testing” for every control. The CISO is worried about workload. Which statement BEST reflects the flexibility allowed by 800-53A?  
A. The assessor must apply all three methods to every control; no deviation is permitted.  
B. The organization may substitute “Interview” with “Testing” if it reduces cost, as long as one method is used.  
C. The selection of methods and objects is risk-based and can be tailored, but must produce sufficient evidence to support a conclusion.  
D. Only controls categorized “High” require all three methods; “Moderate” and “Low” can rely on attestation.  

Correct Answer: C  
Explanation: SP 800-53A is purposefully flexible; the depth and type of assessment procedure are scaled to the impact level, risk, and prior assessment results. Sufficient, appropriate evidence is the goal, not a mechanical checklist of methods.

Q5. A bank runs an internal phishing simulation. The baseline click-rate is 18 %. After deploying a new security-awareness computer-based training (CBT) module, the click-rate drops to 14 %. Senior management refuses to fund further awareness activities, claiming “success.” Which metric should the security team cite to demonstrate the program has NOT yet achieved its risk-tolerance target?  
A. Percentage of users who reported the phish (reporting rate) stayed flat at 5 %.  
B. Repeat clickers (users who clicked in both the baseline and post-training tests) represent 60 % of the clicks.  
C. The margin of error is ±3 %, so the 4 % drop is not statistically significant.  
D. The industry benchmark for banks is 8 % click-rate.  

Correct Answer: B  
Explanation: A high proportion of repeat clickers indicates the training failed to change behavior in the riskiest population, so residual risk remains unacceptably high. While C (statistical significance) and D (benchmarking) are useful, B directly highlights that the most vulnerable cohort is still susceptible, undercutting the “success” claim.

Q6. A critical ERP system has been in production for ten years; original developers are no longer with the company. Penetration testers discover a SQL-injection flaw in a proprietary module. Source-code escrow exists, but the escrow agent reports the deposit package is “incomplete – no build instructions.” Which type of assessment is MOST appropriate BEFORE the vendor can issue an emergency patch?  
A. White-box fuzzing on the provided source fragments.  
B. Black-box dynamic testing combined with reverse engineering.  
C. Gray-box testing with read-only access to the production database.  
D. Static binary analysis on the compiled libraries.  

Correct Answer: B  
Explanation: With incomplete source, testers must treat the system as a black box and use dynamic testing plus reverse engineering to understand the flaw and verify any compensating controls. White-box (A) is impossible without buildable code, gray-box (C) does not address the module layer, and static binary analysis (D) alone may miss runtime behavior.

Q7. A healthcare provider’s internal audit charter states audits will follow “a risk-based approach consistent with ISO 19011.” The CISO wants to add privacy audits to the annual plan. Which factor MUST be documented FIRST to satisfy ISO 19011 risk-based planning?  
A. Audit program budget and number of available auditors.  
B. Context and relevant privacy legislation (HIPAA, GDPR, etc.) that create risk to the organization.  
C. A list of all audit suppliers that are certified to ISO 19011.  
D. The precise sampling technique that will be used during fieldwork.  

Correct Answer: B  
Explanation: ISO 19011 clause 5.2 requires understanding the context and risk environment before scoping the audit program. Legislation drives privacy risk, so it must be documented first to determine which processes, controls, and entities to audit. Budget (A) and sampling (D) come later; auditor certification (C) is not mandated by 19011.

Q8. A company is adopting a DevSecOps model. The security team wants to insert automated security testing into the CI/CD pipeline but must avoid slowing releases. Which testing approach provides the BEST balance between speed and defect-discovery effectiveness for every build?  
A. Full dynamic application security testing (DAST) with a 3-hour scan.  
B. Software composition analysis (SCA) for known vulnerable libraries plus incremental static analysis (SAST) on changed code only.  
C. Manual secure-code review performed by the security champion during the merge request.  
D. Full fuzz testing of every API endpoint.  

Correct Answer: B  
Explanation: SCA is fast and catches high-risk third-party flaws, while incremental SAST focuses only on new or modified code, keeping scan time under a few minutes and aligning with “shift-left” goals. Full DAST (A) and fuzzing (D) are too slow per build; manual review (C) is not scalable or automated.

Q9. An organization uses the STRIDE model to threat-model a new mobile banking app. During an assessment, the reviewer discovers that no test cases exist for the “Information Disclosure” threat. Which of the following test activities would BEST validate that sensitive data is not leaked?  
A. Conduct a code-review focused on hard-coded API keys.  
B. Run a network-layer DDoS test to observe failover logging.  
C. Perform static and dynamic analysis to search for sensitive data in crash logs, backups, and IPC channels.  
D. Execute a transaction while running an integrity checker to detect unauthorized code modification.  

Correct Answer: C  
Explanation: Information Disclosure in STRIDE maps directly to ensuring sensitive data is not exposed in unexpected channels such as logs, backups, or inter-process communication. Static and dynamic analysis can instrument the app to detect such leaks. A focuses on Spoofing/Tampering, B on Denial of Service, and D on Tampering again.

Q10. A cloud service provider (CSP) undergoes an annual SOC 2 Type II audit. The report includes an “unqualified” opinion but lists three “matters of substance” related to change-management timing. Prospective enterprise customers are asking if the report can be reused for their own vendor assessments. Which statement BEST describes the limitations of reusing the SOC 2 report?  
A. The report is restricted to management and customers under NDA, so it cannot be shared with prospects.  
B. The opinion covers only the CSP’s controls; each customer must still map the CSP controls to their own control objectives and risk tolerance.  
C. Because the opinion is unqualified, prospects can accept the report without further due diligence.  
D. The “matters of substance” automatically convert the opinion to “qualified,” invalidating the report.  

Correct Answer: B  
Explanation: SOC 2 reports provide a basis but not a blanket transfer of risk; customers must perform their own vendor-risk mapping and decide whether the noted change-management issues affect their environment. Sharing under NDA (A) is true but not the “best” limitation. An unqualified opinion does not eliminate customer due diligence (C), and “matters of substance” are disclosed weaknesses, not an opinion modifier (D).
