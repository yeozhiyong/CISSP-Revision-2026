Q1. A multinational cloud-storage provider is preparing to migrate legacy customer data from on-premise tape archives to a new multi-region object-storage service. The tapes contain mixed data classifications (Confidential, Private, Internal, Public) that were originally assigned by different business units using inconsistent criteria. The CISO has asked the security team to produce a single data-classification scheme for the new environment that will satisfy both GDPR and PCI DSS requirements. Which action is MOST critical before any data are moved?  
A. Decrypt all tapes, re-encrypt them with the cloud provider’s KMS, and then label each object with the original business-unit classification.  
B. Perform an data-discovery and data-mapping exercise to inventory every data element and assign a consistent enterprise classification.  
C. Accept the highest classification found on any tape and apply that label to the entire data set to avoid under-protection.  
D. Hash every file on the tapes and store the hashes as metadata so customers can later prove integrity regardless of classification.  
Correct Answer: B  
Explanation: A consistent, enterprise-wide classification scheme is the prerequisite for applying appropriate controls in the cloud (Domain 2). Option B builds the inventory and mapping needed to satisfy GDPR (lawful basis, data-minimization) and PCI DSS (scope-reduction). A only perpetuates inconsistent labels and does not address scope. C over-protects, driving unnecessary cost and complexity. D provides integrity assurance but does nothing for classification or jurisdictional requirements.

Q2. A SaaS company that stores EU customer health records in Ireland has just merged with a U.S. firm whose data warehouse is located in Ohio. The combined company wants to run unified analytics across both data sets. The EU data were originally collected under explicit consent and classified as “Special Category” under GDPR. The U.S. data are classified as “Sensitive” under HIPAA. A single data lake is proposed in Ohio. Which classification approach BEST supports lawful cross-border processing?  
A. Re-label all EU data as “Sensitive” to match HIPAA and transfer under Standard Contractual Clauses.  
B. Maintain the “Special Category” label, tag the U.S. data as “Restricted,” and apply the stricter GDPR controls to the entire lake.  
C. Create a new label “Merger Critical,” apply it to both data sets, and rely on the merger as the lawful basis for transfer.  
D. Anonymize the EU data in Ireland first, then ship to Ohio; classification is no longer required.  
Correct Answer: B  
Explanation: When data sets with different regulatory origins are combined, the highest/minimum common denominator rule applies. Option B keeps the stricter GDPR “Special Category” controls, thereby satisfying both GDPR transfer rules and HIPAA. A ignores GDPR’s prohibition on re-purposing consent-based data. C invents an arbitrary label without legal basis. D may destroy analytic value and still requires classification decisions for the anonymization residual risk.

Q3. A manufacturer uses bar-code labels on physical media that store firmware signing keys classified as “Top Secret.” During a third-party logistics move, several crates arrived with labels missing and the media still inside. A subsequent audit cannot determine whether the media were lost, stolen, or merely mis-labeled. Which control failure MOST contributed to this asset-tracking gap?  
A. Lack of environmental monitoring sensors in the truck.  
B. Absence of cryptographic encryption on the firmware files.  
C. Inadequate physical asset labeling and inventory linkage.  
D. Failure to use tamper-evident packaging inside the crates.  
Correct Answer: C  
Explanation: Domain 2 stresses labeling and inventory as the foundation of asset tracking. Missing labels meant the media could not be reconciled with the inventory database. A is environmental, not asset tracking. B protects confidentiality but does not help track presence. D would show tampering but still requires a label to know what asset is missing.

Q4. A FinTech startup developed a mobile wallet that stores truncated PANs (last four digits) and tokens on the device. The security team needs to classify these data for the mobile-app secure-development guide. Which classification is MOST appropriate?  
A. Public – because truncated PANs are not regulated cardholder data.  
B. Internal – because tokens have no exploitable value.  
C. Confidential – because tokens can be replayed if compromised in combination with other metadata.  
D. Restricted – because any card-related data must retain the same classification as the full PAN.  
Correct Answer: C  
Explanation: Even truncated PANs plus tokens can be replayed in certain contexts (PCI DSS SAQ guidance). “Confidential” reflects the need for encryption at rest and key protection. A ignores residual risk. B underestimates token replay. D over-classifies; full PAN is “Restricted,” but tokens are not PANs.

Q5. A government agency is disposing of 2,000 legacy hard drives that previously held “Secret” data. Declassification procedures require a two-step process: cryptographic erasure followed by physical destruction. An intern proposes using the agency’s existing solid-state destruction standard (20 mm particle size) for all media. Which concern MUST be addressed first?  
A. Verify that the cryptographic erasure keys are escrowed for forensic needs.  
B. Confirm that 20 mm particles meet the agency’s data-type-specific destruction standard for magnetic drives.  
C. Ensure that destruction is recorded in the asset-tracking system with video evidence.  
D. Check whether the drives support hardware-level cryptographic erasure.  
Correct Answer: B  
Explanation: Asset Security requires that destruction methods align with media type and classification. A 20 mm particle requirement for SSDs may be overkill or insufficient for magnetic drives; the standard must be reviewed. A is irrelevant—keys should be destroyed, not escrowed. C is secondary documentation. D is valid but later in the workflow.

Q6. A cloud security architect must label virtual machine snapshots that contain database dumps. The dumps include hashed passwords (bcrypt) and customer purchase histories. The company policy states that any data that can lead to financial fraud if disclosed must be labeled “Confidential.” Which label is correct and why?  
A. Internal – because passwords are hashed.  
B. Confidential – because purchase histories plus hashed passwords enable fraud.  
C. Restricted – because any authentication data must always be Restricted.  
D. Private – because only natural persons are affected.  
Correct Answer: B  
Explanation: The policy trigger is “can lead to financial fraud.” Even with bcrypt, cracked passwords plus purchase history facilitate account-takeover fraud. The label must therefore be “Confidential.” A underestimates offline cracking. C overstates; policy does not mandate Restricted for hashed passwords. D is not among the company’s four-tier scheme.

Q7. A security analyst is building a data-life-cycle diagram for “Proprietary” CAD files shared with external fabrication partners. The diagram must show how classification changes at each phase. Which statement is TRUE?  
A. Classification drops to “Internal” once the file leaves the organization’s network perimeter.  
B. Classification remains “Proprietary” throughout the life cycle regardless of location or format.  
C. Classification can be lowered to “External” if the file is converted to a read-only format.  
D. Classification is temporarily elevated to “Restricted” during transit over the internet.  
Correct Answer: B  
Explanation: Classification is tied to the asset’s value and legal protection, not location or format. A, C, and D erroneously tie classification to network location or transport encryption level.

Q8. During an M&A due-diligence review, the target company provides a spreadsheet listing 5,000 software licenses with their “Asset Criticality” ratings (1–5). The spreadsheet is marked “Internal Use Only.” The acquiring company’s policy equates criticality 4–5 assets to “Confidential” classification. Which step MUST the acquiring CISO take first?  
A. Accept the target’s ratings and apply “Confidential” labels to all 4–5 assets.  
B. Re-audit a sample of the licenses to validate both existence and criticality before re-labeling.  
D. Label the spreadsheet itself as “Confidential” because it contains aggregation risk.  
C. Immediately apply DRM to the spreadsheet to prevent leakage.  
Correct Answer: B  
Explanation: Asset classification must be based on verified attributes. Re-auditing ensures that the criticality (and therefore classification) is accurate. A trusts unverified data. D and C are secondary; the data must first be validated.

