Q1. A multinational bank is preparing to enter a new, emerging market country where the anti-money-laundering (AML) regulations are still being drafted. The CISO has been asked to brief the board on how this regulatory uncertainty affects the organization’s overall risk posture. Which of the following best describes the primary risk the CISO should highlight?  
A. Strategic risk arising from potential changes in statutory compliance obligations  
B. Transaction risk that may increase the volume of fraudulent wire transfers  
C. Reputation risk caused by negative social-media sentiment in the home country  
D. Credit risk due to higher default rates among new retail customers  
Correct Answer: A  
Explanation: Entering a jurisdiction with evolving AML laws creates strategic risk—uncertainty at the board level about future compliance obligations that could fundamentally alter business models or require costly retro-fits. Transaction risk (B) is operational, not regulatory; reputation risk (C) is secondary and speculative; credit risk (D) is financial, not legal/regulatory.

Q2. The board of a publicly traded retailer has adopted a risk appetite statement that says, “No cybersecurity incident shall materially affect quarterly earnings.” After a PCI DSS assessment, the CIO learns that the current card-holder environment cannot be fully segmented before the holiday season, leaving a 35 % probability of a breach costing up to USD 40 M. What is the MOST appropriate risk response?  
A. Accept the risk and document the rationale in the risk register because holiday revenue is critical  
B. Avoid the risk by suspending all card-present transactions until segmentation is complete  
C. Mitigate the risk by accelerating a micro-segmentation project and adding continuous monitoring  
D. Transfer the risk by purchasing a cyber-insurance policy with a USD 50 M limit and no deductible  
Correct Answer: C  
Explanation: Mitigation reduces likelihood/impact to align residual risk with the board’s “no material effect” appetite. Acceptance (A) violates the appetite. Avoidance (B) is commercially unrealistic for a retailer. Transfer (D) still leaves a breach within the quarterly window; insurance reimburses but does not prevent material earnings impact.

Q3. A cloud service provider (CSP) offers a low-cost object-storage service that encrypts customer data at rest but retains full control of the keys. A healthcare client subject to HIPAA wants to use the service for two years of archived medical images. Which residual risk remains even after the CSP signs a Business Associate Agreement (BAA)?  
A. Unauthorized disclosure if the CSP is subpoenaed without the client’s knowledge  
B. Data loss due to bit rot or silent corruption on spinning disks  
C. Account hijacking because the client does not enforce MFA on its portal account  
D. Jurisdictional risk if the data center is moved from the U.S. to the EU  
Correct Answer: A  
Explanation: With CSP-held keys, the provider can decrypt and produce data in response to a lawful request; the BAA does not negate this residual risk. Bit rot (B) is normally addressed by CSP integrity controls and SLAs. Account hijacking (C) is a client-side control issue, not a residual risk of the CSP architecture. Jurisdictional risk (D) is typically disclosed and contractually stabilized.

Q4. During an ISO 27001 certification engagement, the lead auditor discovers that the organization’s information-security policy still references the retired CEO by name and last year’s revenue figures. The CISO argues that policy accuracy is “editorial” and does not affect security controls. Which risk-management principle has the CISO misunderstood?  
A. Risk ownership must be assigned at the executive level  
B. Policies must be reviewed and approved at least annually  
C. Due-care obligation requires current and accurate documentation  
D. Risk appetite must be expressed in monetary terms  
Correct Answer: C  
Explanation: Stale policies demonstrate lack of due care and can undermine both internal governance and external evidentiary requirements (e.g., in litigation). Annual review (B) is true but narrower; due care (C) is the overarching principle. Risk ownership (A) and monetary appetite (D) are unrelated to the accuracy issue.

Q5. A fintech start-up is building a mobile payment app. The founders, former software engineers, decide to embed privacy-by-design by minimizing data collection to only “name, phone, and card token.” A venture-capital partner warns that this approach may create a competitive disadvantage against rivals that use behavioral analytics. Which ethical principle should the founders prioritize when weighing the decision?  
A. Beneficence—maximizing societal benefit even if it reduces profit  
B. Non-maleficence—avoiding harm to users by limiting data exposure  
C. Justice—ensuring equal access to the app across all demographics  
D. Fidelity—maintaining loyalty to investor financial interests  
Correct Answer: B  
Explanation: Non-maleficence (“do no harm”) directly supports the decision to limit data, thereby reducing breach impact and surveillance potential. Beneficence (A) is broader and subjective. Justice (C) concerns fairness, not data minimization. Fidelity (D) to investors is secondary to ethical duty to users.

Q6. A government agency has classified a new citizen-identity database as “Top Secret” and mandated that all backups be stored with the same classification. A contractor suggests using a public cloud with FIPS-140-2 Level 3 encryption to cut costs. Which concept prevents this proposal from being accepted?  
A. Data sovereignty requirements that prohibit cross-border storage  
B. The need for an equivalent technical, procedural and legal environment  
C. The absence of zero-knowledge architecture in the cloud offering  
D. Lack of redundant power feeds in the chosen availability zone  
Correct Answer: B  
Explanation: For classified data, the cloud must provide an overall environment equivalent to that mandated by the classification—technical, procedural, contractual, legal. Sovereignty (A) may or may not apply. Zero-knowledge (C) is a subset of technical controls. Power feeds (D) are availability, not confidentiality, concerns.

Q7. A European manufacturer acquires a U.S. firm that has self-certified under the EU-U.S. Privacy Shield. Two months later, the Court of Justice of the EU invalidates Privacy Shield. The acquiring company’s privacy officer recommends continuing data transfers under the old privacy policy until new Standard Contractual Clauses (SCCs) are signed, arguing “no immediate enforcement is expected.” Which type of risk is the officer creating?  
A. Compliance risk—potential regulatory fines for unlawful transfers  
B. Transaction risk—currency fluctuation on cross-border payments  
C. Strategic risk—loss of market share to privacy-focused competitors  
D. Operational risk—system outage during SCC re-negotiation  
Correct Answer: A  
Explanation: Continued transfer without a valid mechanism violates GDPR, exposing the firm to administrative fines—pure compliance risk. The other options are financial, competitive, or technical, not regulatory.

