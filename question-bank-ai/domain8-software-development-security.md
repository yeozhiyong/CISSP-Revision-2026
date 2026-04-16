Q1. A global e-commerce company is adopting a DevSecOps model and wants to ensure that every pull-request to the “main” branch is automatically evaluated for security before it can be merged. They currently run SAST, DAST, dependency-check, Infrastructure-as-Code (IaC) scanning, and unit tests in parallel inside containerized build agents. During the first week of operation the pipeline blocks 38 % of all pull-requests because the IaC scan flags the Terraform module that creates the AWS S3 bucket as non-compliant. The Terraform module sets “block-public-acls = true” and uses AES-256 server-side encryption, but the scanner still fails the build. Which of the following is the MOST probable root-cause and the simplest fix that will reduce false positives without weakening security posture?

A. The scanner rule set is outdated and does not recognize the newer “block-public-acls” parameter; update the scanner signature database.  
B. The Terraform module is missing an explicit “bucket-policy” that denies HTTP access; add an AWS:SecureTransport condition.  
C. The scanner requires the bucket to be created with “ObjectOwnership=BucketOwnerEnforced” to enforce AWS ownership controls; add the attribute.  
D. The scanner is flagging the absence of a “lifecycle-policy” for aborting incomplete multipart uploads; add the lifecycle block.

Correct Answer: C  
Explanation: Many hardened CIS benchmarks and custom policy packs used by IaC scanners will fail an S3 bucket unless “ObjectOwnership” is explicitly set to “BucketOwnerEnforced” (or the legacy “BucketOwnerPreferred”) to prevent ACL-based object ownership hijacking. The other options either describe controls that are not related to the ownership issue (A, B) or are secondary hardening items that would not cause an immediate block (D).

------------------------------------------------------------------

Q2. A medical-device manufacturer is rewriting the firmware for an implanted cardiac monitor. Because the device communicates over Bluetooth Low Energy (BLE) to a smartphone app, the development team must implement mutual authentication and encrypted channels within severe CPU and battery constraints. The team’s lead architect proposes using ECDH (P-256) for key agreement and AES-CCM for packet encryption, but the security reviewer insists that NIST SP 800-56A “Key Establishment” schemes require full key confirmation and an RNG with 256-bit entropy. The hardware RNG realistically provides only 160-bit entropy. Which option BEST satisfies the security requirements while remaining feasible on the device?

A. Replace ECDH with a pre-shared AES-128 key loaded at manufacturing time and use AES-CCM.  
B. Keep ECDH P-256, concatenate the 160-bit RNG output with a 96-bit counter value, feed the 256-bit result through a NIST-approved DRBG, and perform key-confirmation as per SP 800-56A.  
C. Switch to ECDH Curve25519 which does not require key confirmation and use Poly1305-ChaCha20.  
D. Derive the ECC private key directly from the 160-bit RNG and rely on ECDSA signature for authentication instead of key confirmation.

Correct Answer: B  
Explanation: SP 800-56A allows key confirmation and mandates adequate entropy. By expanding the 160-bit hardware entropy through a NIST-approved deterministic random-bit generator (DRBG) and adding key confirmation, the solution stays within standard constraints. Option A removes forward secrecy, Option C introduces non-NIST curves that may not pass FDA/NIST review, and Option D skips key confirmation and risks weak private keys.

------------------------------------------------------------------

Q3. A SaaS provider is building a multi-tenant REST API that uses JSON Web Tokens (JWT) for authorization. To achieve horizontal scalability, the company signs tokens with an RSA private key and publishes the corresponding public key at an HTTPS JWKS endpoint. During a penetration test, the tester demonstrates that if a victim user can be convinced to visit an attacker-controlled site while logged into the SaaS, the attacker can replay the victim’s JWT against the “/admin/backup” endpoint and receive a full database dump. Logs show that the JWT was still within its “exp” claim but was originally issued for the “/user/profile” endpoint. Which control would have MOST effectively prevented this unauthorized reuse?

A. Store a per-JWT jti claim in a server-side cache and reject replayed tokens.  
B. Add an application-level “scope” claim in the JWT and enforce authorization at the endpoint layer.  
C. Bind the JWT to the client’s TLS session ID so it cannot be replayed over another channel.  
D. Shorten the “exp” claim to five minutes and rely on refresh tokens.

Correct Answer: B  
Explanation: The attack succeeded because the service performed authentication but failed to check whether the token holder was actually authorized for the requested resource. Embedding an explicit “scope” or “authorization” claim and enforcing it at every endpoint is the most direct fix. Option A blocks replay but not privilege escalation, Option C is impractical across load-balancers, and Option D merely narrows the window without fixing the privilege mismatch.

------------------------------------------------------------------

Q4. A Fortune-500 company is adopting a micro-service architecture orchestrated by Kubernetes. The security team wants to prevent compromised containers from harvesting secrets stored in environment variables. The company already uses a commercial secrets vault with dynamic secrets and short TTLs. Which Kubernetes-native feature BEST complements the vault to keep secrets out of the process environment?

A. Use Kubernetes Secrets mounted as tmpfs volumes and referenced via volumeMounts in the pod spec.  
B. Store secrets in etcd encrypted with a KMS provider and rely on RBAC to limit access.  
C. Use a MutatingAdmissionWebhook that injects secrets directly into the application’s configuration file on startup.  
D. Run the container with the “–read-only” flag and copy secrets through docker exec at runtime.

Correct Answer: A  
Explanation: Mounting secrets as memory-only tmpfs volumes keeps them out of the container’s environment block and off the union filesystem, while still allowing the application to read them as files. Option B protects data at rest but not at runtime, Option C still leaves secrets in a file that might be committed or logged, and Option D is manual and non-scalable.

------------------------------------------------------------------

Q5. A payment-card company is implementing a new Android mobile app that will store sensitive customer authentication data (SAD) temporarily in encrypted SharedPreferences while waiting for network connectivity. The app must remain PCI DSS compliant. The lead developer proposes using Android’s Keystore-generated 256-bit AES key, encrypted with an RSA 2048-bit key also stored in the Keystore, and setting KeyGenParameterSpec.Builder.setUserAuthenticationRequired(true) with an authorization timeout of 30 seconds. The QSA objects that the solution may still violate PCI DSS requirement 3.2 (no storage of SAD after authorization). Which additional control BEST addresses the QSA’s concern?

A. Set setUserAuthenticationRequired(true) without any timeout so the key is unusable unless the user is present.  
B. Store the data in RAM only and wipe the byte array once the network call succeeds.  
C. Encrypt the data with a key derived from both the Keystore key and a server-side component, then delete the server component after authorization.  
D. Use hardware-backed StrongBox and set setInvalidatedByBiometricEnrollment(true).

Correct Answer: C  
Explanation: By splitting the key so that the server supplies an ephemeral component that is destroyed after authorization, the mobile device can no longer decrypt SAD, thereby satisfying PCI DSS 3.2. Option A still allows local decryption within 30 s, Option B risks memory dumps, and Option D is a hardware requirement that does not guarantee post-authorization deletion.

------------------------------------------------------------------

Q6. A government agency is contracting a vendor to build a new citizen-service portal that must comply with NIST SP 800-63-3 Authenticator Assurance Level 3 (AAL3). The vendor wants to use a single multi-factor cryptographic device that performs both possession and biometric verification. Which of the following authentication flows BEST meets AAL3 requirements?