Q9. A hospital stores MRI scans in a PACS that automatically tags each file with patient ID, procedure code, and radiologist notes. The security team wants to apply metadata-driven access control. Which metadata element is MOST reliable for assigning GDPR “Special Category” classification automatically?  
A. Procedure code indicating “brain MRI.”  
B. Patient ID starting with numeric digits.  
C. File size larger than 50 MB.  
D. Radiologist notes containing the word “normal.”  
Correct Answer: A  
Explanation: Procedure codes (e.g., ICD-10) reliably indicate health information, triggering Special Category status. B is just an identifier format. C is unrelated to category. D is subjective and may be absent.

Q10. A global retailer runs nightly ETL jobs that copy POS transaction logs from 500 stores to a regional data mart. Logs include full PANs, which are immediately tokenized upon arrival, but the original file is left on the store server for 30 days for troubleshooting. The CISO needs to classify the local log files. Which classification and justification pair is CORRECT?  
A. Internal – because the PANs are eventually tokenized elsewhere.  
B. Restricted – because the file contains full PANs and is stored in 500 remote locations with limited physical security.  
C. Confidential – because only the security team has SSH access to the servers.  
D. Private – because no employee data are present.  
Correct Answer: B  
Explanation: PCI DSS considers any system storing full PANs as in-scope for all PCI requirements; therefore the asset must receive the highest classification (“Restricted”) to ensure strong encryption, access control, and destruction. A ignores the 30-day window of exposure. C confuses technical access with regulatory scope. D introduces an undefined label.
Q1. A multinational retailer is preparing to migrate its on-premise customer-analytics platform to a public-cloud SaaS offering. The dataset contains 12 years of purchase history, loyalty-card numbers, and full credit-card PANs for 38 million shoppers. Which action BEST reduces the organization’s data-privacy liability before the migration?  
A. Hash the PANs with SHA-256 and store the salt in the same cloud tenant.  
B. Tokenize the PANs via an on-premise token vault and send only tokens to the cloud.  
C. Encrypt the entire database with AES-256 and keep the cloud provider’s key in its HSM.  
D. Replace each PAN with the last four digits and delete the original file from on-premise storage.  

Correct Answer: B  
Explanation: Tokenization (B) replaces sensitive data with non-sensitive tokens and keeps the original values in an on-premise vault, eliminating the need to store regulated PAN data in the cloud and therefore reducing privacy liability. Hashing with salt in the same tenant (A) still leaves recoverable PANs if the salt is compromised. Full-database encryption (C) protects data at rest but does not remove the regulated data from the cloud provider’s custody. Truncating to the last four digits (D) destroys data utility for analytics and is not a reversible or complete protection strategy.

Q2. A hospital’s research department wants to share de-identified MRI scans with an AI start-up. The DICOM files embed patient name, DOB, and exam date in the metadata. Which control provides the MOST reliable assurance that the data cannot be re-identified?  
A. Remove metadata fields and apply a one-way hash to each image.  
B. Strip direct identifiers and add a 6-month date jitter to exam timestamps.  
C. Replace names with pseudonyms and encrypt the files with the start-up’s public key.  
D. Remove all identifiers and down-sample images from 512×512 to 64×64 pixels.  

Correct Answer: B  
Explanation: Option B achieves “safe-harbor” de-identification under HIPAA by removing direct identifiers and obfuscating quasi-identifiers such as precise dates. Hashing the image (A) does nothing for metadata identifiers. Encrypting (C) protects confidentiality but does not de-identify the data. Down-sampling (D) degrades clinical utility and still leaves metadata untouched.

Q3. A cloud-first company tags every S3 bucket with “Confidential,” “Internal,” or “Public.” During an audit, the CISO discovers that 18% of objects have conflicting tags within the same bucket. What is the PRIMARY risk created by this inconsistency?  
A. Data owners cannot be held accountable for breaches.  
B. Access-control or DLP rules may be applied incorrectly.  
C. Encryption-key rotation schedules will fail to execute.  
D. The company will exceed its data-retention limit.  

Correct Answer: B  
Explanation: Inconsistent classification tags cause downstream technical controls (IAM policies, DLP, CASB) to apply the wrong enforcement actions (B). Ownership (A) is a governance issue but not the primary technical risk. Key rotation (C) and retention (D) are unrelated to object-level tagging conflicts.

Q4. A manufacturer stores CAD drawings for military-grade components in an offline, encrypted tape archive. The security policy states drawings must be destroyed 7 years after last manufacture. Which process BEST ensures reliable destruction of the encrypted data?  
A. Delete the encryption keys and record the key-deletion event in the CMDB.  
B. Overwrite the tapes with random data and ship them to a recycler.  
C. Degauss the tapes and retain certificates of destruction.  
D. Let the tapes expire in the vault because encryption makes the data unusable.  

Correct Answer: C  
Explanation: Physical destruction (degaussing) plus documented evidence (C) is the strongest assurance for sensitive offline media. Deleting keys (A) is acceptable for online crypto-shredding but does not meet defense-contractor requirements for physical media. Overwriting (B) is ineffective against modern high-coercivity tape. Relying on encryption alone (D) leaves residual data that may be decrypted in the future.

Q5. A social-media firm classifies user-generated videos as “Public,” “Followers-Only,” or “Private.” The firm now introduces AI-based facial recognition that creates biometric templates. How should the templates be classified?  
A. At the same level as the source video.  
B. Always “Restricted” regardless of the video’s classification.  
C. One level higher than the source video.  
D. As “Internal” unless the video is already “Restricted.”  

Correct Answer: B  
Explanation: Biometric templates are inherently sensitive and require the highest default classification (“Restricted”) because they can be used to identify individuals across any context, unlike the original video content. Matching them to the source video’s level (A) or only one level higher (C) underestimates the risk. “Internal” (D) is insufficient for biometric data.

Q6. A bank is disposing of 1,000 SATA drives that contained transaction logs governed by PCI DSS and national banking regulations. Which destruction method provides the GREATEST assurance while minimizing environmental impact?  
A. Cryptographic erasure verified by sampling 10% of the drives.  
B. NSA-approved degauss followed by shredding to 6 mm particles.  
C. ATA secure-erase command with a signed certificate for each drive.  
D. Shred drives to 12 mm particles and send shredded material to an e-waste recycler.  

Correct Answer: B  
Explanation: Dual-step destruction (degauss + 6 mm shred) (B) meets both PCI DSS and most national banking standards for top-secret data, and the shredded material can still be recycled. Cryptographic erasure (A) is acceptable only if full-disk encryption was always enabled, which is not stated. ATA secure-erase (C) is reversible with forensic tools if the firmware is compromised. Shredding alone to 12 mm (D) leaves larger recoverable pieces and is weaker than 6 mm.

Q7. A SaaS vendor offers “data residency options” for EU customers: (1) store in Frankfurt, (2) store in Paris, or (3) allow the vendor to optimize between EU and US data centers. The customer’s DLP policy forbids personal data from leaving the EEA. Which attribute of the data catalog must be updated FIRST to enforce this policy automatically?  
A. Jurisdictional sovereignty tag  
B. Record-of-processing activity (ROPA)  
C. Asset owner field  
D. Criticality rating  