Q8. A quantitative risk analysis shows that the Annualized Loss Expectancy (ALE) of a web-application breach is USD 4 M. A proposed security upgrade reduces the probability from 40 % to 5 % but costs USD 1.2 M annually. The board’s capital-investment hurdle rate is 3 years. What should the CISO recommend?  
A. Reject the upgrade because the exposure factor is still unknown  
B. Accept the upgrade because the 3-year ROI is positive  
C. Transfer the risk via insurance instead because premiums are only USD 800 k  
D. Defer the decision until a qualitative analysis is completed  
Correct Answer: B  
Explanation: Original ALE = USD 4 M; new ALE = 0.05/0.40 × 4 M = USD 0.5 M; annual savings = 3.5 M. Upgrade cost 1.2 M yields net annual benefit 2.3 M, paying back in ~0.5 years, well under the 3-year hurdle. Exposure factor (A) is already baked into the ALE. Insurance (C) costs less but does not reduce probability/impact. Deferring (D) ignores the positive ROI.

Q9. A startup’s CISO wants to adopt the NIST CSF but must map it to the ISO 27001 controls already demanded by European customers. Which risk-management technique is being performed?  
A. Risk aggregation across multiple business units  
B. Control mapping to satisfy overlapping compliance obligations  
C. Risk transference through standards adoption  
D. Qualitative risk ranking using maturity models  
Correct Answer: B  
Explanation: Mapping NIST CSF categories to ISO 27001 Annex A controls is a control-mapping exercise to achieve compliance efficiency. It is not aggregation (A), transference (C), or qualitative ranking (D).

Q10. A city government is drafting an incident-response plan. The mayor insists that “no ransomware payments will ever be made.” The CISO argues that this blanket statement could endanger lives if 911 systems are encrypted. Which governance document should be updated first to resolve the conflict?  
A. The risk-appetite statement endorsed by the city council  
B. The disaster-recovery plan’s RTO table for emergency services  
C. The business-impact analysis (BIA) for the 911 dispatch system  
D. The cyber-insurance policy exclusion list  
Correct Answer: A  
Explanation: The mayor’s directive is a risk-appetite position; lives-at-risk is a stakeholder impact. The appropriate venue to reconcile the two is the formal risk-appetite statement, which the council can amend to allow exceptions under life-safety criteria. BIA (C) informs but does not set appetite; DR RTO (B) and insurance (D) are downstream artifacts.
Q1. A multinational retailer wants to move customer loyalty data from on-premise servers in the EU to a new cloud region located in Singapore. The CISO is asked whether the transfer can proceed immediately. Which of the following is the MOST important security consideration that could delay the migration?  
A. The cloud provider’s data-center is Tier III, not Tier IV.  
B. Singapore’s PDPA may impose data-localization requirements.  
C. Cross-border transfer rules under GDPR require an adequacy decision or other safeguard.  
D. The retailer’s incident-response team is staffed only during EU business hours.  
Correct Answer: C  
Explanation: GDPR (and most modern privacy regimes) restricts transfers of personal data outside the EEA unless the destination country has an “adequacy” finding, or the exporter puts in place approved safeguards such as SCCs or BCRs. Failure to meet these conditions exposes the firm to regulatory fines and injunctions, so this is the show-stopper. A is irrelevant—Tier III still offers 99.98 % availability. B is incorrect because Singapore’s PDPA does not require loyalty data to stay in Singapore. D is an operational issue, not a legal barrier to transfer.

Q2. A hospital is negotiating a radiology-outsourcing contract with a third-party that will store CT scans containing patient data. The CISO must ensure the vendor contract meets HIPAA requirements. Which contractual clause BEST demonstrates that the hospital has met its “business associate agreement” obligation?  
A. Right to require annual penetration tests paid by the vendor.  
B. Requirement that the vendor return and securely destroy all PHI within 30 days of contract termination.  
C. Service-level agreement guaranteeing 99.9 % uptime for image retrieval.  
D. Indemnity clause limiting the hospital’s liability to USD 1 million per breach.  
Correct Answer: B  
Explanation: HIPAA explicitly requires a BAA to mandate return or destruction of PHI at termination. This addresses the Security Rule’s “assigned security responsibility” and Privacy Rule’s minimum-necessary principle. A is good but not explicitly required; C is operational, not privacy-focused; D is risk transfer, not core HIPAA compliance.

Q3. A zero-day ransomware attack encrypts 80 % of file shares at a manufacturing firm. The BC plan calls for a 4-hour RTO and 1-hour RPO for critical ERP data, yet after 12 hours the ERP is still unavailable. Post-event review shows the most recent off-site ERP backup was 6 hours old. Which portion of the BC/DR program failed?  
A. Risk assessment  
B. RPO definition  
C. Backup process (actual vs. required RPO)  
D. Incident classification  
Correct Answer: C  
Explanation: The stated RPO (1 hour) was not achieved because the last usable backup was 6 hours old, indicating the backup frequency or replication mechanism did not support the documented RPO. The RPO definition itself (B) was correct; the failure was in execution. A and D are not the primary cause of data loss.

Q4. A city government is building a smart-city IoT sensor network. The project sponsor argues that “because no personal data are collected, privacy impact is negligible.” The CISO disagrees. Which argument BEST supports the CISO’s position?  
A. Sensor metadata can be combined with open data sets to re-identify individuals.  
B. Availability risks from DDoS are privacy risks under GDPR.  
C. The sensors use Bluetooth 4.0, which has known encryption flaws.  
D. The vendor’s privacy notice is written in English only, violating local language laws.  
Correct Answer: A  
Explanation: Even anonymized telemetry (location, MAC addresses, noise levels) can be triangulated with public data to profile citizens, creating a privacy risk that triggers data-protection obligations. B incorrectly labels availability as a privacy risk. C is a confidentiality issue for sensor firmware, not personal data. D is a notice issue, not the primary privacy concern.

Q5. A software company’s board wants to quantify cyber-risk in monetary terms for the annual report. The CISO proposes a FAIR analysis. Which FAIR component estimates the probable frequency of a threat event?  
A. LEF (Loss Event Frequency)  
B. TEF (Threat Event Frequency)  
C. Vuln (Vulnerability)  
D. TCap (Threat Capability)  
Correct Answer: B  
Explanation: TEF is the rate at which a specific threat actor is expected to act against an asset. LEF is the subset of those events that become loss events after accounting for controls and vulnerability. Vuln describes the asset’s susceptibility, and TCap describes the attacker’s strength.