A. FIDO2/WebAuthn with a roaming authenticator that verifies a fingerprint, outputs a signed assertion, and requires PIN entry if the biometric fails.  
B. One-time password (TOTP) mobile app plus SMS backup codes.  
C. Smart card with PKI certificate plus memorized secret (password) verified on the server.  
D. Push notification to a mobile phone that the user approves with FaceID.

Correct Answer: A  
Explanation: AAL3 requires a hardware-based cryptographic authenticator with multi-factor verification (something you have + something you are/know) and verifier impersonation resistance. FIDO2/WebAuthn with a roaming authenticator that incorporates biometric verification and fallback PIN meets these criteria. TOTP/SMS (B) lacks verifier resistance, smart-card + password (C) is AAL2 unless the card reader also verifies biometrics, and push + FaceID (D) does not bind the cryptographic operation to the device.

------------------------------------------------------------------

Q7. A software company is establishing a Secure Development Lifecycle (SDLC) for its first ISO 27034-compliant application. During the security risk assessment, the team identifies a high-risk threat: malicious insiders with source-code access could embed backdoors that exfiltrate customer PII. Management is unwilling to accept the risk and asks for a preventive control. Which control provides the BEST prevention while remaining compatible with agile delivery?

A. Implement four-eyes code review (two approvers) plus mandatory static-analysis rules that reject any network or crypto API call not on an approved whitelist.  
B. Log every git push to a SIEM and use UEBA to detect anomalous commits.  
C. Run a daily full-penetration test against the staging environment.  
D. Digitally sign all release binaries and verify the signature at installation time.

Correct Answer: A  
Explanation: Requiring two independent reviewers plus an automated whitelist of sensitive APIs directly prevents unauthorized code from reaching the mainline, addressing the insider threat at the point of introduction. SIEM/UEBA (B) is detective, daily pentesting (C) is too late and too costly, and code signing (D) ensures integrity but does not prevent backdoor insertion.

------------------------------------------------------------------

Q8. A cloud-native team is building a CI/CD pipeline in AWS. The buildspec.yml file needs to retrieve the database password from AWS Secrets Manager, run integration tests, then destroy the RDS instance. The team wants to minimize the risk of accidental password leakage in build logs. Which approach is the MOST secure and operationally simple?

A. Export the password as an environment variable and mark the CodeBuild project with “secure-environment-variables” set to true.  
B. Use the Secrets Manager GetSecretValue API inside the build script, assign the value to a bash variable, and overwrite it with an empty string after the test step.  
C. Store the password in AWS Systems Manager Parameter Store (SecureString) and reference it directly in the buildspec using “–parameter-override” without printing it.  
D. Let the build job assume an IAM role that can only read the secret, retrieve the secret, mask the variable in CodeBuild logs, and unset it after use.

Correct Answer: D  
Explanation: AWS CodeBuild can automatically mask secrets retrieved via the Secrets Manager plugin when the build job assumes an IAM role with least privilege. This keeps the plaintext out of logs and avoids custom overwrite code. Option A still risks echoing the variable, Option B relies on developer discipline, and Option C does not natively mask values.

------------------------------------------------------------------

Q9. A global logistics firm is exposing a new GraphQL endpoint to replace legacy REST services. During a design review, the security team notes that nested queries could lead to denial-of-service through excessive database joins. The developers propose limiting query depth to 7 levels and disabling introspection in production. Which additional control BEST mitigates remaining GraphQL-specific abuse without breaking legitimate clients?

A. Implement server-side query-complexity analysis that assigns cost points to each field and rejects requests that exceed a budget.  
B. Require mutual TLS so only known clients can connect.  
C. Enable schema-stitching to split the graph into federated subgraphs.  
D. Convert all GraphQL mutations back to REST endpoints and expose only read queries.

Correct Answer: A  
Explanation: Query-complexity analysis (a.k.a. “cost analysis”) quantifies the server work implied by a query and blocks expensive requests regardless of depth, addressing the DoS vector. mTLS (B) is transport-layer, schema-stitching (C) does not limit cost, and reverting to REST (D) negates the architectural benefits.

------------------------------------------------------------------

Q10. A software vendor is undergoing a SOC 2 Type II audit. The auditor discovers that the production build server uses a mutable baseline image that administrators patch manually each month. The server also hosts both the build agent and the artifact repository on the same VM. The auditor cites this as a deficiency against CC6.1 (logical access) and CC7.2 (system monitoring). Which remediation step BEST addresses both citations simultaneously while supporting DevOps velocity?

A. Rebuild the build server from a locked, versioned golden image each night via Infrastructure-as-Code, and stream all OS-level and application logs to a tamper-proof log aggregator.  
B. Require two-factor authentication for administrators and enable FIM (File Integrity Monitoring) on the VM.  
C. Separate the artifact repository onto its own VM and keep the existing build server patching process.  
D. Move the build workload to a serverless CI service and delete the VM.

Correct Answer: A  
Explanation: Nightly immutable rebuilds from a versioned image eliminate configuration drift (CC6.1) while centralized, tamper-proof logging provides continuous monitoring (CC7.2). 2FA/FIM (B) helps but does not remove mutable state, separation (C) only partially reduces risk, and serverless (D) may not be feasible for all artifact types or compliance evidence retention.
Q1. A global e-commerce company is migrating its monolithic storefront to a micro-services architecture. During a threat-modeling workshop, the team identifies that the new “checkout” service will invoke the “payment” service over mTLS, but the payment service still needs to call a 15-year-old mainframe CICS module through a proprietary binary protocol. The mainframe module runs as a single batch ID with *ALLOBJ authority.  
A. Accept the risk; the mainframe has never been breached.  
B. Place both services behind a single API gateway and let the gateway terminate mTLS.  
C. Wrap the CICS module with a new least-privilege “facade” service that uses role-based access and input validation, then expose only the facade to the payment service.  
D. Re-write the CICS module in Java and deploy it in a container on OpenShift.  

Correct Answer: C  
Explanation: Domain 8 stresses secure software design and interfacing with legacy systems. Option C applies the security principles of least privilege, abstraction, and input validation while preserving the investment in the mainframe. A is a dangerous risk acceptance with no compensating control. B only moves the TLS termination point and does not address the excessive authority or protocol mismatch. D is ideal but not always feasible in the real world due to cost, schedule, or lack of source code; CISSP expects “best practical” security, not academic perfection.

---

Q2. Your firm’s Secure SDLC mandates that every pull request to the “main” branch must pass a SAST scan. A high-performing Scrum team complains that the SAST tool takes 45 minutes and breaks their “commit every few minutes” cadence. Product management threatens to remove the gate entirely.  
A. Run SAST only on the nightly build.  
B. Move the SAST gate to the merge of the release branch and accept that main may have vulnerabilities.  
C. Split the monolith into smaller compile-safe components and run incremental/differential SAST on only the changed code in the pipeline.  
D. Replace SAST with DAST because dynamic tests are faster.  

Correct Answer: C  
Explanation: Incremental/differential SAST preserves the security gate while reducing scan time, aligning with “shift-left” and “automation” tenets of Domain 8. A and B delay vulnerability detection, violating the principle of early remediation. DAST is complementary but does not identify code-level flaws such as hard-coded credentials or buffer overflows that SAST catches.

---