Correct Answer: A  
Explanation: A jurisdictional sovereignty tag (A) directly labels data as “EEA-only,” allowing CASB/DLP tools to block cross-border transfers. ROPA (B) is a compliance register, not an enforceable technical tag. Owner (C) and criticality (D) do not drive geographic enforcement rules.

Q8. A startup uses object storage with lifecycle policies that move data to cheaper tiers after 30 days and delete it after 1 year. Pen-testing reports warn that snapshots of deleted volumes remain in the cloud provider’s backup system for an additional 35 days. Which policy element isMISSING?  
A. Data retention schedule  
B. Secure destruction policy  
C. Version-control baseline  
D. Encryption-key escrow  

Correct Answer: B  
Explanation: The secure destruction policy (B) must explicitly cover provider-side backups and snapshots; otherwise data remains recoverable. Retention schedule (A) already exists (1 year). Version-control baseline (C) and key escrow (D) are unrelated to residual snapshots.

Q9. A university research team plans to release an open dataset of 50,000 student Wi-Fi connection logs. The logs contain hashed MAC addresses, building names, and 5-minute-interval timestamps. The IRB requests a re-identification risk assessment. Which finding presents the HIGHEST residual risk?  
A. Hash algorithm is SHA-1.  
B. Timestamps are precise to 5 minutes.  
C. Building names are included.  
D. Dataset covers only one semester.  

Correct Answer: A  
Explanation: SHA-1 of MAC addresses (A) can be reversed by brute-forcing the 48-bit space, making re-identification trivial. Precise timestamps (B) and building names (C) increase risk but only if the identifier (MAC) can be recovered. A single semester (D) actually reduces risk by limiting the correlation window.

Q10. A company’s data-classification policy states that “Confidential” data must be encrypted with FIPS 140-2 validated modules. A new HR SaaS vendor claims AES-256 encryption but is only FIPS 140-2 “Level 1” validated. The CISO is concerned about key storage. What should be the CISO’s PRIMARY objection?  
A. Level 1 does not require hardware-based key storage.  
B. AES-256 is not approved for “Confidential” data.  
C. SaaS providers cannot be FIPS 140-2 validated.  
D. Level 1 allows only 128-bit keys.  

Correct Answer: A  
Explanation: FIPS 140-2 Level 1 (A) provides cryptographic-module validation but does not mandate physical protection or hardware key storage, leaving keys potentially exposed in software. AES-256 is FIPS-approved (B is false). SaaS vendors can use validated modules (C is false). Level 1 imposes no key-length restriction (D is false).
Q1. A multinational online-learning company has deployed a cloud-first data-classification program. During a recent acquisition, the security team discovers that the acquired subsidiary has 8 TB of unstructured “legacy” files on on-premise Windows servers. The CIO wants the data moved to the company’s S3-compatible object store within 30 days, but the subsidiary has never tagged anything more specific than “Confidential / Public.” Which action BEST satisfies both the timetable and the parent company’s mandatory three-level scheme (Public, Internal, Restricted)?  
A. Hash every file, move it immediately to the cloud, then apply machine-learning classification once the transfer is complete.  
B. Run a scripted scan that reads each file’s header, keywords, and extension; auto-apply the highest-matched label; migrate only after Legal signs off.  
C. Quarantine the servers, restore the last six months to a sandbox, let data owners manually label that subset, and delete everything else.  
D. Migrate the entire 8 TB as “Restricted,” force business units to down-grade labels in the cloud within 90 days, and block all access until relabeled.  

Correct Answer: B  
Explanation: Option B is the only choice that performs at least a cursory automated classification based on content indicators before data crosses the trust boundary, satisfying the “classify before you move” principle. A moves data unclassified, violating the policy. C destroys potentially valuable records and still leaves 90 % of the data unlabeled. D over-classifies everything, creating a denial-of-service for users and does not meet the 30-day goal because business units will be swamped with relabeling requests.

Q2. A hospital maintains an enterprise data-lake that contains both de-identified research data and raw PHI. A researcher requests a copy of “all stroke-patient data for the last five years” on portable encrypted SSDs so the analytics can be performed on an air-gapped cluster. Which control is MOST important to prevent an unauthorized disclosure that still satisfies the research objective?  
A. Require the researcher to sign an NDA and return the drives within 30 days.  
B. Export only the minimum data elements that have been tokenized or hashed.  
C. Use FIPS-140-3 level-3 SSDs with hardware-based encryption.  
D. Log the serial numbers of the drives and store them in a sealed envelope under dual control.  

Correct Answer: B  
Explanation: Tokenization/hashing is the only option that fundamentally reduces the sensitivity of the data set while preserving analytic utility. An NDA (A) is administrative and does not prevent misuse. Strong encryption (C) protects only while the drives are at rest; once mounted on the air-gapped cluster the clear text is exposed. Logging serial numbers (D) is detective, not preventive.

Q3. A SaaS provider gives customers the option to bring their own encryption keys (BYOK) for object storage. A financial-services customer wants “complete custody” so that the SaaS vendor can never access the data, even under subpoena. Which BYOK architecture BEST achieves this goal?  
A. Customer uploads a 256-bit symmetric key sealed inside the vendor’s public-key certificate; vendor stores the blob in a dedicated HSM.  
B. Vendor proxies all object requests to an on-premise customer HSM that performs encryption in real time but caches the ciphertext key in vendor RAM for performance.  
C. Customer operates an offline KMS; vendor receives a wrapped key at object-upload time and unwraps it inside the vendor’s cloud HSM for every operation.  
D. Customer retains the key in its own KMS; vendor passes a request token to customer KMS, encrypted object is streamed directly from browser to customer KMS, and vendor never sees the plaintext key.  

Correct Answer: D  
Explanation: In D the SaaS vendor never possesses the plaintext key, achieving true custodial separation. A and C still give the vendor transient access to the unwrapped key. B caches the key in vendor memory, exposing it to memory dumps or lawful intercept.

Q4. A manufacturer tags every CAD file with “Confidential” in the DLP system, but engineers routinely upload files to a partner extranet that is labeled “Internal.” End-users see no pop-up warnings and incidents are not logged. Which missing control is the PRIMARY cause of this policy violation?  
A. Data ownership assignments are not documented in the asset inventory.  
B. The DLP tool is not integrated with the classification metadata repository.  
C. Role-based access control (RBAC) is missing from the extranet.  
D. The retention schedule for CAD files has not been approved by Legal.  

Correct Answer: B  
Explanation: If the DLP engine cannot read the file’s classification label it cannot enforce the “Confidential ≠ Internal” rule. A, C, and D are good practices but are not the root cause of the silent failure.

Q5. A company is disposing of 2000 used SSDs from R&D laptops that contained both unclassified prototype code and export-controlled encryption libraries. The security policy states “crypto-shred or physically destroy media containing Restricted data.” Which method BEST meets the policy while allowing maximum resale value for the hardware?  
A. Apply the vendor’s secure-erase command that resets the internal encryption keys, then sell the drives.  
B. Degauss with a 2-Tesla coil, then shred the PCB.  
C. Overwrite every logical block with 0x00, followed by 0xFF, followed by random pattern.  
D. Remove and incinerate only the NAND chips; sell the remaining aluminum housing.  