Q6. A financial regulator fines a bank USD 20 million for “failure to employ adequate risk-management governance.” The bank’s CIO had approved a USD 5 million security program that was deferred three years in a row. Which governance principle was MOST directly violated?  
A. Due care  
B. Due diligence  
C. Separation of duties  
D. Least privilege  
Correct Answer: A  
Explanation: Due care requires senior management to act reasonably to protect assets; repeatedly deferring a necessary security budget demonstrates negligence. Due diligence (B) is the ongoing monitoring activity—absent here but not the primary breach. C and D are operational controls unrelated to governance accountability.

Q7. A cloud SaaS vendor offers to sign ISO 27001 certification instead of answering a 300-line security questionnaire. The CISO needs to decide whether the certificate provides “adequate assurance.” Which of the following is the MOST reliable next step?  
A. Accept the certificate because ISO 27001 covers all security controls.  
B. Request the vendor’s most recent Statement of Applicability (SoA) and external audit report.  
C. Require the vendor to obtain SOC 2 Type II instead.  
D. Insist the vendor still complete the questionnaire.  
Correct Answer: B  
Explanation: The SoA and independent audit report detail which Annex-A controls are in scope, any non-conformities, and compensating controls, giving the CISO evidence to map to the firm’s risk appetite. ISO 27001 does not prescribe specific controls, so A is false. C is redundant—both ISO and SOC can provide assurance. D ignores efficient reuse of audit artifacts.

Q8. A company runs a bug-bounty program. A researcher reports a vulnerability that exposes PII of 10,000 customers. The researcher refuses to provide technical details until the company commits to a CVE and a USD 50k reward. Which CISSP ethical principle should guide the CISO’s response?  
A. Protect society, the profession, and the infrastructure.  
B. Act honorably, honestly, justly, and legally.  
C. Provide diligent and competent service.  
D. Advance and protect the profession.  
Correct Answer: B  
Explanation: (ISC)² Code ethics Canon II requires honesty and legality; paying for silence or extortion could violate anti-bribery laws. The CISO should negotiate in good faith, obtain details under responsible disclosure, then decide on reward and CVE based on policy. Canon I (A) is broader; C and D are less relevant to the immediate ethical dilemma.

Q9. A startup’s CISO is drafting an asset-classification policy. Development servers in the lab are currently labeled “Internal Use Only.” The servers contain experimental AI models that, if leaked, would give competitors a market advantage but do not contain personal data. Which classification label should the CISO assign?  
A. Public  
B. Internal Use Only  
C. Confidential  
D. Restricted  
Correct Answer: C  
Explanation: “Confidential” is appropriate for proprietary data whose unauthorized disclosure would harm the business. “Internal Use Only” understates the competitive impact. “Restricted” (D) is usually reserved for highly regulated or secret data (e.g., state secrets, PCI card data). Public (A) is clearly wrong.

Q10. A conglomerate operates in 40 countries. The board wants a single framework to harmonize risk appetite statements across subsidiaries with different regulatory environments. Which of the following standards provides the BEST overarching structure for integrating risk, compliance, and assurance?  
A. NIST SP 800-53 rev 5  
B. ISO 31000  
C. ISO 27001  
D. COBIT 2019  
Correct Answer: B  
Explanation: ISO 31000 is the international standard for enterprise risk management and is framework-agnostic, allowing alignment of risk appetite across diverse jurisdictions and industries. NIST 800-53 (A) and ISO 27001 (C) are control sets for information security, too narrow. COBIT (D) focuses on IT governance, not total enterprise risk.
Q1. A global retailer is preparing to open its first stores in a country that has just passed a data-localization statute requiring all personal data collected from residents to remain on servers physically located in that country. The company’s current cloud-based point-of-sale (POS) system is hosted in a U.S. region and replicates nightly to a second U.S. region. The CISO has been asked to present a risk-based recommendation to the board within 30 days. Which of the following should be the CISO’s PRIMARY focus when briefing the board?  
A. Quantifying the financial impact of losing local market access if the firm is found non-compliant  
B. Evaluating the technical feasibility of encrypting all resident data before it leaves the country  
C. Drafting an exception request to the local data-protection authority asking for a one-year grace period  
D. Calculating the cost difference between building an in-country data center versus contracting with a local cloud provider that can guarantee data residency  

Correct Answer: A  
Explanation: The first domain stresses that risk management starts with understanding business consequence. Choice A directly addresses the potential business impact (loss of market access) and provides the board with the monetary context needed to make an informed risk decision. B is a control detail, not a board-level risk statement. C is a tactical workaround that may not be granted. D is an implementation option that should be analyzed only after the business impact is understood.

Q2. A hospital’s executive committee has approved a new electronic health-record (EHR) system that will exchange data with affiliated clinics through public internet links. The CIO argues that because the system is HIPAA-compliant out-of-the-box, no further risk assessment is necessary. The CISO disagrees. Which risk-management principle best supports the CISO’s position?  
A. Risk ownership cannot be transferred to a vendor; residual risk must always be reassessed in the deploying organization’s context.  
B. Qualitative risk assessment is required for all public-network data flows regardless of vendor claims.  
C. Annual penetration testing is mandated by HIPAA for any internet-facing system.  
D. The approval of the executive committee automatically lowers the risk rating to “acceptable.”  

Correct Answer: A  
Explanation: Domain 1 teaches that even when a vendor provides a compliant product, the organization still owns the residual risk once the system is integrated into its unique environment. B is partially true but too narrow; qualitative assessment is a method, not a principle. C is a possible control, not a principle. D contradicts the concept that risk acceptance must be evidence-based, not automatic.

Q3. A fast-growing SaaS start-up has limited security staff. The CISO wants to adopt a control framework that will satisfy both SOC 2 Type II audits and future enterprise customers without imposing heavy documentation overhead. Which of the following approaches BEST aligns with risk-management best practice?  
A. Map SOC 2 criteria to ISO 27001 Annex A and implement only the controls that are material to the company’s risk profile  
B. Adopt the NIST SP 800-53 moderate baseline in its entirety to ensure no control gaps  
C. Outsource all security functions to a managed service provider that is ISO 27001 certified  
D. Delay framework adoption until the company reaches 250 employees, then perform a single risk assessment  

Correct Answer: A  
Explanation: Risk management is context-specific; adopting only material controls avoids “check-box” security while still meeting audit needs. B creates unnecessary overhead for a start-up. C transfers operational burden but does not eliminate risk ownership or the need for internal governance. D postpones risk treatment and violates the principle of due care.