Q3. A healthcare SaaS start-up wants to achieve SOC 2 Type II within a year. The CTO insists on deploying every feature branch directly to production using feature flags to enable “true CI/CD.” The CISO is concerned that un-tested code paths could violate HIPAA.  
A. Disable feature flags for any code that touches PHI.  
B. Require that every feature flag be accompanied by a kill switch and a security review documented in Jira before the flag is created.  
C. Forbid feature flags and return to month-long release trains.  
D. Allow flags but rely on WAF rules to block any exploitation.  

Correct Answer: B  
Explanation: Feature flags are a legitimate DevOps practice, but HIPAA requires documented, risk-based controls. Option B introduces a compensating security review and an emergency kill switch, satisfying both agility and compliance. A is too restrictive and may impede innovation. C abandons CI/CD benefits. D places undue confidence in a perimeter control that cannot understand business logic flaws.

---

Q4. During a code review, a senior developer discovers that the junior team used RSA ECB (electronic-codebook) mode to encrypt credit-card tokens at rest. The sprint ends tomorrow.  
A. Defer the fix to the next sprint because no breach has occurred.  
B. Apply for a PCI-DSS waiver and continue using ECB.  
C. Immediately re-encrypt using RSA-OAEP or switch to AES-256-GCM and rotate all tokens.  
D. Add a secondary layer of base64 encoding and release on schedule.  

Correct Answer: C  
Explanation: ECB leaks deterministic patterns; Domain 8 requires use of strong, modern cryptographic modes. RSA-OAEP or authenticated AES-GCM is the correct remediation. A and B violate due-care and PCI-DSS 3.5.1. D is obfuscation, not encryption.

---

Q5. A mobile banking app uses a third-party facial-recognition SDK. The SDK vendor’s privacy policy states that biometric templates are stored “in the secure cloud.” Your data-protection impact assessment (DPIA) concludes that the vendor is a data processor under GDPR.  
A. Add a clause in the EULA stating that the user consents to offshore biometric storage.  
B. Ensure a Data Processing Agreement (DPA) is signed, require SOC 2 + ISO 27018 attestations, and implement on-device template generation with irreversible cancelable biometrics.  
C. Drop the SDK and build your own facial-recognition algorithm.  
D. Anonymize the templates by removing the user’s last name.  

Correct Answer: B  
Explanation: GDPR Article 28 mandates a DPA, and biometric data is “special category” requiring extra safeguards. On-device generation plus cancelable biometrics reduces breach impact and aligns with privacy-by-design (Domain 8). A’s consent clause is invalid under GDPR because special-category data needs explicit, freely given, informed consent plus necessity test. C is disproportionate cost. D does not anonymize high-entropy biometric vectors.

---

Q6. A start-up’s flagship REST API is implemented in Node.js and relies on 247 open-source npm packages. A routine dependency scan reveals that one nested package, “left-pad 1.0.2,” is licensed under GPL-3.0 and is distributed in the Docker image shipped to customers.  
A. Ignore; the package is only 11 lines of code.  
B. Replace with a proprietary re-implementation or use a non-copy-left alternative, then re-test, to avoid GPL “viral” clause.  
C. Dual-license the start-up’s entire codebase under GPL.  
D. Ask customers to sign an NDA promising not to reverse-engineer the GPL code.  

Correct Answer: B  
Explanation: GPL-3.0 requires that combined work be released under the same license, creating IP risk. Option B is the standard commercial approach: remove or isolate the GPL dependency. A ignores license compliance. C is usually unacceptable to investors. D is unenforceable and does not satisfy GPL obligations.

---

Q7. A multinational ISV is adopting a DevSecOps model. The security team wants to insert an automated security test that verifies whether secrets are present in Docker image layers. Which is the MOST effective place to run this test?  
A. In the container registry’s webhook after the image is pushed.  
B. As a pre-receive hook in the Git server.  
C. As a stage in the CI pipeline before the image is built (e.g., pre-commit or pre-build).  
D. As a nightly cron job on the developer laptops.  

Correct Answer: C  
Explanation: Detecting secrets before the image is built prevents the secret from ever entering an intermediate layer that could be pulled later. A is too late—the secret is already in registry history. B only scans source, missing secrets added in Dockerfile COPY/ADD. D is unenforceable and non-centralized.

---

Q8. A government agency requires that all software packages be reproducibly built so that independent auditors can obtain identical binaries from the same source. Which of the following BEST supports this requirement?  
A. Pin dependency versions with checksums in a lock-file and use a hermetic, containerized build environment with fixed compiler tool-chain versions.  
B. Tag the release in Git and keep a README of build instructions.  
C. Use the “latest” tag for all dependencies to ensure patches are always included.  
D. Store the final binary in an immutable artifact repository.  

Correct Answer: A  
Explanation: Reproducible builds demand deterministic compilation, which is achieved by locking all inputs (source, libraries, compiler, timestamps). Option A embodies supply-chain integrity controls emphasized in Domain 8. B is insufficient because Readmes rarely capture the full environment. C introduces non-determinism. D preserves the output but does not guarantee reproducibility.

---

Q9. A financial firm is evaluating two static-analysis vendors. Vendor X reports 2,000 HIGH findings with 5 % false-positive rate. Vendor Y reports 200 HIGH findings with 40 % false-positive rate. Development capacity allows remediation of 150 findings per sprint.  
A. Select Vendor X because it finds the most real vulnerabilities.  
B. Select Vendor Y because the lower absolute count reduces developer fatigue.  
C. Run both tools and intersect the high-severity results to produce a de-duplicated list.  
D. Reject both and wait for a perfect tool with 0 % false positives.  

Correct Answer: C  
Explanation: Using multiple, heterogeneous security tools and correlating results is a defense-in-depth practice cited in Domain 8. Intersection reduces false positives while retaining broad coverage. A ignores the 5 % FP rate (still 100 bad alerts). B ignores the 40 % FP rate (80 bad alerts). D is impractical; no tool is perfect.

---

Q10. A cloud-native application uses Kubernetes with a GitOps workflow (ArgoCD). An attacker compromises a developer’s laptop and pushes a malicious image tag to the Git repository. ArgoCD automatically syncs and schedules the pod. Which control would have BEST prevented the deployment?  
A. A Kubernetes admission controller that verifies each pod image is signed by the corporate Notary v2 instance and rejects unsigned images.  
B. Runtime EDR on the worker node to kill the malicious process.  
C. A manual change-advisory board (CAB) meeting every Friday.  
D. Image vulnerability scanning with Trivy.  

Correct Answer: A  
Explanation: Code signing enforced at deploy time is a preventive control that stops tampered images before they run, aligning with secure coding and deployment practices in Domain 8. B is detective/corrective but too late. C conflicts with GitOps automation and does not scale. D identifies CVEs but does not attest to image authenticity.
Q1. A global e-commerce firm is adopting a “shift-left” DevSecOps model. During sprint planning, the product owner insists that new microservices must be built with reusable in-house libraries that have not been updated in three years. The security team runs an automated software-composition analysis (SCA) scan and discovers 17 CVEs rated HIGH or CRITICAL in those libraries. The DevOps lead argues that the libraries are “internal,” so the CVEs do not represent real risk. Which secure-coding principle is being violated MOST severely?  
A. Defense in depth  
B. Safe reuse of trusted components  
C. Psychological acceptability  
D. Complete mediation  