Correct Answer: A  
Explanation: Crypto-shredding (changing the media-encryption key) instantly renders all previous data unrecoverable on modern self-encrypting drives and preserves resale value. Degaussing (B) is ineffective on SSDs and destroys the drive. Multi-pass overwrite (C) is unreliable due to over-provisioning and wear-leveling. D is overkill and still leaves no resale value.

Q6. A cloud security team wants to enforce “data cannot leave the EU” for any VM that processes personal data. Which cloud-native control MOST reliably prevents an operator from accidentally migrating the workload to another region?  
A. Tag the subscription with “EU-only” and create an Azure Policy (or AWS SCP) that denies VM creation outside designated EU regions.  
B. Enable region lock at the hypervisor level with a hardware TPM seal.  
C. Require two-person approval for any console login that selects a non-EU region.  
D. Configure the SIEM to alert when a VM is launched outside the EU and auto-terminate after 15 minutes.  

Correct Answer: A  
Explanation: Policy/SCP is preventive, deterministic, and enforced by the control plane before the resource is created. B is not supported by major public clouds. C is administrative and can be bypassed. D is detective and allows a 15-minute exposure window.

Q7. A streaming service stores customer viewing histories in a single Amazon S3 bucket. The data is classified “Internal,” but an analytics team needs to share it with an external marketing agency for sentiment analysis. The security architect recommends creating a second bucket that contains only pseudonymous IDs and dropping any row with fewer than 50 viewers to prevent re-identification. Which privacy principle is PRIMARILY being applied?  
A. Data minimization  
B. Consent revocation  
C. Differential privacy  
D. K-anonymity  

Correct Answer: D  
Explanation: Ensuring each record relates to at least k=50 individuals is the textbook definition of k-anonymity. Data minimization (A) would mean not sharing at all. Consent (B) is unrelated to the technical control. Differential privacy (C) would require mathematical noise, not suppression.

Q8. A security manager is building an asset-inventory database. Which attribute MOST increases the ACCURACY of data-classification assignments over time?  
A. Including the name and email of the employee who created the file  
B. Storing the SHA-256 hash of every file to detect bit-rot  
C. Linking each asset to a formally appointed data owner in the HR system  
D. Recording the purchase price and depreciation schedule  

Correct Answer: C  
Explanation: A live link to an accountable data owner ensures classification can be reviewed when business context changes. Creator name (A) becomes stale after org moves. Hash (B) is integrity, not classification accuracy. Purchase price (D) is financial, not security, metadata.

Q9. A startup uses a single Git repository that contains both open-source libraries and proprietary algorithms. The CI/CD pipeline automatically labels the entire repo “Public” because portions are open-source. A developer accidentally pushes hard-coded cloud credentials that remain in the history. Which control would have BEST prevented the credential leak from being public?  
A. Enforce separation of repos: public code in a public repo, proprietary code in a private repo.  
B. Require code owners to digitally sign every commit.  
C. Run a pre-receive hook that searches for high-entropy strings and blocks the push.  
D. Enable immutable backups of the repository so credentials can be expunged later.  

Correct Answer: C  
Explanation: Blocking the push at the server side (pre-receive hook) stops the exposure before it becomes part of the history. A would reduce risk but still allows mistakes in the private repo. B does not detect secrets. D is after-the-fact remediation.

Q10. A government agency is retiring a Top-Secret relational database. The media will be donated to a school after sanitization. According to current NIST 800-88 rev.1, which action is REQUIRED before the drives can leave the facility?  
A. Perform a single-pass overwrite verified by sampling 10 % of the drives.  
B. Execute a full disk manufacturer secure-erase and document the results.  
C. Physically shred the drives to 5-mm particles under witnessed chain-of-custody.  
D. Cryptographically erase the volume keys stored in the RAID controller NVRAM.  

Correct Answer: C  
Explanation: For Top-Secret data, NIST 800-88 requires “destroy” (shredding, incineration, etc.) regardless of any logical sanitization method. Overwrite (A) and secure-erase (B) are only acceptable for lower classifications. D does not affect the user data on the platters.
Q1. A multinational retailer is preparing to migrate its on-premise customer-analytics database to a PaaS offering. The dataset contains 30 million customer records with credit-card tokens, geolocation histories and loyalty-point balances. Regulations in three of the countries where the retailer operates require that “personal data must remain within the jurisdiction where it was collected unless the data subject’s explicit consent is on file.” Which of the following is the MOST important asset-security activity to perform before contract signature with the cloud vendor?  
A. Map every data field to the country of collection and build a data-flow diagram that shows which logical servers in the provider’s region will store each field.  
B. Require the vendor to supply a SOC 2 Type II report and place the findings into the corporate risk register.  
C. Encrypt all fields with AES-256 and keep the keys on-premise so that data is unreadable outside the home country.  
D. Run a vulnerability scan against the provider’s API endpoints to confirm that CVSS scores are below 4.0.  
Correct Answer: A  
Explanation: Jurisdiction-based data-locality requirements are essentially data-classification and location questions. Until you know exactly which data elements belong to which country (and can prove where they will reside, be processed and backed up) you cannot determine compliance. Option A is the only choice that creates the evidence needed to decide whether the PaaS architecture itself is lawful. B is useful but does not prove data-location compliance. C does not satisfy most data-locality laws because encrypted personal data is still considered “exported.” D is unrelated to residency obligations.

Q2. A hospital’s medical-device project team is designing a portable ultrasound that will store 24 hours of fetal-monitor strips on an internal SSD. The chief privacy officer asks security to “tag the data so we can prove chain-of-custody if the device is lost.” Which security control BEST satisfies the request?  
A. Digitally sign each monitor strip at creation and append the signature to the file header.  
B. Install a TPM in the device and bind the SSD to the TPM so it cannot be removed.  
C. Create a unique asset tag with bar-code and require clinicians to scan the device in and out.  
D. Write the device serial number into every file name so files can be traced to the unit.  
Correct Answer: A  
Explanation: A digital signature provides non-repudiation and integrity evidence, allowing the hospital to prove the strip has not been altered and to trace it back to the originating device (via the certificate). B is a hardware protection control, not chain-of-custody evidence. C tracks the physical device, not the data. D is trivial to spoof and offers no integrity protection.

Q3. A SaaS provider offers “secure multi-tenant object storage.” During due-diligence the vendor states that each object is assigned “a unique, random 160-bit identifier and is encrypted with a separate key.” Which question BEST validates whether the vendor’s architecture provides adequate asset isolation?  
A. “Are keys deterministically derived from the 160-bit object identifier, and if so can tenants predict or brute-force another tenant’s key?”  
B. “Is the 160-bit identifier hashed with SHA-1 before storage?”  
C. “Do you replicate objects to at least three geographically separated data centers?”  
D. “Do you use TLS 1.3 for data in transit?”  
Correct Answer: A  
Explanation: If keys are derived from the object ID, an attacker can enumerate identifiers and regenerate keys, breaking tenant isolation. Option A directly tests the confidentiality goal for co-mingled assets. B is irrelevant to isolation. C addresses availability, not isolation. D addresses transport security, not storage segregation.