Q4. A nation-state attack group is rumored to be targeting the power-grid sector with zero-day malware. A regional utility’s risk register already lists “nation-state cyber attack” as a very high impact but very low likelihood event. The board is concerned that the likelihood estimate is outdated. Which of the following sources would BEST support an updated, defensible likelihood estimate?  
A. The company’s historical incident database over the past five years  
B. Industry-wide threat-intelligence sharing portals specific to energy-sector ICS attacks  
C. The annual loss expectancy (ALE) calculated from last year’s penetration-test findings  
D. The vendor-selected CVSS scores of patches deployed in the last quarter  

Correct Answer: B  
Explanation: Likelihood for low-frequency, high-impact events is best informed by sector-specific threat intelligence. Historical internal data (A) will be sparse for events that have not yet occurred. C relates to known vulnerabilities, not adversary intent. D measures severity of existing vulnerabilities, not probability of a nation-state attack.

Q5. A multinational manufacturer is negotiating cyber-insurance for the first time. The insurer requires a documented risk-appetite statement. Which of the following statements BEST satisfies the insurer’s requirement while remaining internally useful?  
A. “The organization has a zero-risk tolerance for any event that could disrupt manufacturing.”  
B. “The organization accepts no more than a 2% deviation from annual revenue due to cyber events, with a confidence level of 95%, and will insure or mitigate beyond this threshold.”  
C. “All cyber risk must be reduced to ‘low’ as defined by the corporate heat map.”  
D. “Risk appetite is reviewed annually by the CISO and may be adjusted without board approval.”  

Correct Answer: B  
Explanation: A measurable, monetary risk-appetite statement (B) is auditable and aligns with both insurance underwriting and ISO 31000. A is operationally unrealistic and therefore not credible. C is qualitative and ambiguous. D omits the board’s governance role in setting risk appetite.

Q6. A city government is deploying body-worn cameras for police officers. Civil-rights groups worry that footage could be used for unauthorized facial-recognition surveillance. Legally, the police department can record in public spaces, but the mayor wants to demonstrate ethical data use. Which risk treatment option BEST addresses ethical concerns while remaining compliant with the law?  
A. Avoid the risk by canceling the camera program entirely  
B. Transfer the risk by requiring the camera vendor to indemnify the city against privacy lawsuits  
C. Mitigate the risk through policy prohibiting facial-recognition processing of footage without court order and conduct annual audits  
D. Accept the risk because the recording activity itself is legal  

Correct Answer: C  
Explanation: Ethical risk is still risk; mitigation via policy and audit demonstrates due care and maintains public trust. A is an extreme business-negative. B does not prevent reputational damage. D ignores stakeholder trust and could increase liability if misuse occurs.

Q7. A payment-processor’s board has declared that any single security incident costing more than USD 5 million will be considered a “material breach” of risk appetite. The CISO needs to translate this into operational terms for the IT team. Which of the following metrics BEST operationalizes the board’s statement?  
A. Maximum single loss expectancy (SLE) for any threat–asset pair in the risk register  
B. Annualized rate of occurrence (ARO) for denial-of-service attacks  
C. Number of critical vulnerabilities older than 30 days  
D. Mean time to patch (MTTP) across all systems  

Correct Answer: A  
Explanation: SLE directly measures the financial impact of one occurrence, aligning with the board’s monetary threshold. B, C, and D are frequency or process metrics that do not, by themselves, indicate dollar loss.

Q8. A software company’s security steering group has approved a risk response that relocates sensitive R&D source code from an on-premise data center to an IaaS provider headquartered in a foreign country. The CISO’s next task is to update the corporate risk register. Which update is MOST critical for maintaining traceability?  
A. Change the threat entry from “insider theft” to “foreign government subpoena” and re-score residual risk  
B. Reduce the inherent risk score because the cloud provider is ISO 27001 certified  
C. Remove the risk entry because the code now resides outside the company’s physical perimeter  
D. Add a new risk entry for “cloud misconfiguration” and assign risk ownership to the cloud provider  

Correct Answer: A  
Explanation: The threat landscape changes with jurisdiction; the register must reflect new threats (e.g., extraterritorial subpoena) and updated residual risk. B incorrectly lowers inherent risk—certification does not eliminate it. C destroys audit trail and violates risk-management principles. D is partially correct but assigning ownership to the provider is invalid; the company always retains risk ownership.

Q9. A financial-services firm must comply with both PCI DSS and a new domestic regulation that mandates encryption of all credit-card data with “government-approved ciphers.” The government list excludes some algorithms that PCI DSS allows. The firm has already invested heavily in hardware security modules (HSMs) that support the PCI-approved ciphers only. Which risk-management strategy is MOST appropriate?  
A. Accept the risk and continue using existing HSMs because PCI DSS is the globally recognized standard  
B. Avoid the risk by ceasing to process credit-card transactions until the HSMs are upgraded  
C. Mitigate the risk by deploying additional HSMs that support government-approved ciphers and re-encrypt the data  
D. Transfer the risk by asking the card brands to assume liability for any regulatory fines  

Correct Answer: C  
Explanation: Mitigation through additional controls (new HSMs) allows continued business while achieving compliance with the stricter requirement. A invites regulatory fines. B is business-prohibitive. D is not feasible—card brands will not accept liability for local law violations.

Q10. A CISO is reviewing the company’s security-awareness program after a series of successful business-email-compromise (BEC) scams. The phishing simulations show a 5% click-through rate, down from 25% two years ago, yet BEC losses have doubled in the same period. Which risk-assumption mistake BEST explains this apparent contradiction?  
A. The risk assessment assumed that reduced click-through rate directly translates to lower financial loss, ignoring adversary adaptation and dollar amount per incident  
B. The inherent risk of BEC was incorrectly calculated using qualitative methods instead of quantitative  
C. The residual risk was accepted by the business without board sign-off  
D. The security-awareness program adopted NIST SP 800-50 instead of 800-16  

Correct Answer: A  
Explanation: The assumption that fewer clicks equal lower loss is flawed; BEC actors may target fewer but higher-value transactions. B is method-oriented and does not explain the doubling of losses. C is a governance issue, not an assumption error. D is a framework choice, not a root cause of increased losses.
Q1. The CISO of a global retailer learns that a new EU regulation will require explicit, revocable consent for every instance of biometric processing. The company currently uses facial-recognition cameras in 800 stores to detect known shoplifters, and the data is stored in a cloud located in the United States. Which action is MOST appropriate in the first 30 days?  
A. Re-configure cameras to blur faces by default and only un-blur when a court order is received.  
B. Draft a binding corporate rule (BCR) that unilaterally declares the data transfers as adequate.  
C. Perform a gap analysis that maps every biometric data flow against the new consent and transfer requirements.  
D. Immediately re-route all video feeds to a new EU-based cloud region and delete the U.S. copies.  