Correct Answer: B  
Explanation: Safe reuse demands that any component—internal or external—be free of known, exploitable vulnerabilities before integration. Ignoring 17 high/critical CVEs in shared libraries violates this principle and propagates risk across every consuming microservice. Defense in depth (A) is a broader architecture concept; psychological acceptability (C) relates to usability; complete mediation (D) refers to authorization checks on every access—none are the primary issue here.

--------------------------------------------------------------------
Q2. [Scenario] A healthcare start-up is building a mobile app that collects PHI and uploads it to a RESTful API running in AWS. The development team decides to use a commercial cross-platform SDK that promises “bank-level encryption.” The SDK ships as a shared-object file without source code. Pen-testing reveals that the SDK statically embeds a 512-bit RSA private key that is identical in every download. Which aspect of software-supply-chain risk is MOST evident?  
A. Insider threat from AWS administrators  
B. Third-party component transparency  
C. Insecure deserialization in REST endpoints  
D. Weak session management  

Correct Answer: B  
Explanation: The vendor supplied an opaque binary with a hard-coded, weak key—classic supply-chain opacity. Without source or attestations (SBOM, SLSA, etc.), the team cannot verify crypto implementations or rotate the key, illustrating third-party component transparency risk. The other choices describe different attack surfaces not highlighted by the scenario.

--------------------------------------------------------------------
Q3. [Scenario] A bank’s waterfall SDL requires that security teams perform threat modeling only during the “design” phase. After code freeze, a static-analysis scan finds 400+ instances of SQLi in legacy COBOL modules that interface with a new Java layer. Remediation would delay release by four months and cost €2 M. Which CORE security activity, had it been performed continuously, would MOST likely have prevented this expensive late-stage discovery?  
A. fuzz testing  
B. secure code review  
C. iterative threat modeling  
D. penetration testing  

Correct Answer: C  
Explanation: Iterative threat modeling (e.g., STRIDE per user story or sprint) surfaces trust-boundary violations—such as new Java-to-COBOL data flows—early enough to architect controls like parameterized queries or ORM libraries. Static scans, fuzzing, and pen-tests are point-in-time validation techniques; they do not proactively design out flaws.

--------------------------------------------------------------------
Q4. [Scenario] A government agency is adopting a microservices architecture orchestrated by Kubernetes. Developers bind service-to-service tokens to the container image at build time so that containers can authenticate to an internal IAM service. A misconfigured Git repo leaks the image, and attackers extract the embedded token. Which secure-coding practice would BEST have mitigated this breach?  
A. Externalizing secrets to a runtime secrets-manager  
B. Digitally signing the container image  
C. Scanning base images for CVEs  
D. Enabling mutual TLS between pods  

Correct Answer: A  
Explanation: Embedding secrets in images is an anti-pattern; externalizing them to a runtime vault (e.g., Vault, AWS Secrets Manager) keeps sensitive material out of artifacts and allows rotation without rebuilding. Image signing (B) assures integrity but does not protect a leaked embedded token. CVE scanning (C) and mTLS (D) are good hygiene but do not address secret leakage.

--------------------------------------------------------------------
Q5. [Scenario] A SaaS provider practices continuous deployment, pushing code to production 50× daily. The firm adds a “canary” stage wherein 5 % of traffic hits new builds. After three minutes, if error rates stay below 0.1 %, the build proceeds to 100 %. One Friday, an engineer inadvertently commits credentials that are baked into JSON config and exposed via an info leak bug. The credentials are not detected by unit tests or SAST. Within four minutes, automated rollback occurs because the canary triggers 0.3 % 5xx errors. Which DevSecOps benefit is PRIMARILY demonstrated?  
A. Immutable infrastructure  
B. Fast feedback and fail-fast  
C. Blue/green environment parity  
D. Infrastructure as Code version control  

Correct Answer: B  
Explanation: The canary environment provided rapid telemetry that the defective build introduced faults, prompting automatic rollback—an example of fast feedback and fail-fast culture. Immutable infra (A) refers to replacing rather than patching servers; blue/green (C) is a different deployment pattern; IaC version control (D) is unrelated to runtime defect detection.

--------------------------------------------------------------------
Q6. [Scenario] A PCI-DSS merchant is refactoring its monolithic payment service into serverless functions (AWS Lambda). The security team mandates that every function artifact be accompanied by an SBOM in CycloneDX JSON and that the build pipeline reject functions containing GPL-3.0 libraries. Which software-supply-chain security objective is being enforced?  
A. License compliance and risk management  
B. Code obfuscation  
C. High availability  
D. Threat modeling  

Correct Answer: A  
Explanation: GPL-3.0 can impose copyleft obligations incompatible with proprietary distribution; blocking it addresses intellectual-property compliance risk, an increasingly critical part of supply-chain security. The SBOM provides transparency, but the decisive action here is license enforcement.

--------------------------------------------------------------------
Q7. [Scenario] An automotive OEM’s infotainment firmware is built in C++ and uses a home-grown memory allocator. During fuzzing, researchers discover a heap-based buffer overflow that can be reached via malformed ID3 tags in MP3 files. Management asks why earlier code audits missed the flaw. The security architect traces the issue to custom macros that hide pointer arithmetic, making bounds checking non-obvious. Which secure-coding technique would BEST reduce recurrence?  
A. Replacing custom macros with safer abstractions (e.g., std::span)  
B. Increasing compiler optimization level  
C. Switching to a functional language  
D. Mandatory unit-test coverage of 90 %  

Correct Answer: A  
Explanation: Safer abstractions enforce bounds contractually at compile time or runtime, eliminating hidden arithmetic. Higher optimization (B) can even remove security checks; language shift (C) is impractical for legacy C++ firmware; high coverage (D) does not guarantee absence of edge-case overflows.

--------------------------------------------------------------------
Q8. [Scenario] A Fortune 500 company runs an internal PKI that issues short-lived X.509 certificates to containerized workloads. A new Go microservice uses the private key by reading a file on a tmpfs mount. The developers chmod the file to 0644 so that an unprivileged sidecar metrics exporter can read it. An attacker who compromises the exporter can now retrieve the key and impersonate the workload. Which secure-coding principle is MOST directly violated?  
A. Least privilege  
B. Separation of duties  
C. Open design  
D. Fail secure  

Correct Answer: A  
Explanation: The key file is granted world-readable permission, exceeding the minimum access required by the legitimate process—classic violation of least privilege. Separation of duties (B) applies to role assignment; open design (C) refers to cryptographic transparency; fail secure (D) relates to maintaining security state after error.

--------------------------------------------------------------------
Q9. [Scenario] A social-media company crowdsources mobile-app beta builds through TestFlight and Google Play Console closed tracks. A rogue employee embeds an Easter-egg feature that uploads the user’s entire photo roll to a private S3 bucket controlled by the employee. Neither Apple’s nor Google’s pre-release scanning detects the behavior, and the code is guarded by an OS-detection conditional that activates only after 24 hours. Which control would BEST detect this malicious code before public release?  
A. Mandatory developer background checks  
B. Manual code review focusing on conditional compilation blocks  
C. Runtime application self-protection (RASP) in production  
D. Binary diversity compilation  

Correct Answer: B  
Explanation: Human review of unobfuscated conditional blocks can spot time-bomb or environment-gated malicious logic that automated scanners miss. Background checks (A) deter but do not detect; RASP (C) is reactive and post-release; binary diversity (D) mitigates exploitation but not insider code injection.