Q4. A software company has adopted a “label-based” data-classification scheme. Source code is labeled “Internal,” but a developer recently checked in a file containing hard-coded AWS keys. The security team wants to prevent recurrence. Which action BEST enforces the principle that data should be handled according to its true (not declared) classification?  
A. Deploy a DLP scanner in the CI/CD pipeline that re-classifies files based on regex matches for cloud keys and blocks the commit.  
B. Change the default repository ACL so only senior developers can commit to any branch.  
C. Require two-person code review for every commit labeled “Internal.”  
D. Move all repos to a private network segment and require VPN plus MFA for cloning.  
Correct Answer: A  
Explanation: The real classification of the file is “Confidential/High” because of the embedded credentials. A content-aware control that re-evaluates and blocks on true classification closes the gap. B and D are generic access controls that do not address mis-classified data. C relies on human detection, which already failed.

Q5. A manufacturing firm runs a legacy MRP system that stores 15-year-old supplier contracts on optical WORM media. New privacy regulations require that “personal data be deleted once the business purpose expires.” The compliance team asks security to “ensure erasure.” Which statement is MOST accurate?  
A. Optical WORM cannot be overwritten; therefore physical destruction is the only acceptable sanitization method.  
B. Because the data is on WORM, no erasure is possible and the firm must relocate the media to a country with weaker privacy laws.  
C. Overwriting the media three times with random data meets regulatory requirements.  
D. Degaussing the optical platters will render the data unreadable.  
Correct Answer: A  
Explanation: Write-Once-Read-Many media is, by definition, non-erasable. Regulatory “right to be forgotten” still applies, so the only compliant path is destruction (shredding/incineration). B is illegal. C is technically impossible. D is ineffective because optical media is not magnetic.

Q6. A cloud-first policy mandates that all “non-critical” data older than one year be moved to an object-storage archive to cut cost. The data-classification policy labels such data “Internal—Low Impact.” Which residual risk remains AFTER the migration if the cloud region uses encrypted-at-rest storage but multi-tenant hardware?  
A. Data remanence on drives that are later repurposed for other tenants.  
B. Crypto-shredding is impossible because the cloud provider holds the KEKs.  
C. Cross-region replication could increase the probability of nation-state subpoena.  
D. Integrity loss due to bit rot in the object store.  
Correct Answer: A  
Explanation: Low-impact data is still company data; if disks are not sanitized between tenants (common in large-scale cloud) remanence is possible. B is incorrect—you can still delete customer-managed keys to render ciphertext unrecoverable (crypto-shredding). C is a geopolitical risk, not an asset-security remanence issue. D is an availability/integrity risk, not confidentiality.

Q7. A financial-exchange company keeps a “golden” configuration repository for all trading algorithms. Version-control metadata shows classification “Public” because the repo is labeled open-source, but embedded API keys make the actual content “Restricted.” Which control failure allowed the discrepancy?  
A. Lack of mandatory metadata review during code promotion.  
B. Absence of role-based access control on the repo.  
C. Failure to implement pull-request approvals.  
D. Insecure direct object references in the web-GUI.  
Correct Answer: A  
Explanation: Classification metadata should be validated whenever content changes. Because the promotion process did not re-check the true sensitivity, keys remained in a “Public” repo. B, C and D are generic access or coding issues; only A addresses the asset-classification gap.

Q8. A university research lab shares genomic data sets with external partners under strict data-use agreements that require deletion within 90 days. Partners receive the data on encrypted USB 3.2 SSDs. Which step BEST demonstrates compliance with the deletion requirement?  
A. Include a secure erase utility on the drive and require partners to run it, returning a digitally signed attestation with the drive’s serial number and timestamp.  
B. Use drives with hardware-based full-disk encryption and change the passphrase after 90 days.  
C. Physically shred the drives at the university before shipment so partners cannot copy the data.  
D. Require partners to store the drives in a locked safe and mail them back after 90 days.  
Correct Answer: A  
Explanation: A gives both technical assurance (secure erase) and evidentiary proof (signed attestation). B leaves ciphertext intact; keys might be recovered. C contradicts the business need to share data. D does not guarantee deletion—drives could be lost or copied in transit.

Q9. A company is disposing of 2000 used laptops from a closed facility. The data-classification matrix shows that some devices processed “Confidential—Restricted Trade Secret” while others processed only “Public” marketing material. Inventory logs are incomplete. Which approach BEST aligns with due-care for asset disposal?  
A. Treat all 2000 laptops as if they contain the highest classification and sanitize or destroy them uniformly.  
B. Spot-check 5 % of laptops with forensics; if no restricted data is found, recycle the rest without sanitization.  
C. Boot each laptop and run a file-scan for keywords such as “secret,” sanitizing only those that match.  
D. Remove and shred only the hard drives of laptops that were assigned to R&D staff.  
Correct Answer: A  
Explanation: When classification is unknown, the secure default is the highest label—this avoids under-sanitization. B provides weak statistical assurance. C misses deleted or hidden data. D relies on incomplete assignment records.

Q10. A global social-media firm is implementing a “privacy-by-design” feature that lets users mark posts as “ephemeral—delete after 24 hours.” The firm operates a geo-distributed Cassandra cluster with asynchronous replication that can delay deletes by several hours. Which control BEST minimizes the risk of data-asset remnants in remote nodes?  
A. Use a customer-managed key per post and delete the key after 24 hours to achieve crypto-shredding.  
B. Set TTL=24h on the column and rely on Cassandra’s built-in compaction to delete tombstones.  
C. Write a manual repair job that issues DELETE statements to every replica and log the outcome.  
D. Disable cross-region replication for ephemeral posts.  
Correct Answer: A  
Explanation: Crypto-shredding is instantaneous and global; once the key is destroyed, data on any lagging replica becomes unrecoverable, meeting the user expectation. B and C still leave windows where replicas contain readable data. D hurts availability and does not address existing replicas.
Q1. A multinational retailer is preparing to migrate its on-premise customer-analytics platform to a hybrid cloud. The project manager has produced a spreadsheet listing every data element the company stores (name, address, credit-card number, loyalty points, click-stream, in-store CCTV footage, employee ID, etc.) and has asked the security team to classify each row so that appropriate protection levels can be budgeted. Which of the following is the MOST important next step before classification can be performed?  
A. Encrypt every column that contains personally identifiable information (PII).  
B. Map each data element to the applicable legal or regulatory jurisdiction(s) in which it is processed.  
C. Assign the “Confidential” label to any field that is unique to an individual customer.  
D. Purchase a data-loss-prevention (DLP) appliance and point it at the on-premise database.  
Correct Answer: B  
Explanation: You cannot select an appropriate confidentiality label or protection level until you know which laws (PCI-DSS, GDPR, CCPA, LGPD, etc.) apply; those statutes dictate minimum required controls. Encrypting or labeling data without this context (A, C) risks under- or over-protection. Buying a tool (D) is premature before the classification scheme is defined.