Correct Answer: C  
Explanation: A gap analysis is the first step to understand the scope of non-compliance before designing controls (ISO 27001 Plan-Do-Check-Act). A is wrong because it may not satisfy the “explicit consent” requirement and could cripple loss-prevention. B is wrong because BCRs must be approved by regulators, not self-declared. D is premature and costly without knowing retention limits, legal basis, or whether onward transfers are still allowed.

---

Q2. A hospital’s executive committee asks the security team to quantify the annualized loss expectancy (ALE) of a new ransomware threat. The team estimates an attack would corrupt 20 % of the 5 TB PACS image archive. Recovery cost is $2,000 per TB, downtime is 6 hr at $15,000/hr, and the attack probability is 25 % per year. What ALE should be presented?  
A. $27,500  
B. $30,000  
C. $32,500  
D. $130,000  

Correct Answer: C  
Explanation: ALE = SLE × ARO. Single loss = (5 TB × 20 % × $2,000) + (6 hr × $15,000) = $2,000 + $90,000 = $92,000. ARO = 0.25. ALE = $92,000 × 0.25 = $23,000 (corruption) + $9,500 (downtime portion) = $32,500. A omits downtime; B omits corruption; D uses ARO = 1.

---

Q3. A multinational bank wants to replace its paper-based vendor NDA process with an e-signature platform. The CISO must ensure the solution provides non-repudiation that will hold up in New York, London, and Singapore courts. Which requirement is MOST critical?  
A. AES-256 encryption of the PDF at rest.  
B. Digital signatures created with a FIPS 140-3-validated HSM and a publicly trusted CA.  
C. GDPR data-processing addendum with the vendor.  
D. ISO 27001 certification of the SaaS provider.  

Correct Answer: B  
Explanation: Courts accept digital signatures only if the signer’s private key is under sole control and backed by a trustworthy CA; an HSM provides this. Encryption (A) protects confidentiality, not non-repudiation. GDPR (C) and ISO 27001 (D) are good governance but do not directly prove who signed.

---

Q4. A city government is drafting an information-security policy for its smart-municipality program. The mayor insists the policy must “never impede innovation.” Which approach BEST reconciles this mandate with security objectives?  
A. Reference an ISO 27001 control set and allow waivers for any control that slows deployment.  
B. Publish a high-level policy that mandates risk assessment and assigns ownership, then delegate detailed standards to individual departments.  
C. Adopt the vendor’s default security settings as the official policy.  
D. Issue a single city-wide technical baseline and require every IoT project to comply before procurement.  

Correct Answer: B  
Explanation: A high-level policy sets governance expectations without dictating technology, letting departments innovate while still requiring risk ownership. A undercuts security by pre-authorizing waivers. C transfers policy control to vendors. D blocks innovation by front-loading lengthy approvals.

---

Q5. A software company’s board wants to measure the effectiveness of the security-awareness program. The company runs monthly phishing simulations; over six months the click-through rate dropped from 18 % to 5 %, yet two employees who never clicked still leaked credentials via a fake LinkedIn survey. Which metric should the CISO recommend to the board?  
A. Replace click-through rate with mean time to report phishing (MTTR-P).  
B. Add a lagging indicator: number of incidents traced to human error.  
C. Switch to measuring training completion percentage only.  
D. Stop simulations and invest in technical filters only.  

Correct Answer: B  
Explanation: A lagging indicator (incidents caused by human error) captures credential leaks that bypass click-through tests, giving the board a risk-based outcome metric. A is useful but still leading; C ignores behavior change; D abandons human controls entirely.

---

Q6. A cloud service provider (CSP) offers a shared-tenancy PaaS for health records. The provider’s certification statement says: “Our controls meet HIPAA requirements; customer still responsible for PHI.” A covered entity customer suffers a breach because an S3 bucket was mis-configured to “public.” Who is legally liable under U.S. HIPAA, and what concept determines this?  
A. CSP is liable because it processed PHI; concept of safe harbor.  
B. Customer is liable; concept of shared responsibility.  
C. CSP is liable; concept of downstream liability.  
D. Neither party is liable; public cloud is exempt.  

Correct Answer: B  
Explanation: HIPAA’s business-associate agreement and OCR guidance place configuration of access controls on the customer under the shared-responsibility model. Safe harbor (A) applies to encryption, not mis-configuration. CSP is not automatically liable (C), and clouds are not exempt (D).

---

Q7. A defense contractor uses the NIST SP 800-171 control set to protect controlled unclassified information (CUI) on a local file server. A new subsidiary in Canada must access the same CUI via a VPN. Which step is REQUIRED before allowing access?  
A. Update the risk register to reflect cross-border data flows.  
B. Obtain a Canadian government security clearance for the subsidiary.  
C. Map 800-171 controls against Canadian Centre for Cyber Security ITSG-33 and document any gaps.  
D. Encrypt the VPN with AES-256 and continue current controls.  

Correct Answer: C  
Explanation: DFARS 252.204-7012 requires that any subsidiary handling CUI on behalf of the prime contractor apply “equivalent” security; mapping against ITSG-33 proves equivalence. A is necessary but not sufficient; B is not required for CUI; D ignores potential gaps in logging, incident response, etc.

---

Q8. A zero-day exploits a widely used image-processing library. The vendor will not have a patch for 14 days. The CISO convenes a war-room and must choose the BEST risk-response strategy for the company’s public-facing e-commerce site.  
A. Accept the risk because a patch is imminent.  
B. Mitigate by temporarily disabling image upload and using a WAF rule that blocks malformed magic bytes.  
C. Transfer by buying a cyber-insurance rider that covers zero-day losses.  
D. Avoid by shutting down the entire site until the patch is released.  

Correct Answer: B  
Explanation: Mitigation with a virtual patch (WAF rule) plus disabling the vulnerable function reduces likelihood quickly without halting revenue. Accept (A) ignores active exploitation. Transfer (C) does not prevent service disruption. Avoid (D) is disproportionate.

---