--------------------------------------------------------------------
Q10. [Scenario] A retail chain maintains a 20-year-old COBOL inventory system that is too brittle to refactor. The CIO mandates that a new REST wrapper written in Spring Boot expose read-only data via HTTPS. Pen-testing shows that the wrapper is vulnerable to XXE attacks because it accepts XML input and enables external entities to support legacy clients. The security team recommends disabling external entities, but the dev team claims this will break compatibility. Which secure-SDLC strategy is MOST appropriate for resolving the impasse?  
A. Deploy a Web Application Firewall signature and defer fixing  
B. Create an API gateway that transforms JSON to minimal XML without external entities  
C. Accept the risk and document it in the risk register  
D. Rewrite the COBOL system to natively emit JSON  

Correct Answer: B  
Explanation: An API gateway can act as a secure façade, translating safe JSON requests into XML devoid of external entities, thereby neutralizing XXE while preserving legacy compatibility. Relying solely on WAF (A) is bypass-prone; accepting risk (C) ignores regulatory due-diligence; full rewrite (D) is cost-prohibitive and high-risk for a brittle system.
Q1. A global retail company is migrating its monolithic, on-premise point-of-sale (POS) suite to a containerized micro-service architecture running in a public cloud. The security team wants to ensure that every build promoted to the staging repository has a verifiable, tamper-evident chain of custody from source to image. Which of the following BEST satisfies the goal while fitting naturally into an “everything-as-code” CI/CD pipeline?  
A. Digitally sign the container image with the company’s private code-signing key and publish the corresponding public key to an internal certificate transparency log.  
B. Store the SHA-256 hash of the final image layer in the Git repo that holds the Dockerfile so the ops team can compare hashes before deployment.  
C. Require the pipeline to push the image to a registry that enforces Docker Content Trust (DCT) and configure all orchestration nodes to enable DCT verification.  
D. Tag every image with the Git commit hash and block promotion unless the tag is prefixed with “RELEASE-”.  

Correct Answer: C  
Explanation: Docker Content Trust (DCT) implements The Update Framework (TUF), providing signed metadata that is automatically verified by the Docker CLI/container runtime. It establishes a cryptographically secure chain of custody (signing at build, verification at deploy) without manual hash comparison or reliance on human-readable tags. A transparency log (A) is useful for public discovery but does not enforce runtime verification. Storing a hash in Git (B) is brittle and offers no integrity once the image leaves the build node. Commit-hash tagging (D) is good for traceability but lacks cryptographic assurance of image integrity.

--------------------------------------------------------------------

Q2. During a secure-code review of a new REST API, the security architect discovers that the “/admin/backup” endpoint accepts a “path” query parameter which is concatenated directly with a base directory and passed to the operating system to create a zipped backup. The developer argues the code is safe because it strips “..” sequences and because the service runs as a low-privilege account. Which attack is STILL possible against the endpoint?  
A. Server-Side Request Forgery (SSRF)  
B. Local File Inclusion / Path Traversal  
C. XML External Entity (XXE)  
D. Insecure Direct Object Reference (IDOR)  

Correct Answer: B  
Explanation: Black-list filtering of “..” is notoriously insufficient; alternate encodings (e.g., “..%252f”, Unicode overlong sequences, or absolute symlinks) can still traverse outside the intended directory. Because the parameter ultimately reaches the OS file system API, the flaw is a classic path traversal / local file inclusion. SSRF (A) requires the app to fetch remote URLs, XXE (C) requires XML parsing with external entities enabled, and IDOR (D) is about access-control on objects, not file-system traversal.

--------------------------------------------------------------------

Q3. A fintech start-up practices continuous deployment of its Node.js payment service. The security team wants to prevent production secrets (API keys, DB credentials) from ever being stored in the Git repository while still allowing developers to run the full stack locally. Which approach MOST effectively enforces this requirement with the LOWEST ongoing operational overhead?  
A. Check an “env.example” file into Git and add “*.env” to .gitignore; require developers to copy and populate env.example before starting the app.  
B. Store secrets in an encrypted YAML file committed to the repo; decryption key is delivered to laptops via the corporate MDM.  
C. Move all secrets to a cloud-native key management service (KMS) and inject them at runtime through environment variables populated by the orchestration platform.  
D. Commit GPG-encrypted secrets under a “secrets” directory; require each engineer to add their public key to a shared keyring.  

Correct Answer: C  
Explanation: Using a KMS plus runtime injection keeps secrets out of source control entirely, enforces access control via IAM, rotates easily, and requires no manual file handling by developers. Options A and D still risk accidental commit of plaintext or forgotten files. Option B places encrypted secrets in version control, which violates the “don’t store secrets in repos” principle even if encrypted.

--------------------------------------------------------------------

Q4. A company is adopting a DevSecOps model. The CISO wants every pull request to automatically undergo SAST, DAST, dependency-scan, and infrastructure-as-code (Terraform) linting. Which orchestration layer is BEST suited to aggregate all results into a single policy gate that blocks merge if any critical findings exist?  
A. A Static Analysis Results Interchange Format (SARIF)–compliant IDE plugin run on the developer’s laptop.  
B. The built-in security tab of the on-premise Git repository that only ingests SAST output.  
C. A containerized “policy-as-code” validator (e.g., OPA/Conftest) invoked in the CI server after all tools emit JSON/SARIF reports.  
D. A standalone DAST appliance that opens tickets in Jira automatically.  

Correct Answer: C  
Explanation: Running a policy-as-code engine inside the CI pipeline allows uniform evaluation of heterogeneous tool outputs (SAST, DAST, dependency, IaC) and enforces a single quality gate before merge. IDE plugins (A) are pre-commit, not PR-gating. Git repo security tabs (B) usually cover only one tool type. Stand-alone DAST appliances (D) operate post-deploy and are not part of the PR workflow.

--------------------------------------------------------------------

Q5. A multi-tenant SaaS application uses a shared PostgreSQL database. Each table carries a “tenant_id” column and every produced query appends “WHERE tenant_id = ?”. During a penetration test the consultant shows that simply changing the exposed REST ID “/orders/1234” to “/orders/5678” returns another tenant’s data. Which secure-coding technique would have PREVENTED the issue?  
A. Parameterized queries / prepared statements  
B. Row-Level Security (RLS) policies in the database tied to the application user’s session context  
C. Escaping single quotes and semicolons before concatenating SQL  
D. Forcing HTTPS on all API endpoints  

Correct Answer: B  
Explanation: Row-Level Security lets the database enforce “tenant_id = current_tenant” at the storage engine level, making it impossible for any application query—no matter how it is constructed—to touch other tenants’ rows. Parameterized queries (A) prevent SQL injection but not IDOR/authorization bypass. Escaping (C) is also SQL-injection focused. HTTPS (D) protects data in transit, not access control.

--------------------------------------------------------------------

Q6. A mobile banking app uses a 3rd-party facial-recognition SDK downloaded from an open-source repository. The security policy requires that any open-source component must not have a CVSS score ≥ 7 in the NVD and must be licensed under OSI-approved terms. Which tool BEST automates enforcement of this policy at build time?  
A. Interactive Application Security Testing (IAST) console  
B. Software Composition Analysis (SCA) scanner integrated into the CI pipeline  
C. Fuzzing framework that targets the SDK’s native libraries  
D. Manual code review by an external auditor  