Q2. A hospital keeps electronic health records (EHR) on a clustered database that replicates synchronously to a hot site 200 km away. After a recent ransomware attack, the CIO wants to add an immutable copy that cannot be changed for seven years. Which control BEST satisfies the requirement while preserving patient-data availability?  
A. Write-once-read-many (WORM) tape vaulted off-site.  
B. Blockchain ledger anchored to the hospital’s production EHR.  
C. Snapshots stored on the same SAN as the primary database.  
D. Cloud object storage with object-lock (WORM) and cross-region replication.  
Correct Answer: D  
Explanation: Cloud object-lock provides hardware-grade immutability plus geographic separation, meeting both retention and availability goals. WORM tape (A) is immutable but restores are slow, hurting availability. Blockchain (B) is immutable but introduces complexity and latency unsuitable for primary EHR queries. Local snapshots (C) are not immutable—ransomware can delete them.

Q3. A software vendor ships appliance servers to customers pre-loaded with licensed machine-learning models. The vendor’s legal department is worried that competitors could reverse-engineer the models if disks are removed. Which data-protection technique addresses this threat at the LOWEST operational cost?  
A. Full-disk encryption with TPM-backed key sealing.  
B. Double encryption—file-level inside full-disk encryption.  
C. Hardware security module (HSM) in every appliance.  
D. Tokenize the model weights and store them in the cloud.  
Correct Answer: A  
Explanation: TPM-sealed full-disk encryption denies access when the disk is removed, is transparent to the OS, and adds no cloud or HSM cost. Double encryption (B) is overkill and increases support burden. HSMs (C) are expensive and unnecessary when keys can be sealed locally. Tokenization (D) breaks the on-prem licensing model and raises latency.

Q4. A financial-services firm labels data “Public,” “Internal,” “Confidential,” and “Restricted.” The CISO discovers that trading algorithms classified “Restricted” are stored in the same SAN tier as “Internal” marketing videos. What is the PRIMARY risk?  
A. Inadequate media-sanitization controls when disks are retired.  
B. Over-exposure to loss of availability due to co-mingled backups.  
C. Insufficient granularity in access-control lists (ACLs) on the SAN.  
D. Inability to apply cost-effective, tiered protective controls.  
Correct Answer: D  
Explanation: When high- and low-value assets share infrastructure, the organization must protect everything to the highest level or accept under-protection; either choice is inefficient. The scenario does not mention disposal (A), availability (B), or ACL detail (C)—the core issue is misalignment of controls to classification.

Q5. A city government is disposing of 1,000 laptops formerly used by the police department. Some laptops processed CJIS (criminal-justice) data, some processed only administrative spreadsheets, but asset tags have worn off and records are incomplete. Which sanitization method BEST balances cost, compliance, and risk?  
A. Degauss every drive and send the laptops to auction as scrap metal.  
B. Boot each laptop with a NIST 800-88 tool that issues a cryptographic erase followed by a full overwrite, then spot-verify 10 %.  
C. Remove all drives and shred them; donate the chassis to a local school.  
D. Perform a single pass overwrite and release the laptops to the public.  
Correct Answer: C  
Explanation: Because you cannot confirm which laptops held sensitive CJIS data, the only compliant, low-risk option is physical destruction of the storage medium. Degaussing (A) ruins the entire laptop, wasting value. Cryptographic erase (B) is valid only if keys are provably destroyed and media is not expected to leave organizational control—here they are. Single pass (D) is insufficient for potential CJIS data.

Q6. A cloud-first retailer wants to assign data ownership roles for customer payment data stored in a managed PostgreSQL service. Which pairing of role and responsibility is MOST appropriate?  
A. Data Owner: Cloud DBA; Data Custodian: Retailer CISO.  
B. Data Owner: Retailer Head of Payments; Data Custodian: Cloud provider SRE team.  
C. Data Owner: Cloud provider VP of Engineering; Data Custodian: Retailer DBA.  
D. Data Owner: Retailer CFO; Data Custodian: External QSA (Qualified Security Assessor).  
Correct Answer: B  
Explanation: The business unit that profits from and decides on the data is the owner (Head of Payments); the entity that implements day-to-day controls on the infrastructure is the custodian (cloud SRE). A reverses the roles; C gives ownership to the wrong party; D assigns custody to an auditor who does not operate systems.

Q7. A gaming company collects player biometric data (face & gait) for anti-cheating. Regulations require that personal data be deleted once the “processing purpose” ends. The company keeps hashes of the biometric templates because engineers claim “hashes can’t be reversed.” Which statement creates the GREATEST compliance risk?  
A. Hashed biometric data are still considered personal data because they can be used to single out individuals.  
B. Deletion of the original images satisfies the purpose-limitation principle.  
C. Salting the hashes would make the data non-personal.  
D. Hashes reduce storage cost and therefore align with data-minimization.  
Correct Answer: A  
Explanation: Under most modern privacy laws, any identifier that can be linked back to an individual—even irreversible hashes—remains personal data. Therefore retaining the hashes still triggers deletion obligations. B is wrong because templates remain; C is wrong because salting does not anonymize biometrics; D confuses cost with legal minimization.

Q8. An HR start-up stores employee offer letters in AWS S3. Objects are tagged “PII” and encrypted with AWS KMS. A new policy requires that any object untouched for 90 days be moved to Glacier and encrypted with a different key that only the compliance team can use. What AWS feature BEST enforces this automatically?  
A. S3 Lifecycle + S3 Object Ownership + Customer-managed CMK rotation.  
B. S3 Intelligent-Tiering with default encryption.  
C. AWS Config rule with auto-remediation.  
D. S3 Lifecycle + separate KMS CMK owned by compliance.  
Correct Answer: D  
Explanation: S3 Lifecycle can transition based on age; using a separate customer-managed CMK in a compliance account enforces the key-segregation requirement. Intelligent-Tiering (B) does not guarantee Glacier nor key change. Config (C) detects but does not perform transition. CMK rotation (A) rotates the same key, not a different one.

Q9. A manufacturer stamps QR codes on engine parts to track warranty claims. A competitor photographs the codes in transit and clones legitimate parts. The security team recommends changing the identifier format. Which data-security principle is PRIMARILY being violated?  
A. Integrity  
B. Confidentiality  
C. Availability  
D. Non-repudiation  
Correct Answer: B  
Explanation: The QR code data itself is public, but its value relies on secrecy of the issuance process (i.e., the ability to counterfeit depends on knowing valid codes). The violation is disclosure of authentic identifiers—an issue of confidentiality, not integrity (data is unchanged) or availability (service is up).

Q10. During due-diligence of an acquisition, TargetCo provides a data-flow diagram showing that “Highly Confidential” R&D files are stored on the same enterprise-drop-folder as “Public” marketing assets, differentiated only by filename prefix. Which finding poses the GREATEST impact to the acquiring firm?  
A. Single point of failure in the drop-folder server.  
B. Lack of encryption in transit to the folder.  
C. Absence of granular access controls and data segregation.  
D. Inadequate backup of marketing assets.  
Correct Answer: C  
Explanation: Co-mingling highly confidential IP with public data without role-based or folder-level controls means any insider or compromised marketing account can exfiltrate crown-jewel R&D data. Backup (D) and availability (A) are secondary; encryption in transit (B) does not fix the access problem.
Q1. A global retailer is about to migrate 5 PB of customer purchase histories from on-premise NAS to a cloud vendor’s “cool” storage tier. The data includes 20-year-old credit-card magnetic-stripe dumps that were never purged. Which action BEST fulfils asset-security responsibilities before the transfer?  
A. Negotiate a shared-responsibility addendum that forces the cloud provider to delete data older than seven years.  
B. Conduct a data-classification and retention review, then destroy any data that exceeds the PCI DSS retention requirement.  
C. Encrypt the NAS volumes with AES-256 and ship the disks to the cloud vendor for offline ingestion.  
D. Tokenise the credit-card data in place and move everything to the cool tier so the tokens are worthless to attackers.  