Q9. A privacy impact assessment (PIA) for a new mobile banking app shows that collecting precise geolocation for fraud detection creates high privacy risk to data subjects. The DPO recommends “privacy by design.” Which control BEST implements this principle?  
A. Add a click-through consent banner that geolocation is collected.  
B. Collect city-level location instead of GPS coordinates and re-evaluate fraud-detection accuracy.  
C. Encrypt the GPS coordinates in transit and at rest.  
D. Provide an opt-out toggle in the settings menu.  

Correct Answer: B  
Explanation: Minimizing data precision (city vs. GPS) is core to privacy by design; it lowers risk while retaining utility. Consent (A) and opt-out (D) are lawful but do not reduce the data’s sensitivity. Encryption (C) protects confidentiality, not privacy from over-collection.

---

Q10. A conglomerate with four autonomous divisions wants to create an enterprise-wide risk appetite statement. The CISO’s first draft is rejected by the board because it lists only technical IT risks. Which addition would BEST satisfy governance expectations?  
A. Include a risk tolerance table for reputation, regulatory, financial, and strategic risk categories.  
B. Attach the NIST 800-53 control catalog as an appendix.  
C. Quantify every risk in monetary terms using FAIR.  
D. Require divisions to adopt the same risk-scoring matrix (1–5).  

Correct Answer: A  
Explanation: A board-level appetite statement must cover all material risk categories, not just IT. Tolerance tables translate risk into business terms. B is too tactical; C is useful but not the only dimension; D standardizes scoring but does not articulate appetite.
Q1. A multinational bank is preparing to enter a new Asian market where the regulator requires all customer data to be “kept in-country” and accessible to domestic intelligence services on demand. The CISO’s risk assessment shows that the local data-centre operator has never obtained an ISO 27001 certification and the country’s corruption index is rated “high.” Executive management still wants to proceed for strategic-reasons. Which risk-handling option is MOST consistent with fiduciary duty to shareholders?  
A. Accept the risk and document the rationale in the risk register once the contract is signed.  
B. Avoid the risk by abandoning the market entry and surrendering first-mover advantage.  
C. Transfer the risk by buying an insurance policy that covers regulatory fines and civil damages.  
D. Mitigate the risk by negotiating contractual security controls, right-to-audit clauses, and a comprehensive cyber-insurance policy that names the bank as loss-payee.  

Correct Answer: D  
Explanation: Mitigation (D) reduces likelihood and impact to a level commensurate with the strategic reward while preserving market entry; residual risk can then be accepted by the board. Accept (A) without first lowering the risk would breach fiduciary duty given the high inherent risk. Avoid (B) is unnecessarily conservative and ignores business strategy. Transfer alone (C) does not satisfy the regulatory requirement that the bank remain ultimately responsible for data protection; insurance is only a financial back-stop, not a control.

---

Q2. A SaaS provider’s board has adopted an “acceptable residual risk” threshold of ≤ 2 % annualised loss expectancy (ALE) of EBITDA. During the annual review, the CISO calculates that a newly discovered vulnerability exposes the firm to an ALE of USD 4.2 M (4.5 % EBITDA). A patch exists but will cost USD 1.1 M to deploy across the multi-tenant estate and degrade performance, generating an estimated USD 0.8 M in lost revenue. Which choice BEST demonstrates risk-based decision making aligned with the board’s risk appetite?  
A. Patch immediately because the vulnerability ALE exceeds the threshold.  
B. Do not patch; the sum of patching cost and revenue loss (USD 1.9 M) is less than the ALE, so the business comes out ahead.  
C. Accept the risk because the vulnerability is not yet public and the firm has WAF logs that might detect exploitation.  
D. Re-evaluate the quantitative model with threat-intelligence that lowers the exposure factor, then re-assess against the 2 % threshold.  

Correct Answer: D  
Explanation: The board’s monetary threshold is policy; before deviating from it the model assumptions must be validated (D). Option A ignores cost-benefit and could violate fiduciary duty by overspending. B compares cumulative cost only to gross ALE, not to the 2 % cap. C is dangerous “security through obscurity” and ignores the already-quantified exceedance of appetite.

---

Q3. A U.S.-based cloud company is negotiating with a European utility to process smart-grid data. The utility insists that the provider become “GDPR art. 28 compliant” and “certified under the EU-U.S. Data Privacy Framework (DPF).” The provider’s GC notes that DPF certification is optional and GDPR Article 28 is only one of several lawful paths. The CISO recommends instead signing Standard Contractual Clauses (SCCs) and encrypting data at rest with keys kept in the United States. Which concept is MOST relevant to determining whether the CISO’s recommendation introduces unacceptable residual risk?  
A. Due care versus due diligence  
B. Legal precedent in Schrems II  
C. Safe-harbour sunset provisions  
D. NIST SP 800-53 control baselines  

Correct Answer: B  
Explanation: Schrems II (B) invalidated Privacy Shield and cast doubt on SCCs absent “supplementary measures” for U.S. government surveillance risk, directly impacting the CISO’s plan. Due care/diligence (A) is too generic. Safe-harbour (C) is obsolete. NIST baselines (D) are technical and do not address cross-border transfer law.

---

Q4. A hospital chain wants to outsource medical-transcription services to a vendor that uses offshore staff in a country with no HIPAA-equivalent law. The contract will include HIPAA Business Associate Agreement (BAA) language, but the vendor refuses to allow on-site audits citing COVID restrictions. Which control combination BEST satisfies the “security rule” requirement for reasonable assurance?  
A. Right-to-audit clause, annual SOC 2 Type II report from an independent CPA, and contractual requirement for encryption of PHI in transit and at rest.  
B. Force-majeure waiver that shifts all liability to the vendor if PHI is breached.  
C. Purchase of a cyber-liability policy with a USD 10 M limit naming the hospital as beneficiary.  
D. Require the vendor to obtain a PCI-DSS ROC because it covers card data and therefore implies strong security.  

Correct Answer: A  
Explanation: SOC 2 + right-to-audit + encryption (A) gives verifiable, ongoing assurance when physical audits are impractical. Force-majeure waiver (B) is unenforceable and does not demonstrate due diligence. Insurance (C) is only financial recovery, not assurance. PCI-DSS (D) is irrelevant to PHI.

---

Q5. A fintech start-up’s board has adopted the NIST CSF as its “single source of truth.” During a Series-B due-diligence review, investors discover that the company has implemented 85 % of CSF sub-category controls but has not produced a single policy document longer than two pages. Which principle is MOST violated?  
A. Alignment to the CSF Inform function  
B. Governance through “tone at the top”  
C. Due care versus due diligence  
D. Transparency to shareholders  