Correct Answer: B  
Explanation: SCA tools (e.g., Snyk, WhiteSource, Black Duck) parse dependency manifests, match against vulnerability databases, and can break the build if a component violates CVSS or licensing rules. IAST (A) looks for runtime flaws in custom code, not 3rd-party libraries. Fuzzing (C) finds implementation bugs but does not check CVE or license. Manual review (D) is neither scalable nor automated.

--------------------------------------------------------------------

Q7. A healthcare provider is writing an embedded insulin-pump control unit in C. Because the device is life-critical, the firmware must never dereference a null or freed pointer after deployment. Which language-level countermeasure is MOST effective during compilation?  
A. Address Space Layout Randomization (ASLR)  
B. Static analysis with MISRA-C compliance checking  
C. Using a language subset (e.g., CERT C) combined with a proven memory-safe subset compiler (e.g., MISRA-C + static analyzer)  
D. Hardware watchdog timer  

Correct Answer: C  
Explanation: A memory-safe subset plus static analysis catches null or use-after-free issues at build time, eliminating entire classes of vulnerabilities before the code reaches the device. ASLR (A) is a runtime OS mitigation, not language-level. A watchdog (D) reboots on hangs but does not prevent pointer misuse. MISRA-C compliance (B) is part of the correct answer but is only half of the picture without enforcement via a compiler/static-analysis toolchain.

--------------------------------------------------------------------

Q8. A startup practicing Infrastructure-as-Code (IaC) uses Terraform to spin up AWS workloads. A developer accidentally commits an AWS access key and secret to the public GitHub repo. Within one minute the credential is detected by an external attacker and used to launch 500 large EC2 instances for crypto-mining, costing $8 000. Which control would have MOST economically prevented the incident?  
A. AWS CloudTrail anomaly detection alerting the SOC within 15 minutes  
B. A pre-commit git hook that runs the open-source tool “git-secrets” to block any AWS key pattern  
C. Mandatory vCPU service quotas in the AWS account set to the startup’s baseline need  
D. GuardDuty runtime alert that terminates instances tagged as crypto-miners  

Correct Answer: B  
Explanation: Blocking the secret at the moment of commit (pre-commit hook) prevents exposure entirely and costs virtually nothing. CloudTrail/GuardDuty (A, D) are detective and would still incur cost before remediation. Service quotas (C) limit blast radius but do not prevent unauthorized API calls or data theft.

--------------------------------------------------------------------

Q9. A web application relies on a legacy SOAP service that accepts XML from partners. The development team wants to allow external entities so that partners can reference local DTDs for validation, but the security team is concerned about XXE attacks. Which approach BEST balances functionality and security?  
A. Disable XML external entities entirely and ask partners to embed DTDs inline.  
B. Use a validating XML parser that resolves external entities but runs inside a sandboxed container with no network egress.  
C. Configure the parser to allow only trusted, pre-whitelisted external entities fetched over HTTPS from a partner-controlled domain.  
D. Keep the legacy service as-is and place it behind an XML firewall that blocks outbound connections from the service host.  