Correct Answer: B  
Explanation: PCI DSS explicitly forbids retaining magnetic-stripe data after authorisation; a classification & retention review identifies the illegal data so it can be destroyed, eliminating both regulatory risk and unnecessary cloud cost. A is wrong because the retailer, not the provider, is liable for PCI violations. C only adds a crypto control but does not purge prohibited data. D leaves the prohibited data intact; tokenisation protects PANs but not mag-stripe dumps.

Q2. A hospital’s medical-imaging system creates 200 MB studies that must be readable for 30 years. The CIO worries that bit-rot will render DICOM files useless before the retention period ends. Which control BEST preserves the long-term integrity of these assets?  
A. Store the files on RAID-6 SATA drives and perform a parity scrub every month.  
B. Calculate SHA-256 hashes at ingestion, store the hashes separately, and recompute hashes every two years.  
C. Migrate the data to LTO-9 tape and re-write the entire archive to new tapes every five years.  
D. Compress the studies with lossless FLAC and store three copies in different AWS S3 buckets.  

Correct Answer: B  
Explanation: Periodic hash verification with independent hash storage detects bit-rot early and triggers restoration from backup; it is the most cost-effective integrity control for long-term, rarely accessed data. RAID scrubbing (A) only protects against disk failure, not silent corruption. C is a valid media-renewal tactic but is more expensive and does not verify logical integrity. D adds redundancy but no integrity checking.

Q3. A startup uses a single AWS KMS CMK to encrypt every S3 object in the company. The CISO now requires that each customer’s data be cryptographically isolated so that a compromise of one customer cannot leak another’s data. Which approach BEST meets the requirement with minimal key-management overhead?  
A. Generate a customer-specific data-encryption key (DEK) and encrypt that DEK with the same CMK but a different key alias.  
B. Create a new customer-specific KMS CMK for each tenant and rotate it every 30 days.  
C. Use envelope encryption: create a unique DEK per customer, encrypt the DEK with the existing CMK, and store the encrypted DEK beside the object.  
D. Switch to S3 SSE-S3 and let AWS manage a unique key for every object.  

Correct Answer: C  
Explanation: Envelope encryption with a per-customer DEK provides cryptographic isolation while still using one KMS CMK for master-key management, balancing isolation and overhead. A does not isolate because all DEKs are wrapped under the same CMK; an insider with decrypt rights on the CMK can access every customer. B gives perfect isolation but explodes key-management cost. D delegates control to AWS and does not give per-customer isolation.

Q4. A manufacturer tags every laptop with an RFID label containing the serial number and employee name. An attacker walks through the cafeteria with a high-gain reader and harvests asset data. Which countermeasure BEST reduces the confidentiality risk without impeding legitimate inventory scans?  
A. Replace RFID with barcodes so optical line-of-sight is required.  
B. Store only a random 128-bit asset ID in the RFID tag and keep the mapping table in the CMDB.  
C. Encrypt the serial number with AES-128 and put the ciphertext on the tag.  
D. Shield the cafeteria with a Faraday cage to block unauthorised RF.  

Correct Answer: B  
Explanation: A random surrogate identifier prevents disclosure of business-relevant data while still allowing quick inventory sweeps; the CMDB provides the correlation when needed. A eliminates RF risk but slows down inventory. C leaks metadata length and still exposes ciphertext that can be brute-forced. D is impractical and does not protect assets outside the cafeteria.

Q5. A company’s data-classification policy labels source code as “Internal.” During an audit it is discovered that a repo contains hard-coded API keys to a SaaS billing system. Which is the MOST appropriate next step under an asset-security framework?  
A. Re-classify the repo as “Confidential” and apply access controls commensurate with that level.  
B. Remove the API keys, store them in a secrets manager, and keep the “Internal” label.  
C. Encrypt the repo with AES-256 and leave the keys in place.  
D. Move the repo to an off-line, air-gapped git server.  

Correct Answer: A  
Explanation: The asset now contains credentials whose compromise would affect financial systems, so the classification must be elevated to ensure stricter handling rules. B fixes the exposure but ignores policy: the asset’s sensitivity has permanently increased. C does not address key leakage to anyone with repo access. D is excessive and hampers agile development.

Q6. A cloud SaaS provider offers multi-tenant analytics. Each tenant uploads CSV files that are merged into a single columnar store. A tenant asks for cryptographic proof that its data is deleted when the contract ends. Which technical control BEST provides verifiable data-deletion assurance?  
A. Overwrite the tenant’s objects with random data and provide the overwrite logs.  
B. Issue a legal attestation of deletion signed by the CFO.  
C. Encrypt each tenant’s data with a unique KMS-backed key; destroy the key upon termination.  
D. Store each tenant’s data on separate encrypted EBS volumes and shred the volumes.  

Correct Answer: C  
Explanation: Cryptographic erasure—rendering data undecryptable by destroying the key—is fast, verifiable, and loggable; it scales in shared storage. A is unreliable because columnar stores may relocate blocks. B is procedural, not technical. D is costly and does not guarantee that snapshots or replicas are also shredded.

Q7. A university research lab shares genomic data with external partners under strict data-use agreements that prohibit re-identification attempts. The DLP system alerts that a partner’s IP has downloaded the entire dataset to a laptop. Which is the BEST first response from an asset-security perspective?  
A. Revoke the partner’s VPN certificate and wipe the laptop remotely.  
B. Immediately re-classify the dataset as “Top Secret” and move it to a higher security zone.  
C. Suspend the data-sharing agreement, image the laptop for forensics, and start contractual remediation.  
D. Encrypt the dataset with a new key and re-upload it to the secure file-share.  

Correct Answer: C  
Explanation: The priority is to stop the contractual breach, preserve evidence, and enforce the agreement; suspension and forensics achieve this. A is aggressive and may destroy evidence. B is reactive and does not address the partner’s mis-use. D does nothing about the copy already on the laptop.

Q8. A company runs a bring-your-own-device (BYOD) program. Employees store corporate documents in personal cloud drives. The organisation wants to ensure that when an employee leaves, corporate data can be wiped without touching personal files. Which technology BEST provides this selective-wipe capability?  
A. MDM full-device wipe triggered by HR workflow.  
B. Containerisation app that encrypts corporate data with enterprise-controlled keys.  
C. Encrypted OTA backup followed by remote factory reset.  
D. DLP watermarking that marks every corporate file.  

Correct Answer: B  
Explanation: A container app (e.g., Workspace ONE, Intune managed app) sandboxes corporate data under enterprise keys, allowing selective cryptographic erase or app wipe. MDM full wipe (A) destroys personal data and may be illegal. C still wipes everything. D identifies but cannot delete data.