Correct Answer: A  
Explanation: The Inform function requires that policies, processes, and procedures be documented and communicated; absence of documentation violates this regardless of control implementation. Tone at the top (B) is present but undocumented. Due care (C) is broader and less specific. Transparency (D) is secondary to operational evidence.

---

Q6. A national telecom regulator proposes a new rule: “Critical-network operators must maintain at least 99.99 % availability averaged over any calendar month, measured at the service interface.” The CISO calculates that achieving this will require N+2 redundancy and an estimated USD 40 M CAPEX. The CFO argues this is a “business decision,” not a security issue. Which CISSP concept BEST supports the CISO’s position that availability requirements are within the security programme’s scope?  
A. The AIC triad  
B. ISO 27001 Annex A controls  
C. COBIT DSS05 process  
D. COSO ERM cube  

Correct Answer: A  
Explanation: Availability is one leg of the AIC (confidentiality, integrity, availability) triad foundational to security management. The other choices are frameworks or processes that implement but do not define the scope.

---

Q7. A cloud vendor offers a “shared responsibility matrix” that states: “Customer is responsible for encrypting data in transit; provider is responsible for encrypting data at rest.” The customer CISO discovers that the provider’s “at-rest encryption” uses transparent disk encryption with keys held in the same tenant account. Government subpoenas could therefore compel the provider to hand over unencrypted data. Which risk remains despite the provider’s claim of “encryption at rest”?  
A. Jurisdictional insider threat  
B. Residual data remanence  
C. Vendor lock-in  
D. Key-custodian conflict of interest  

Correct Answer: D  
Explanation: The provider is both data processor and key custodian, creating a conflict (D) that negates the protective value of encryption against lawful access requests. Insider threat (A) is broader and less specific. Remanence (B) is irrelevant to live data. Lock-in (C) is an economic, not confidentiality, risk.

---

Q8. A U.S. state enacts a law requiring any company that “does business” in the state and suffers a breach affecting > 500 residents to pay USD 500 per affected record into a consumer-privacy fund. A regional retailer estimates it holds 200 k resident records and its breach probability is 0.3 per year. The CISO proposes tokenising the data set at a one-time cost of USD 1.2 M, reducing breach probability to 0.05. Which ROI calculation BEST justifies the control investment to the board?  
A. (200 000 × 500 × 0.3) – 1 200 000 = 29.8 M benefit; ROI = 29.8 M / 1.2 M = 2 483 %  
B. (200 000 × 500 × 0.05) – 1 200 000 = –200 k; ROI negative, reject control  
C. (200 000 × 500 × 0.25) – 1 200 000 = 23.8 M; ROI = 23.8 M / 1.2 M = 1 983 %  
D. 1 200 000 / (200 000 × 500) = 0.012; ROI = 1.2 %  

Correct Answer: C  
Explanation: The relevant saving is the reduction in expected loss (0.3 – 0.05 = 0.25) multiplied by records and fine, minus cost (C). A uses old probability, not reduction. B uses post-mitigation probability incorrectly. D computes cost as percentage of maximum loss, not ROI.

---

Q9. A global manufacturer’s risk register shows a “critical” risk that a single source supplier of custom ASIC chips could implant hardware Trojans. The board decides to invest USD 5 M in an on-chip integrity-verification technology rather than dual-source. Which risk treatment strategy is being employed?  
A. Risk avoidance  
B. Risk mitigation  
C. Risk transfer  
D. Risk acceptance  

Correct Answer: B  
Explanation: Integrity-verification technology lowers the likelihood/impact of Trojan insertion, classic mitigation (B). Avoidance (A) would mean dropping the supplier. Transfer (C) would be insurance or contractual indemnity. Acceptance (D) would be doing nothing.

---

Q10. A security-awareness vendor offers a phishing-simulation service that requires employees to click a link that briefly installs a benign beacon before redirecting to training. The works-council (employee union) objects, claiming the beacon is “spyware” under national labour law. The CISO argues the beacon is essential for metrics. Which governance concept should guide the final decision?  
A. Alignment of security objectives with legal and regulatory requirements  
B. Cost-benefit analysis of the training programme  
C. Principle of least privilege  
D. Single sign-on integration  

Correct Answer: A  
Explanation: Labour law is a regulatory requirement; security must align with it (A). Cost-benefit (B) is secondary to legal compliance. Least privilege (C) and SSO (D) are technical, not governance, issues.
Q1. A global pharmaceutical company is about to acquire a smaller competitor that has a promising drug pipeline but a history of compliance violations. The CISO has been asked to provide a security opinion to the M&A steering committee within five business days. The due-diligence data room contains only high-level policy documents and last year’s SOC-2 Type II report. Which of the following is the MOST important next step before forming an opinion?  
A. Accept the SOC-2 report at face value and note no critical findings.  
B. Request the right to perform a targeted security assessment of the competitor’s R&D network.  
C. Calculate the annualized loss expectancy (ALE) for each drug patent.  
D. Draft a memorandum of understanding (MOU) requiring the competitor to adopt the parent’s security policy on Day 1.  
Correct Answer: B  
Explanation: A targeted assessment (B) provides the evidence needed to judge residual risk before the company is legally and financially committed. Accepting the SOC-2 (A) ignores the competitor’s compliance history and the limited scope of SOC-2. Calculating ALE (C) is premature without understanding the actual control gaps. Drafting an MOU (D) is a post-deal activity and does not inform the current risk decision.

Q2. A national retailer’s board has just approved a five-year strategic plan that expands e-commerce revenue from 20 % to 60 % of total sales. The CISO must now update the enterprise risk register. Which risk is MOST likely to increase as a direct result of this strategic shift?  
A. Physical theft of point-of-sale terminals in stores  
B. Credit-card skimming at gas-station pumps owned by partners  
C. Distributed denial-of-service (DDoS) attacks against the public website  
D. Insider theft of paper-based customer receipts  
Correct Answer: C  
Explanation: A 3× increase in e-commerce revenue makes the public website a higher-value target for DDoS extortion or competitor sabotage (C). Physical POS theft (A) and paper receipts (D) decline as store traffic drops. Skimming at partner pumps (B) is unrelated to the retailer’s online strategy.