Correct Answer: A  
Explanation: The only fully reliable defense against XXE is to disable external entity resolution. Inline DTDs still allow validation without network lookups. Sandboxing (B) or whitelisting (C) reduces but does not eliminate risk (e.g., file:// URIs, SSRF via HTTPS). An XML firewall (D) does not stop internal file reads or DoS from entity expansion.

--------------------------------------------------------------------

Q10. A company is evaluating two static-analysis solutions for its Java codebase. Tool X reports 300 findings per KLOC with a false-positive rate of 45 %. Tool Y reports 30 findings per KLOC with a false-positive rate of 5 %. The development team has limited bandwidth to triage findings. Which tool BETTER aligns with the “risk-based” secure-code strategy advocated by CISSP?  
A. Tool X, because more findings indicate deeper analysis and therefore higher security coverage.  
B. Tool Y, because a low false-positive rate encourages developer trust and rapid remediation of true positives.  
C. Tool X, after tuning its rules to reduce false positives, because it covers more vulnerability categories.  
D. Neither; static analysis should be abandoned in favor of manual code review.  

Correct Answer: B  
Explanation: Risk-based security prioritizes actionable intelligence. A 45 % false-positive rate erodes developer confidence and wastes scarce resources, leading to “alert fatigue” and ignored true positives. Tool Y’s low noise ratio ensures that each flagged issue is likely real and worth fixing, aligning with the CISSP principle of cost-effective control selection. Tuning (C) is possible but not guaranteed; the question asks which is better “as-is.” Abandoning SAST (D) contradicts defense-in-depth.
Q1. A global e-commerce company is adopting a DevSecOps pipeline that must support 40+ deployments per day. Product owners insist that security gates cannot add more than 5 % overhead to the total build time. The CISO wants every code commit to be accompanied by proof that secrets have not been hard-coded. Which of the following approaches BEST satisfies all stakeholders?  
A. Run a nightly secret-scanning batch job against the whole repo and e-mail results to developers.  
B. Install a pre-commit Git hook that runs a lightweight secrets-detection tool; reject the push if any secret is found.  
C. Require two-person code review for every pull request with a checklist item titled “no secrets in code.”  
D. Perform a full SAST scan (including secret patterns) in the release stage and open Jira tickets for any findings.  

Correct Answer: B  
Explanation: A pre-commit hook executes locally in milliseconds and blocks the commit before it enters the shared history, giving immediate feedback with zero impact on CI clock time. Nightly jobs (A) and release-stage scans (D) discover secrets too late and violate the “fail fast” DevSecOps principle. Manual review (C) is inconsistent and cannot scale to 40+ daily deployments.

Q2. During a secure-code review of a RESTful microservice written in Spring Boot, you discover the following method:

@GetMapping(“/admin/backup”)  
public void runBackup(@RequestParam String path) {  
    Runtime.getRuntime().exec(“/opt/backup.sh “ + path);  
}

The code is already running in production inside a container that operates as USER spring (UID 1000). Which combination of controls MOST effectively reduces the risk of command injection in this specific component?  
A. Input validation using a whitelist of allowed path values plus moving the container to a gVisor sandbox.  
B. Re-write the endpoint to use a safer language (Rust) and re-deploy the entire service.  
C. Upgrade Spring Boot to the latest release and add a WAF rule that blocks the string “&&”.  
D. Set the container’s seccomp profile to “unconfined” so the backup script can run without kernel restrictions.  

Correct Answer: A  
Explanation: Whitelist input validation removes attacker-controlled metacharacters, while gVisor adds a second-layer kernel sandbox that confines the process even if injection occurs. Rewriting in Rust (B) is a long-term strategy but not an immediate fix. A WAF (C) is bypassable and does not protect against encoded payloads. Removing seccomp (D) increases, not decreases, risk.

Q3. A medical-device manufacturer needs to comply with FDA 21 CFR Part 820 (Quality System) while adopting an agile SDLC. The regulation demands “documented evidence that the software meets specified requirements” and “traceability between requirements, code, and tests.” The agile teams work in two-week sprints. Which practice BEST reconciles agility with the regulatory traceability requirement?  
A. Generate a formal requirements specification at the start of the project and freeze it for the entire release.  
B. Maintain a living requirement-to-test matrix in an ALM tool that is updated every sprint; export a snapshot for regulatory submission.  
C. Wait until the final hardening sprint and then create traceability documentation retrospectively.  
D. Replace agile with the V-model to satisfy FDA mandates.  

Correct Answer: B  
Explanation: An ALM matrix updated each sprint provides continuous traceability without sacrificing iterative development. Regulators accept snapshots taken at release boundaries. Freezing requirements (A) or switching to V-model (D) undermines agility, while retroactive documentation (C) is error-prone and audit-failing.

Q4. A fintech startup is building a mobile wallet that stores encrypted card data on the device. The CTO wants to use white-box cryptography to protect the DUKPT key used for contactless payments. The security architect is concerned that white-box implementations can still be compromised. Which compensating control BEST mitigates the residual risk?  
A. Store the white-box key in the Android Keystore hardware-backed keystore and never export it.  
B. Add certificate pinning to the mobile API channel.  
C. Obfuscate the mobile binary and deploy app shielding with runtime application self-protection (RASP).  
D. Require biometric unlock every time the user opens the wallet.  

Correct Answer: C  
Explanation: White-box cryptography is vulnerable to differential fault analysis and side-channel attacks. RASP monitors runtime integrity and can react to tampering or debugger attachment, raising the bar for key extraction. Android Keystore (A) defeats the purpose because the key must reside in software for DUKPT derivation. Pinning (B) protects network data, not local keys. Biometrics (D) authenticate the user, not the app binary.

Q5. A SaaS provider runs a multi-tenant application on AWS. Each tenant’s data is tagged with a customer_id column in a shared PostgreSQL RDS database. The provider wants to add row-level security (RLS) so that a SQL injection bug in the application layer cannot expose another tenant’s data. Which implementation approach is MOST secure and maintainable?  
A. Create one database role per tenant and attach RLS policies that reference current_user; set role after OAuth login.  
B. Keep a single application role and enforce tenant isolation in the WHERE clauses of every query.  
C. Spin up a separate RDS instance for every tenant.  
D. Encrypt each tenant’s rows with a unique column-level key and decrypt in the application.  

Correct Answer: A  
Explanation: RLS policies tied to database roles are enforced inside the engine, making isolation independent of application query construction. Separate instances (C) are operationally expensive and still vulnerable if the same buggy app code connects. WHERE-clause filtering (B) is exactly what injection bypasses. Per-tenant encryption (D) adds key-management complexity without blocking injection-driven denial-of-service.

Q6. During a penetration test, a consultant exploits a deserialization flaw in a Java EE legacy monolith to gain remote code execution. The development team states the codebase is 1.2 MLOC and a full rewrite will take two years. Which short-term remediation strategy provides the BEST risk reduction while the rewrite is underway?  
A. Add a JVM SecurityManager policy that blocks Runtime.exec and network access for the application’s protection domain.  
B. Upgrade the JDK to the latest LTS release and disable the Serialization API completely.  
B. Place the monolith behind an API gateway that strips serialized objects from HTTP requests.  
D. Recompile the code with a static analysis tool and fix only high-severity findings.  

Correct Answer: A  
Explanation: A tightly scoped SecurityManager sandbox confines the attacker even if deserialization succeeds, preventing the observed RCE. Disabling serialization (B) breaks legitimate session clustering. An API gateway (C) cannot inspect binary RMI or JBoss remoting protocols. Static analysis (D) is helpful but does not guarantee all deserialization flaws are found.

Q7. A CI/CD pipeline uses containerized build agents in Kubernetes. Build pods need credentials to pull source code from a private GitHub org and to push Docker images to Amazon ECR. Which approach MINIMIZES the lifetime of these credentials while still allowing unattended builds?  
A. Store GitHub PAT and AWS keys in the pipeline’s “secret” store and rotate them every 90 days.  
B. Mount a Kubernetes ServiceAccount token into the pod; use OIDC federation so GitHub and AWS issue short-lived tokens (15 min) bound to the running pod.  
C. Embed the secrets in the container image during the docker build stage and clean them up with an ENTRYPOINT script.  
D. Pass secrets through environment variables set in the pipeline UI; enable “mask passwords” plugin.  

Correct Answer: B  
Explanation: OIDC federation lets GitHub and AWS act as token issuers, delivering 15-minute credentials that expire automatically and are not stored anywhere. Long-lived PATs (A) remain valid if leaked. Embedding secrets (C) leaves them in image layers. Environment variables (D) are visible in /proc and build logs.

Q8. A software vendor is adopting the NIST Secure Software Development Framework (SSDF). The secure-operations (PS) practice requires “verification that the software behaves as expected when deployed.” The vendor ships firmware updates to Internet-connected industrial gateways that have no local console. Which verification technique BEST satisfies SSDF PS-3 while remaining practical in the field?  
A. Require customers to run a checksum of the firmware file before flashing.  
B. Include a cryptographically signed attestation report that the bootloader sends to a cloud monitoring service after each boot.  
C. Publish SHA-256 hashes on the vendor web site.  
D. Add a “–dry-run” flag to the flashing tool that simulates the update without writing flash.  

Correct Answer: B  
Explanation: A signed attestation (measured boot log, TPM quote, etc.) proves that the expected firmware is running and has not been rolled back, satisfying SSDF’s runtime verification requirement. Checksums (A, C) only validate the file pre-installation. Dry-run (D) does not verify behavior on actual hardware.

Q9. A large bank is building an open-banking API that exposes GET /accounts/{id}/transactions. The API gateway already performs OAuth 2.0 client-credentials validation. Security testing shows that an authorized partner can substitute any {id} and retrieve other customers’ transactions. Which secure-coding practice would have PREVENTED this vulnerability during development?  
A. Implementing rate-limiting at the gateway layer.  
B. Adding an additional API key header that is unique per partner.  
C. Enforcing server-side authorization that compares the JWT scope claim to the {id} parameter.  
D. Encrypting the {id} parameter in transit using TLS 1.3.  

Correct Answer: C  
Explanation: The flaw is broken object-level authorization (BOLA). Validating that the JWT scope or claim contains the exact customer_id being requested closes the gap. Rate-limiting (A) and extra keys (B) do not stop horizontal privilege escalation. TLS (D) protects on the wire but not from an already-trusted client.

Q10. A team is evaluating two static analysis offerings for a C/C++ embedded project:  
Tool X: 8 % false-positive rate, 15 min scan time, limited to MISRA-C rules.  
Tool Y: 2 % false-positive rate, 4 h scan time, full path coverage with taint analysis.  
The build pipeline currently compiles 20 firmware variants nightly, and the build farm has 32 cores idle after 22:00. Which tool and deployment model BEST balances security value and pipeline performance?  
A. Run Tool X on every pull request; schedule Tool Y as a nightly job only for variants that changed.  
B. Run Tool Y on every pull request and accept the 4-hour wait because accuracy is paramount.  
C. Replace both with a dynamic fuzzer that executes the firmware in QEMU.  
D. Run Tool X nightly; skip static analysis on pull requests to keep developer velocity.  

Correct Answer: A  
Explanation: Using the fast, low-noise tool at the left-shift (PR) stage gives immediate feedback, while the high-precision but slow tool runs offline when CPU capacity is abundant. Running Tool Y per PR (B) would bottleneck merges. Fuzzing (C) is complementary but does not replace static analysis for MISRA compliance. Skipping PR scans (D) violates the “fail early” principle.
Q1. A global e-commerce company is adopting a DevSecOps model. The CISO wants to ensure every pull request to the “main” branch is automatically assessed for security defects before human code review.  
A. Configure static application security testing (SAST) in the CI pipeline gated by a quality gate that fails the build on high-severity findings.  
B. Run dynamic application security testing (DAST) immediately after each microservice is deployed to staging.  
C. Require two-person manual code review for every pull request and document the review in the ticketing system.  
D. Schedule quarterly third-party penetration tests and block releases until high findings are retested.  

Correct Answer: A  
Explanation: DevSecOps demands “shift-left” security that is automated, fast, and developer-centric. SAST analyzes source code or compiled artifacts without executing the program and can run in milliseconds inside the CI pipeline, gating the merge via quality gates. DAST (B) occurs too late; manual review (C) is human-intensive and inconsistent; quarterly pen tests (D) are point-in-time and cannot block every pull request.

---

Q2. A healthcare SaaS provider allows patients to upload clinical images. The development team wants to prevent attackers from embedding malicious JavaScript inside an uploaded JPEG comment field that is later reflected in an administrative dashboard.  
A. Validate that the uploaded file extension is .jpg or .png.  
B. Re-encode every image with a lossy algorithm to strip metadata and serve the re-encoded file.  
C. Store uploads outside the web root and return them through a Content-Disposition: attachment header.  
D. Configure the browser to set X-Content-Type-Options: nosniff.  

Correct Answer: B  
Explanation: Re-encoding (transcoding) removes all extraneous metadata—including comment fields—while preserving the visual image. Extension checks (A) are trivial to bypass. Serving outside web root (C) and nosniff (D) mitigate other risks (e.g., direct rendering or MIME sniffing) but do not neutralize stored XSS inside metadata.

---

Q3. A bank is building an Angular SPA that invokes RESTful microservices. The security architect insists on adding the “secure” flag to the HTTP-only session cookie, but the QA team reports that some customers still transmit it over plaintext. Which architectural control will BEST mitigate this residual risk?  
A. Register the cookie domain with the HSTS preload list and enforce TLS 1.3 at the edge.  
B. Encrypt the cookie value with AES-256 before setting it.  
C. Add the SameSite=strict attribute to prevent cross-site delivery.  
D. Implement OAuth 2.0 mutual TLS sender-constrained access tokens instead of cookies.  

Correct Answer: A  
Explanation: HSTS (especially preloaded) instructs conforming browsers to upgrade every plaintext request to HTTPS before any HTTP request is sent, eliminating accidental cleartext transmission. Encrypting the cookie (B) does not stop network sniffing; SameSite (C) addresses CSRF, not transport; replacing cookies with mTLS tokens (D) is a major refactor and does not solve the immediate transport issue.

---

Q4. A start-up uses a serverless (Lambda) architecture. A developer inadvertently hard-coded AWS access keys in a public GitHub repo. Within 10 minutes, an attacker used the keys to spin up 500 EC2 instances for crypto-mining, costing USD 8,000. Which preventative control would have MOST effectively stopped the exploit?  
A. Rotate IAM access keys every 24 hours via an automated Lambda job.  
B. Attach an IAM permissions boundary that denies ec2:RunInstances regardless of the user or key.  
C. Enable AWS CloudTrail and configure billing alerts.  
D. Store secrets in AWS Systems Manager Parameter Store and reference them via an environment variable encrypted with KMS.  

Correct Answer: B  
Explanation: A permissions boundary acts as an IAM “sandbox,” capping the maximum permissions even if credentials leak. Denying ec2:RunInstances would have neutered the attacker immediately. Rotation (A) shortens exposure but does not prevent exploitation within the window. CloudTrail and billing alerts (C) are detective, not preventative. Secure secret storage (D) is good practice but does not constrain what legitimate (or stolen) credentials can do.

---

Q5. A multinational firm is selecting a static analysis tool for a 15-year-old C/C++ codebase (three million LOC) that is built nightly on Windows, Linux, and z/OS. The security team must satisfy both MISRA-C compliance and the ability to trace findings back to the original developer commit.  
A. Choose a SaaS SAST engine that only supports Java and .NET but offers excellent OWASP coverage.  
B. Deploy an on-premise SAST scanner with build-wrapper agents for each platform and bidirectional ALM integration into the existing SVN and Git repos.  
C. Rely on compiler warnings with the –Wall –Wextra flags and export results to a CSV file.  
D. Run a weekly source-code grep for strcpy and sprintf and manually review hits.  

Correct Answer: B  
Explanation: Legacy C/C++ and multi-platform builds require an engine that understands each compiler’s dialect and can instrument the build (via build wrappers). On-premise deployment keeps proprietary source internal, while ALM integration maps findings to commits, enabling accountability and remediation tracking. SaaS lacking C/C++ support (A) is useless. Compiler warnings (C) and grep (D) are incomplete and non-scalable.

---

Q6. A mobile payment app uses certificate pinning inside the Android APK. The release engineering team wants to avoid emergency app-store re-submissions when a backend certificate renews. Which approach BEST balances security with operational agility?  
A. Embed only the public key hash (not the full certificate) and rotate it through an over-the-air configuration file signed with the company’s offline CA.  
B. Remove pinning and rely solely on the OS trusted store.  
C. Pin the entire certificate chain including the root CA.  
D. Issue 10-year self-signed certificates for all APIs.  

Correct Answer: A  
Explanation: Pinning the public key hash (Subject Public Key Info, SPKI) survives certificate renewal as long as the key pair is reused, while still allowing controlled rotation via an authenticated config channel. Removing pinning (B) re-exposes the app to rogue CAs. Pinning to the root (C) provides little value (any cert issued by that root is trusted), and 10-year certs (D) violate CAB forum requirements and increase key-compromise impact.

---

Q7. During a Scrum sprint, product management requests a last-minute feature that introduces a new REST endpoint. The secure-code review indicates the endpoint is vulnerable to IDOR (Insecure Direct Object Reference). The sprint ends in two days and blocking the release would breach a contractual deadline. Which risk-management response is MOST appropriate?  
A. Accept the risk, document it in the risk register, and schedule remediation in the next sprint.  
B. Apply a Web Application Firewall rule that validates session ownership for the affected URI pattern and defer full code fix to the next sprint.  
C. Cancel the release, pay the contractual penalty, and fix the code immediately.  
D. Promote the finding to a critical bug and extend the sprint until the code is fixed and retested.  

Correct Answer: B  
Explanation: A targeted virtual-patch via WAF provides immediate, reversible protection without breaking the sprint timeline, aligning with “reduce” (mitigate) rather than “accept” (A) or “avoid” (C/D). Acceptance (A) leaves customers exposed; canceling or extending (C/D) may be idealistic but could violate business constraints and is not the “most appropriate” given a viable compensating control.

---

Q8. A software vendor is pursuing ISO 27034 certification. The auditor asks for evidence that the organization has implemented “control A.10.3 – Secure Coding Practices” across all development teams. Which artifact BEST demonstrates compliance?  
A. A Confluence wiki page titled “Secure Coding Guidelines” last updated three years ago.  
B. A centrally enforced IDE plugin that flags non-compliant code in real time with dashboards showing 95 % adoption and remediation metrics.  
C. A one-time classroom training slide deck delivered to new hires.  
D. Penetration-test reports showing no high-severity vulnerabilities in the past year.  

Correct Answer: B  
Explanation: ISO 27034 expects continuous, measurable implementation of security controls within the application lifecycle. An enforced IDE plugin with metrics provides ongoing evidence that secure-coding rules are embedded in day-to-day engineering, not merely documented (A) or trained once (C). Pen-test absence (D) is circumstantial and could result from scope limitations or tester skill.