Q9. A firm is disposing of 1000 used SSDs that once stored “Confidential” HR files. The internal audit team requires a sanitisation method that is verifiable and meets NIST SP 800-88 Revision 1. Which option is the MOST appropriate?  
A. Run a single-pass overwrite with zeros and document the completion time.  
B. Use the SSD vendor’s secure-erase command and retain the command output for audit.  
C. Physically shred the drives to 5 mm particles and keep the destruction certificate.  
D. Encrypt the drives with BitLocker and throw away the recovery keys.  

Correct Answer: C  
Explanation: For Confidential data on SSDs, destruction (shred to < 5 mm) provides the highest assurance because overwrite and vendor secure-erase may be circumvented by spare-area remapping. B is acceptable for lower classifications but not for Confidential without additional verification. A is insufficient on flash media. D is not recognised sanitisation—key loss ≠ data destruction.

Q10. A movie studio classifies pre-release films as “Restricted” and encrypts them with AES-256 in AWS S3. A vendor editor needs access while travelling in China. The studio wants to prevent download but still allow editing. Which control BEST protects the asset against unauthorised local copies?  
A. Generate time-limited, region-restricted presigned URLs valid only in China.  
B. Stream the decrypted film through Amazon AppStream 2.0 with clipboard and file-transfer disabled.  
C. Embed a forensic watermark in the file and then allow direct S3 download.  
D. Require the vendor to use a company-issued laptop with EDR and full-disk encryption.  

Correct Answer: B  
Explanation: A remote desktop/streaming session keeps the plaintext in the AWS data centre; disabling clipboard/file-transfer prevents exfiltration. A still allows the file to be downloaded inside China. D protects the laptop but not the asset once it leaves S3. C deters but does not prevent copying.
Q1. A multinational retailer is preparing to migrate its on-premise customer-analytics platform to a public PaaS offering. The data set includes 30 million customer records classified as “Confidential – EU Residents.” The cloud provider’s shared-responsibility brief states that the customer is responsible for “data classification, labeling, and privacy controls.” Which action is MOST critical before the migration kicks off?  
A. Negotiate a right to audit clause into the new cloud contract so internal auditors can re-classify the data after it lands in the provider’s object store.  
B. Re-label every field in every database with the provider’s proprietary taxonomy so that object tags follow the retailer’s data dictionary.  
C. Map each GDPR data category to the provider’s labels, then tag data at the object level so retention, locality and deletion obligations travel with the asset.  
D. Export the data to an encrypted tape archive so the original classification labels remain intact in off-line storage.  

Correct Answer: C  
Explanation: Asset Security (Domain 2) requires that classification and labeling persist throughout the life-cycle, especially when responsibility shifts to a cloud shared-responsibility model. Option C ensures that EU-privacy obligations remain bound to the data set even when it moves to the PaaS object store. A is useful but reactive; classification must already be in place before migration. B merely adopts the vendor’s taxonomy without guaranteeing alignment to GDPR categories. D removes the data from the architecture instead of securing it in its intended environment.

Q2. A hospital’s medical-device network has 400 embedded infusion pumps whose firmware cannot be updated by the vendor. The security team discovers that the pumps store ePHI in volatile memory only, but the ePHI is transmitted in cleartext to the central monitoring server. Asset classification efforts have just begun. How should the pumps be handled?  
A. Exclude the pumps from the asset inventory because they are “firmware-static” and therefore out of scope for data-classification policy.  
B. Classify the pumps as data assets containing ePHI, apply compensating network encryption, and record them in the asset inventory with an explicit exception note.  
C. Re-categorize the ePHI as public data since it is volatile and not stored on the device.  
D. Decommission all 400 pumps immediately to avoid regulatory non-compliance.  

Correct Answer: B  
Explanation: Domain 2 requires that every asset that processes, stores, or transmits sensitive data be inventoried and classified. Even volatile ePHI is still ePHI. Option B maintains the inventory’s integrity while applying compensating controls (encryption) where remediation (patching) is impossible. A creates an invisible risk; C mis-classifies the data, undermining downstream controls; D is an unnecessary business disruption.

Q3. During a post-acquisition integration, the acquiring company finds that the target’s R&D file share uses a four-level internal classification: Public, Internal, Secret, Top-Secret. The acquiring firm’s policy recognizes only Public, Internal, Confidential, Restricted. The target’s “Secret” data will be migrated into the acquiring firm’s data lake next quarter. Which next step best preserves asset security governance?  
A. Map “Secret” to “Confidential,” update metadata on every object, and record the mapping in the data-catalog so downstream DLP rules trigger correctly.  
B. Leave labels unchanged and instruct users to apply their best judgment when saving files to the new data lake.  
C. Create a fifth label “Legacy-Secret” so nothing is downgraded accidentally.  
D. Elevate all “Secret” data to “Restricted” to err on the side of caution.  

Correct Answer: A  
Explanation: Consistent classification across the enterprise is a core Domain 2 requirement. A produces a one-to-one mapping that aligns with the acquirer’s four-tier scheme and ensures policy enforcement tools (DLP, access control, retention) operate correctly. B invites inconsistent handling. C perpetuates fragmentation. D over-protects, potentially blocking legitimate business workflows and inflating cost.

Q4. A SaaS start-up offers customers the option to upload sensitive documents for AI-driven translation. The start-up’s data-classification matrix states that customer documents are “Customer-Owned—Classification Unknown.” Privacy counsel now demands that the company treat every uploaded file as “Highly Confidential” by default. The ops team objects because the label triggers aggressive retention (30-day deletion) that would break the SLA (12-month availability). Which compromise best balances Domain 2 principles with business obligations?  
A. Create a new label “Customer Data—Unknown Sensitivity” with retention tied to the SLA and add mandatory tagging within 72 hours of upload based on customer disclosure.  
B. Accept the counsel’s demand and shorten the SLA to 30 days.  
C. Keep the “Unknown” label but encrypt the files and skip any further classification effort.  
D. Refuse to change the label; instead, add a click-through disclaimer that shifts classification responsibility to the customer.  

Correct Answer: A  
Explanation: Domain 2 expects an organization to classify assets “in a timely manner” while supporting business and legal requirements. Option A introduces an interim controlled label, satisfies the 72-hour classification window, and preserves the 12-month SLA. B imposes an unnecessary business penalty. C leaves data under-classified, defeating downstream controls. D improperly outsources a core security responsibility.

Q5. A government contractor maintains a classified project repository on an air-gapped network. A junior administrator copies 200 MB of “Secret” design files to a DVD-R labeled “Unclassified—Draft Graphics” so he can work from home. The security team discovers the mismatch during a routine asset-label audit. Which corrective measure BEST prevents recurrence while meeting Domain 2 requirements?  
A. Increase the frequency of network penetration tests on the air-gapped segment.  
B. Sanction the employee and rely on managerial reprimand to deter future misuse.  
C. Implement mandatory, technical labeling controls that embed classification metadata into each file and enforce write-blocking for removable media unless the label matches the intended destination zone.  
D. Re-classify all “Secret” data to “Top Secret” so employees will take extra care.  

Correct Answer: C  
Explanation: Domain 2 emphasizes labeling that is “persistent” and “usable across the life-cycle.” Technical, enforceable labels tied to hardware controls directly address the root cause: human mislabeling that enables data spillage. A focuses on the wrong threat vector (external penetration). B is punitive but not preventive. D merely escalates classification without fixing the process gap.