Q3. A hospital system is negotiating cyber-insurance coverage. The insurer offers a 25 % premium reduction if the hospital can demonstrate that it has “implemented an organization-wide risk management framework aligned to ISO 27005.” Which document will BEST satisfy the insurer’s requirement?  
A. The hospital’s balanced scorecard showing KPI trends for the last four quarters  
B. A signed attestation from the CIO that HIPAA controls are “effectively deployed”  
C. The hospital’s most recent risk assessment report with an executive summary mapping methodology to ISO 27005  
D. A spreadsheet listing every CVE patched in the prior month  
Correct Answer: C  
Explanation: The risk assessment report (C) explicitly shows the hospital follows ISO 27005 scoping, risk identification, analysis, and treatment steps. A balanced scorecard (A) is too high-level, a CIO attestation (B) lacks objective evidence, and a CVE list (D) addresses only vulnerability management, not enterprise risk.

Q4. A cloud SaaS provider stores EU customer data in AWS Dublin and US customer data in AWS us-east-1. A new German customer requires that its data never leave the EU, even for support tickets. The provider’s standard contract states: “Support may be performed from any location where our personnel reside.” Which governance action should the provider take FIRST?  
A. Enable AWS CloudTrail in Dublin to log all API calls  
B. Draft a data-processing addendum (DPA) that limits support access to EU-based staff  
C. Perform a business-impact analysis (BIA) for the German customer  
D. Encrypt all data stored in Dublin with customer-managed keys  
Correct Answer: B  
Explanation: The contractual statement is the primary compliance gap; a DPA (B) modifies it to satisfy data-localization requirements before any technical controls matter. CloudTrail (A) and encryption (D) do not prevent cross-border human access. A BIA (C) is useful but does not address the immediate legal issue.

Q5. A FinTech start-up has three co-founders who each own 30 % of the company and insist on keeping local root access to production servers “for agility.” The venture-capital term sheet requires SOX compliance within 12 months. Which control will BEST reduce the risk of financial-reporting misstatement while still allowing rapid feature releases?  
A. Implement a segregation-of-duties policy that separates code deployment from production approval  
B. Require each founder to sign an annual integrity statement  
C. Mandate phishing-awareness training for all employees  
D. Install a next-generation firewall at the colocation facility  
Correct Answer: A  
Explanation: SOX focuses on financial-statement accuracy; segregation of duties (A) prevents any single founder from deploying unaudited code that could manipulate transaction logs. Integrity statements (B) and phishing training (C) are useful but do not enforce technical enforcement. A firewall (D) protects network perimeter, not financial logic.

Q6. A provincial government is drafting legislation that would require every critical-infrastructure operator to report “material cyber incidents” within six hours of discovery. The CISO of a regional power utility argues that the proposed timeline is “unrealistic and creates legal risk.” Which risk management technique is the CISO attempting to use?  
A. Risk avoidance  
B. Risk transference  
C. Risk acceptance  
D. Risk rejection  
Correct Answer: D  
Explanation: By lobbying to change the regulation, the CISO is attempting to reject (D) the risk (i.e., eliminate the requirement) rather than avoid, transfer, or accept it. Avoidance (A) would mean exiting the critical-infrastructure sector. Transference (B) would involve insurance. Acceptance (C) would be quietly complying.

Q7. A software vendor offers a bug-bounty program that pays up to USD 50 000 for critical vulnerabilities. A security researcher discovers a flaw that exposes personal data of 100 000 users and demands USD 200 000 “consulting fee” or he will publish the flaw on social media. The vendor’s legal team classifies this as extortion. Which CISSP ethical principle MOST directly conflicts with paying the researcher?  
A. Protect society, the common good, necessary public trust and confidence, and the infrastructure.  
B. Act honorably, honestly, justly, responsibly, and legally.  
C. Provide diligent and competent service to principals.  
D. Advance and protect the profession.  
Correct Answer: B  
Explanation: Paying an extortionate demand violates legal and honest conduct (B). While protecting society (A) is important, the immediate conflict is the unethical/illegal nature of the payment. Competent service (C) and advancing the profession (D) are secondary.

Q8. A multinational mining firm operates in a country that suddenly criminalizes the use of strong encryption without government-issued licenses. The firm’s VPNs and full-disk encryption are now non-compliant locally, but turning them off would violate the parent company’s global policy and EU data-protection clauses. Which of the following is the BEST risk response?  
A. Disable encryption for local laptops and accept the residual risk  
B. Continue using encryption and secretly pay “fines” to local officials  
C. Engage legal counsel to file for a license or seek a regulatory exemption while implementing compensating controls (e.g., strict physical security, tokenization)  
D. Immediately exit the country and abandon the mine  
Correct Answer: C  
Explanation: Engaging counsel and seeking legitimate relief (C) balances legal compliance with security. Disabling encryption (A) creates unacceptable risk. Bribery (B) is illegal under the parent’s anti-corruption policy. Immediate exit (D) is disproportionate without exploring legal avenues.

Q9. A CISO has adopted the NIST CSF and mapped all 108 sub-category controls to internal processes. The board now asks, “How do we know our cyber-risk is ‘within appetite’?” Which deliverable will BEST answer the board’s question?  
A. A heat-map that plots residual risk against the board-approved risk-appetite statement  
B. The latest penetration-test report showing zero critical findings  
C. A balanced budget for the security department  
D. A comparison of the company’s security spending to industry peers  
Correct Answer: A  
Explanation: A heat-map (A) directly compares residual risk levels to the quantitative or qualitative thresholds in the approved appetite statement. A clean pen-test (B) is point-in-time. Budget compliance (C) and peer benchmarking (D) do not measure risk against appetite.

Q10. A Fortune 500 company’s risk committee has set a risk-appetite statement that “single-source supplier risk shall not exceed 5 % of annual revenue.” Procurement has just signed a five-year, USD 2 billion cloud contract with one hyperscaler, representing 8 % of projected annual revenue. What should the CISO recommend FIRST?  
A. Immediately terminate the contract to avoid regulatory scrutiny  
B. Document the exception in the risk register, require board-level approval, and mandate a contingency plan (e.g., data portability testing, exit clauses)  
C. Purchase cyber-insurance for USD 2 billion  
D. Shift 3 % of revenue to a second cloud provider within 30 days  
Correct Answer: B  
Explanation: The appetite is breached; the governance process (B) ensures explicit board acceptance and mitigating controls. Immediate termination (A) is commercially unrealistic. Insurance (C) does not reduce supplier concentration risk. A forced 30-day shift (D) is operationally infeasible and may create more risk.
