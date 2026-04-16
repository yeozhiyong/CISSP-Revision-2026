Q1. A multinational bank is designing a new public-key infrastructure to support digitally-signed trade-finance documents that must remain legally valid for 15 years. The chief cryptographer proposes using 2048-bit RSA with SHA-256 today and re-signing all documents with longer keys immediately before the current signature certificate expires. Which of the following is the MOST important architectural concern with this plan?  
A. SHA-256’s 256-bit output will not provide adequate collision resistance for 15-year archival.  
B. RSA key lengths below 3072-bit will be deprecated by NIST in the next two years, invalidating future signatures.  
C. Re-signing breaks the original trusted time stamp and may not satisfy regulators that the first signature covered the full 15-year period.  
D. The overhead of re-signing multi-gigabyte document repositories every three years will exceed available HSM throughput.  

Correct Answer: C  
Explanation: Regulatory and evidentiary rules require the ORIGINAL signature to remain valid for the entire retention period; re-signing creates a new signature whose time stamp is later than the transaction date, destroying non-repudiation evidence. A is wrong because SHA-256 still gives ≈128-bit collision resistance, sufficient for 15 years. B is wrong because NIST already lists 2048-bit RSA as acceptable through 2030, not “next two years.” D is a valid operational issue but not the most important security-architecture flaw.

Q2. A cloud SaaS provider stores customer backups in Amazon S3 and protects them with SSE-S3 (server-side encryption with Amazon-managed keys). A new compliance requirement mandates that the provider must be able to demonstrate that data could not be decrypted even if AWS became malicious. Which control should be added FIRST?  
A. Enable S3 bucket versioning and MFA delete.  
B. Switch to SSE-KMS with customer-managed CMKs imported into AWS KMS and then turn on KMS key deletion protection.  
C. Encrypt backups on-premise with AES-256 under a hardware-root-of-trust before uploading to S3.  
D. Require AWS KMS to store the CMKs in a FIPS-140-2 Level 3 HSM.  

Correct Answer: C  
Explanation: Only client-side encryption keeps keys totally outside the cloud provider’s control, satisfying the “even if AWS becomes malicious” requirement. B still leaves AWS able to use the CMK. A is an availability control, not confidentiality. D does not change AWS’s ability to use the key.

Q3. During a secure-boot review of an embedded point-of-sale device, the security architect discovers the vendor’s UEFI firmware accepts firmware-signed updates using 1024-bit RSA and SHA-1. Which attack is MOST likely to succeed against this device?  
A. Collision attack on the SHA-1 firmware hash allowing malicious firmware to load with a valid RSA signature.  
B. Timing attack on the 1024-bit RSA decryption routine that recovers the device’s private update key.  
C. Fault-injection attack that downgrades the firmware to an older, vulnerable version still signed with SHA-1.  
D. Birthday attack against the 1024-bit RSA modulus that factorises the public key in tractable time.  

Correct Answer: D  
Explanation: 1024-bit RSA is within reach of nation-state factorisation; once the modulus is factored, an attacker can sign any malicious firmware. A is wrong because SHA-1 collisions do not break RSA signatures—an attacker still needs to forge the RSA signature. B is a side-channel but much harder to exploit remotely. C is possible but not the most likely given the weak RSA key length.

Q4. A company is implementing a zero-trust network architecture. All east-west traffic between micro-services inside the same Kubernetes cluster must be mutually authenticated and encrypted. Which technology BEST fulfills the requirement without changing application code?  
A. Overlay network using VXLAN with AES-GMAC.  
B. Service mesh (e.g., Istio) with mTLS between sidecar proxies.  
C. IPSec tunnels between each worker node.  
D. TLS passthrough on an ingress controller.  

Correct Answer: B  
Explanation: A service mesh injects sidecars that perform mutual TLS transparently to the workload. A only gives network segmentation, not mutual authentication. C encrypts node-to-node but not pod-to-pod. D terminates TLS at the edge, not inside the cluster.

Q5. A defence contractor wants to field a drone swarm that must continue cryptographic operations even when individual drones are captured. Which property should the symmetric-key distribution scheme PRIMARILY exhibit?  
A. Perfect forward secrecy.  
B. Key escrow.  
C. Split-knowledge & threshold cryptography.  
D. Post-quantum key encapsulation.  

Correct Answer: C  
Explanation: Threshold cryptography lets any t-of-n drones sign or decrypt, so capture of fewer than t drones reveals nothing. A is about ephemeral keys, not captured devices. B is the opposite of the desired goal. D is irrelevant to the capture scenario.

Q6. An organisation runs a legacy web application that can only support static 56-bit DES keys for TLS. Compliance requires “adequate cryptographic strength.” Which compensating control is MOST acceptable from a risk-management perspective?  
A. Place the application behind a TLS 1.3 reverse proxy that re-encrypts traffic to the backend using 128-bit AES.  
B. Tunnel all browser connections through an IPsec VPN using AES-256, then allow plain HTTP on the LAN segment.  
C. Accept the risk and document it in the risk register because DES is still resistant to brute force for short sessions.  
D. Upgrade the application to support 3DES-168.  

Correct Answer: A  
Explanation: A modern reverse proxy offloads strong cryptography to the client while speaking legacy crypto only on the trusted backend link. B creates an extra VPN hurdle for users and still leaves internal traffic unencrypted. C ignores compliance. D may be impossible (legacy binaries) and 3DES is also deprecated.

Q7. A smart-card OS implements RSA signature generation in a secure element that is certified FIPS 140-2 Level 3. The card emits the exact same byte pattern for every 1024-bit RSA signature of the same message. Which security principle is MOST clearly violated?  
A. Collision resistance.  
B. Deterministic encryption.  
C. Key-ceremony integrity.  
D. Semantic security / randomness.  

Correct Answer: D  
Explanation: RSA signatures must use a random padding scheme (e.g., PSS); deterministic output leaks that the same message was signed, violating semantic security and enabling some attacks. A is about hash functions. B is a non-issue for signatures. C is unrelated.

Q8. A company is selecting a block-cipher mode for encrypting large video files stored at rest on S3. The files must be randomly accessed by byte range without decrypting the entire object. Which mode is the BEST choice?  
A. CBC with random IV per object.  
B. CTR with unique nonce per object.  
C. GCM with incremental 96-bit IV per 4-KiB chunk.  
D. XTS with 128-bit sector tweaks aligned to 4 KiB boundaries.  

Correct Answer: D  
Explanation: XTS is designed for storage devices supporting random read/write and hides patterns within a sector. CTR (B) and GCM (C) require nonce management and can be dangerous if partial overlaps occur. CBC (A) cannot be randomly decrypted in parallel.

Q9. A manufacturer ships IoT gateways with an ARM TrustZone secure world that stores a device-unique private key in e-fuses and a public key certificate signed by the manufacturer’s CA. Which step is MOST critical to prevent cloned devices from joining the service?  
A. Disable the JTAG interface in the insecure world.  
B. Enable Trustzone’s secure boot to verify the kernel image signature.  
C. Perform mutual TLS authentication using the device certificate and check revocation online during onboarding.  
D. Store the CA public key in the gateway’s TPM NVRAM.  

Correct Answer: C  
Explanation: Only online certificate verification with revocation checking prevents cloned devices with valid-looking certificates from authenticating. A and B protect the firmware but do not detect cloned keys. D is pointless because the CA public key is already public.

Q10. A quantum-computing start-up wants to protect its long-term research data (10+ years) against “harvest-now-decrypt-later” attacks. Data is exchanged between on-prem data centres and AWS VPCs. Which combination of controls provides the STRONGEST defence today?  
A. Use classical ECDH P-384 for key exchange and AES-256-GCM for bulk data, then re-encrypt archives annually.  
B. Replace ECDH with CRYSTALS-KYBER (NIST Round-3 KEM) and use AES-256-GCM; store encrypted data as-is.  
C. Deploy IPsec with RFC 8784 post-quantum preshared keys and continue using AES-256-GCM.  
D. Layer classical TLS 1.3 with pre-shared AES-256 keys plus periodic key rotation every 24 h.  

Correct Answer: B  
Explanation: KYBER provides confidential key exchange even against future quantum adversaries, and AES-256 is currently considered quantum-resistant (Grover’s halves the key space to 128-bit, still safe). A keeps classical key exchange vulnerable. C only protects the IKE/IPsec tunnel, not object-level storage. D still uses classical key exchange for the initial TLS handshake.
Q1. A multinational bank is designing a new cryptographic key-management system for retail-payment HSMs. Regulatory guidance requires that keys used to encrypt PIN blocks are never shared in cleartext outside the HSM boundary, yet the bank must be able to rotate keys monthly without dispatching technicians to every data-center. Which key-block format and distribution method best satisfies the requirement?  
A. DUKPT with initial BDK injected at manufacture, then encrypted under LMK inside each HSM  
B. TR-31 key block signed by the bank’s root CA and transported offline on smart cards  
C. X9.24-2 Symmetric Key Bundle encrypted under the old key and pushed over the WAN  
D. Raw 3DES key components written to three separate smart cards that must be reunited onsite  

Correct Answer: B  
Explanation: TR-31 binds key material with its usage attributes and a CA signature, allowing secure remote distribution while preventing cleartext exposure. DUKPT (A) never shares future keys, so rotation is impossible. X9.24-2 (C) still encrypts under the old key, violating the “never cleartext” mandate if the old key is compromised. Raw components (D) require onsite presence, defeating the “no dispatch” goal.

Q2. During a cloud migration, an e-commerce company wants to maintain end-to-end TLS 1.3 from browser to Docker container without decrypting at the load balancer. The containers run on spot instances that scale every minute. Which architecture preserves confidentiality and integrity while still allowing the SOC to inspect traffic for OWASP Top-10 attacks?  
A. Deploy a cloud-native layer-7 WAF with TLS passthrough and mirror traffic to IDS sensors  
B. Terminate TLS on the load balancer, re-encrypt to containers, and feed cleartext to WAF  
C. Use mutual TLS with client certificates and embed an agent in each container that streams decrypted traffic to a SIEM  
D. Insert a service-mesh sidecar that terminates TLS, sends copy to WAF, then re-encrypts to local container  

Correct Answer: D  
Explanation: A sidecar proxy (e.g., Envoy) can terminate TLS, mirror or log decrypted payloads for inspection, and open a new TLS session to the local container, meeting both encryption and visibility goals. Passthrough (A) prevents inspection. Full termination (B) breaks end-to-end confidentiality. Client certs (C) do not give the SOC visibility into server-side payloads.

Q3. A defense contractor is evaluating CPU hardware for a classified system that processes both TOP SECRET and UNCLASSIFIED data on the same physical blade. Which hardware feature is MOST critical for preventing a malicious VM running UNCLASSIFIED workloads from extracting keystrokes from a TOP SECRET VM via a shared cache timing side channel?  
A. Intel MPK (Memory Protection Keys)  
B. AMD SEV-ES (Secure Encrypted Virtualization–Encrypted State)  
C. Intel CET (Control-flow Enforcement Technology)  
D. ARM Pointer Authentication  

Correct Answer: B  
Explanation: SEV-ES encrypts the entire VM memory space including register state, making cache-granular timing attacks far harder. MPK (A) is per-process, not VM-wide. CET (C) and PAC (D) defend against ROP/JOP, not side channels.

Q4. A smart-city IoT gateway collects 4 KB sensor readings every 5 s from 10 000 devices. Each reading must be authenticated, non-repudiable, and verifiable by third-party auditors, yet battery life is constrained. Which cryptographic approach best balances security and power?  
A. ECDSA signatures over P-256 on the device plus ECDH session keys  
B. HMAC-SHA256 keyed with a unique 256-bit device secret stored in fused ROM  
C. AES-GCM 128-bit with 96-bit IV derived from monotonic counter  
D. Ed25519 signatures computed on the gateway after aggregating cleartext data  

Correct Answer: A  
Explanation: ECDSA on a low-power device (e.g., ARM Cortex-M with crypto accelerator) gives strong non-repudiation with 64-byte signatures, far smaller than RSA and feasible for 4 KB payloads. HMAC (B) lacks non-repudiation. AES-GCM (C) provides only confidentiality+integrity, not third-party verifiability. Gateway-level signing (D) removes device-level non-repudiation.

Q5. A zero-trust vendor claims their SDP controller can “hide” TCP services until mutual TLS is complete. During a PoC, the client’s vulnerability scanner still discovers open port 443 on the gateway. Which control BEST explains why the scanner’s finding does NOT invalidate the claim?  
A. The gateway responds with a TLS handshake that reveals no application-layer banners  
B. Port 443 must remain open to initiate the mutual TLS bootstrap required by the SDP specification  
C. The scanner is whitelisted by the controller to simplify PoC troubleshooting  
D. A secondary firewall rule blocks SYN-ACK for any source not presenting a valid SPA packet  

Correct Answer: B  
Explanation: SDP “hiding” refers to application services, not the TLS port itself; the controller must expose 443 to begin mutual TLS. Once TLS completes, the controller issues tokens for micro-tunnels. Option A is true but secondary. Whitelisting (C) and SPA (D) are deployment choices, not normative SDP behavior.

Q6. A company is selecting a FIPS-140-3 level for a SaaS KMS that stores customer master keys. Regulators require that any tamper attempt zeroizes keys, and that the vendor can demonstrate compliance without shipping hardware to each customer site. Which level and implementation model is MOST appropriate?  
A. Level 2 with a tamper-evident seal on a cloud-hosted HSM cluster  
B. Level 3 with a multi-tenant HSM operated under the vendor’s physical control  
C. Level 4 with SDN-controlled power cut-off to destroy keys if intrusion detected  
D. Level 1 with software-only module running inside a confidential-computing VM  

Correct Answer: B  
Explanation: Level 3 mandates tamper detection and zeroization while still allowing multi-tenant cloud HSMs under provider control. Level 2 (A) only requires tamper evidence, not response. Level 4 (C) needs environmental failure protection unrealistic in cloud. Level 1 (D) offers no tamper response.

Q7. An organization is implementing a new PKI for 5G network slices. Root CA is kept offline; subordinate CAs issue short-lived certs every 6 h. Which validation method prevents relying parties from accepting a revoked slice certificate during the 6-hour window while avoiding OCSP lookup latency in the 5G user plane?  
A. Staple OCSP responses with a NextUpdate 12 h in the future  
B. Embed a 1-hour CRL DP and require devices to cache the CRL every 60 min  
C. Use OCSP-Must-Staple with a 15-minute response lifetime and mandate stapling in TLS handshake  
D. Switch to raw public keys and pin the sub-CA cert in the device firmware  

Correct Answer: C  
Explanation: Must-Staple plus short-lived responses forces the slice to prove non-revocation at handshake time, closing the 6-hour window without extra user-plane latency. Long-lived staples (A) still allow 12-hour exposure. CRL (B) adds download latency. RPK (D) eliminates revocation altogether, violating the requirement.

Q8. A microservice architecture handles credit-card tokens. The security team wants to ensure that even if an attacker gains code execution on the tokenization service, they cannot recover PANs without also compromising a second control. Which design BEST implements this objective?  
A. Split-key format-preserving encryption: half-key in HSM, half in microservice config map  
B. Token vault stored in an AMD SEV-encrypted VM whose attestation key is held in a separate HSM  
C. AES-CBC encryption with IV stored in a different database shard  
D. Hash-based PAN index using PBKDF2 with 100 000 iterations and salt in code repo  

Correct Answer: B  
Explanation: SEV-encrypted memory plus external attestation creates a two-factor barrier: the attacker needs both VM memory and HSM approval to decrypt the vault. Split key (A) still allows offline brute-force if config map leaks. IV separation (C) does not encrypt the key. PBKDF2 (D) is irreversible, so tokens could not be reversed for chargebacks.

Q9. A satellite internet provider uses a proprietary protocol over UDP for customer terminals. They need to add confidentiality and integrity without increasing packet size by more than 32 bytes per 256-byte payload. Which construct is MOST appropriate?  
A. ChaCha20-Poly1305 with 96-bit nonce and 32-bit ICV truncated to 32 bytes total  
B. AES-256-GCM with 96-bit IV and 128-bit tag, then compress tag to 64 bits  
C. SipHash-2-4 for integrity and XOR with a rotating 32-bit OTP for confidentiality  
D. HKDF-expanded AES-CTR for encryption and HMAC-SHA256-32 for integrity  

Correct Answer: A  
Explanation: ChaCha20-Poly1305 produces only 16 bytes of tag; with 12-byte nonce the overhead is 28 bytes, under the 32-byte ceiling. Truncating GCM tag (B) weakens integrity below 96 bits. SipHash+XOR (C) is not semantically secure. CTR+HMAC (D) needs 32-byte MAC alone, exceeding budget.

Q10. A manufacturer ships embedded controllers that verify firmware updates using ECDSA signatures. A new EU regulation mandates that updates remain valid for 15 years even if the original signing algorithm becomes broken. Which long-term signature strategy BEST satisfies the rule while minimizing flash usage (add <2 KB)?  
A. Embed an ECDSA signature plus a 256-bit hash of the future replacement public key; switch algorithm when needed  
B. Use XMSS (hash-based signatures) with 20-byte WOTS+ public keys cached in ROM  
C. Apply PKCS#7 with RSA-4096 and 512-byte signature padding  
D. Dual-sign the image with both ECDSA-P256 and Ed25519, storing two 64-byte signatures  

Correct Answer: D  
Explanation: Two 64-byte signatures total 128 bytes (<2 KB) and provide crypto-agility: if one algorithm is broken, the other still validates. Hash-of-future-key (A) requires an extra update step and does not sign the image with the new algorithm. XMSS (B) has 1–2 kB public keys plus large signatures. RSA-4096 (C) alone is 512 bytes but offers no fallback.
Q1. A mobile-payment start-up is designing a new architecture that must allow micro-payments (≤ $0.50) to be approved even if the back-end is temporarily unreachable from the point-of-sale terminal. Which security engineering principle BEST supports the decision to cache a small, digitally signed “spending balance” on the terminal itself?  
A. Economy of mechanism  
B. Open design  
C. Separation of duties  
D. Psychological acceptability  

Correct Answer: A  
Explanation: “Economy of mechanism” (keep the design as simple and small as possible) justifies storing only the minimal, signed data object needed to authorise micro-payments while offline. Open design (B) is about publishing algorithms—irrelevant here. Separation of duties (C) addresses split authorization, not offline resilience. Psychological acceptability (D) concerns user convenience, not offline security logic.

--------------------------------------------------------------------
Q2. While reviewing a vendor’s FIPS 140-3 submission you see the statement: “The hardware cryptographic module automatically clears all intermediate key material when power is removed, but the firmware is not required to perform an explicit zeroization routine.” For which FIPS 140-3 security level is this acceptable?  
A. Level 1  
B. Level 2  
C. Level 3  
D. Level 4  

Correct Answer: A  
Explanation: Level 1 only requires the use of approved algorithms; explicit zeroization or tamper-evidence is not mandated. Levels 2-4 progressively require stronger key-zeroization, tamper-evidence, or tamper-response, so the absence of an explicit zeroization routine would fail at those levels.

--------------------------------------------------------------------
Q3. A company wants to replace its legacy SHA-1 HMAC-based one-time-password tokens. The new tokens must remain offline, cost under $8 each, and resist attacks even if the attacker gains physical possession of the token for several days. Which of the following token technologies BEST satisfies these constraints?  
A. TOTP based on SHA-256 with a secure element  
B. Event-based HOTP with a user-programmable EEPROM  
C. U2F token with ECDSA private key stored in non-exportable memory  
D. SMS-delivered OTP with PKI-based mutual authentication  

Correct Answer: C  
Explanation: U2F tokens contain an ECC private key that cannot be extracted, resist replay and phishing, and remain under $8 in volume. SHA-256 TOTP (A) still exposes shared symmetric secrets to extraction. HOTP with EEPROM (B) allows key cloning. SMS (D) is online, not offline, and more expensive.

--------------------------------------------------------------------
Q4. An IoT gateway performs firmware updates by verifying an RSA-2048 signature on the new image. To save bandwidth, the vendor ships only the 256-byte signature instead of signing the entire multi-megabyte image with RSA. Which cryptographic construct MOST likely enables this shortcut while preserving authenticity?  
A. RSA blind signature  
B. RSA-PSS with MGF1  
C. Hash-based Merkle tree root signed by RSA  
D. Optimal Asymmetric Encryption Padding (OAEP)  

Correct Answer: C  
Explanation: Signing a Merkle-tree root (or simply signing the hash of the firmware) allows a 256-byte RSA signature to cover a large image; the gateway recomputes the hash/tree and verifies the signature. Blind signatures (A) are for anonymity. RSA-PSS (B) is a padding scheme, not a bandwidth saver. OAEP (D) is for encryption, not signatures.

--------------------------------------------------------------------
Q5. During a security architecture review of a containerized micro-service platform you discover that every container runs with the same Linux UID 0 inside its own user namespace, but the host maps that UID to an unprivileged host UID (>100000). The DevOps team claims this is “rootless” and safe. Which attack vector BEST refutes that claim?  
A. Kernel privilege escalation via a compromised container that escapes its user namespace  
B. Cross-site request forgery against the container registry API  
C. Brute-force cracking of the container image’s compressed hash  
D. BGP hijack of the cluster’s overlay network prefixes  

Correct Answer: A  
Explanation: UID mapping mitigates but does not eliminate kernel bugs that allow a process running as UID 0 in the container to escape its namespace and gain real root on the host. CSRF (B) and BGP hijack (D) are network-layer, not container breakout. Brute-forcing hashes (C) is irrelevant to runtime privilege.

--------------------------------------------------------------------
Q6. A defence contractor must transmit 2.4 Gb/s of AES-256-GCM encrypted video from an airborne drone with less than 5 ms added latency. The existing FPGA already implements the AES core, but the 1 Gb/s Ethernet MAC becomes the bottleneck. Which security architecture change BEST solves the throughput requirement while staying within the same FPGA?  
A. Replace AES-256-GCM with ChaCha20-Poly1305 in the same FPGA fabric  
B. Add a second 1 Gb/s MAC and bond the two interfaces  
C. Upgrade to a 10 Gb/s MAC IP core instantiated in the same FPGA  
D. Offload encryption to a separate CPU and keep the 1 Gb/s MAC  

Correct Answer: C  
Explanation: The bottleneck is link speed, not cipher speed; upgrading to 10 Gb/s MAC inside the same FPGA removes the Ethernet limit while keeping low latency. ChaCha20 (A) won’t help a 1 Gb/s MAC. Bonding (B) only yields ~2 Gb/s and doubles latency. Offloading to CPU (D) adds >5 ms context-switch latency.

--------------------------------------------------------------------
Q7. A hospital is evaluating two full-disk encryption products for Windows laptops that store PHI. Product A uses TPM 1.2 with only the PCR-0 (BIOS firmware hash) sealed key; Product B uses TPM 2.0 with PCR-0, PCR-1 (platform vendor code), and PCR-7 (SecureBoot state) and additionally requires a 6-digit PIN. From a pure security-architecture standpoint, which product provides stronger assurance against an evil-maid attack?  
A. Product A, because fewer PCRs simplify attestation and reduce error rates  
B. Product B, because multi-PCR attestation plus PIN enforces trusted boot and user knowledge factors  
C. Both are equivalent since TPM 1.2 and 2.0 use the same RSA key lengths  
D. Product A, because TPM 1.2 is certified under Common Criteria EAL 4+ whereas TPM 2.0 is not  

Correct Answer: B  
Explanation: Multi-PCR attestation plus PIN binds decryption to both platform integrity and user knowledge, thwarting attackers who re-flash BIOS or boot an unsigned OS. Product A’s single PCR-0 can be replayed after re-sealing. TPM version key length (C) is irrelevant, and EAL statement (D) is false—both can be certified.

--------------------------------------------------------------------
Q8. A public certificate authority is creating a new root CA that must remain valid for 25 years but wants to reduce the impact of a future cryptographic break against RSA-4096. Which key-management technique BEST aligns with NIST SP 800-57 guidance for long-lived trust anchors?  
A. Generate a single RSA-4096 root key and publish a 25-year CRL expiry  
B. Generate an RSA-4096 root key and an offline ECDSA P-521 standby key, with the root certificate containing both public keys  
C. Use a 2048-bit RSA key rolled every 3 years via re-issuance of the root  
D. Store the root private key in an HSM and delete the public key from all repositories  

Correct Answer: B  
Explanation: Dual-key root with algorithms of different mathematical problems (RSA vs ECC) provides crypto-agility without requiring immediate rollover. Single long-lived RSA (A) has no agility. 2048-bit (C) is below current best practice for 25-year roots. Deleting the public key (D) breaks the chain of trust.

--------------------------------------------------------------------
Q9. A smart-city command centre collects 30 000 events/second from roadside sensors. The architecture buffers events in Kafka, then a stream processor computes SHA-256 hashes and writes them to an immutable log for non-repudiation. An auditor warns that the design lacks “proof of integrity order.” Which additional cryptographic component BEST satisfies the auditor at the lowest performance cost?  
A. Digitally sign every individual event with the sensor’s RSA private key  
B. Compute a running SHA-256-chain (each hash includes the previous hash) and sign the chain tip every minute  
C. Replace SHA-256 with SHA-3-512 to increase collision resistance  
D. Encrypt each event with AES-GCM using a 96-bit IV  

Correct Answer: B  
Explanation: A running hash chain (similar to blockchain linking) provides ordered integrity; periodic signing of the tip keeps asymmetric operations low (1 sign per minute vs 30 000/sec). Individual signing (A) is computationally prohibitive. SHA-3 (C) does not address order. AES-GCM encryption (D) provides confidentiality, not ordered non-repudiation.

--------------------------------------------------------------------
Q10. A software company is adopting the Biba integrity model for its build pipeline. The security team labels source code “LOW,” compiled binaries “HIGH,” and the build server “MEDIUM.” Which action is explicitly FORBIDDEN under Biba strict *-property?  
A. A developer labelled LOW writes new source code  
B. The MEDIUM build server reads LOW source code  
C. The MEDIUM build server writes HIGH binaries  
D. A HIGH binary is downloaded by a LOW-end user device  

Correct Answer: C  
Explanation: Biba *-property (no write-up) forbids a MEDIUM subject from writing to a HIGH object. Reading LOW (B) is allowed (simple security property). LOW writing code (A) is a subject write to LOW object—allowed. HIGH downloaded to LOW device (D) is a read-down—also allowed.
Q1. A global SaaS provider is designing a green-field multi-tenant platform that must keep each tenant’s cryptographic keys totally isolated even if the hypervisor is compromised. The physical hosts already support Intel SGX. Which architectural choice best satisfies the requirement while minimizing operational friction?  
A. Store each tenant’s private keys in the OS-level keyring that is protected by file-system ACLs.  
B. Generate and seal all tenant keys inside individual SGX enclaves that never expose cleartext outside the enclave.  
C. Run the key-management service inside a FIPS-140-2-level-2 HSM that is shared by all tenants and accessed through a PKCS#11 interface.  
D. Encrypt every tenant’s key blob with a master key stored in the cloud provider’s default KMS and rotate the master quarterly.  

Correct Answer: B  
Explanation: SGX enclaves provide hardware-isolated memory regions whose secrets are inaccessible to the hypervisor, OS, or any other tenant—meeting the “hypervisor compromised” threat model with minimal operational overhead. A and D leave keys exposed to a compromised kernel/hypervisor. C gives strong hardware protection but still creates a shared tenancy surface inside the HSM; a firmware or logical flaw could leak across tenants.

Q2. During a crypto-agility audit you discover that a legacy e-commerce application hard-codes RSA-2048 for digital signatures and cannot be changed for 18 months. NIST predicts that RSA-2048 will drop to 112-bit security equivalence within 5 years. The business will not accept a shutdown. Which is the most risk-appropriate architectural step today?  
A. Immediately turn off all digital-signature functionality until the code can be rewritten.  
B. Layer an ECDSA-P256 signature on top of every existing RSA-2048 signature (dual signing) so that the weaker RSA can be dropped later.  
C. Re-compile the application inside an SGX enclave so that the RSA key is “hardware protected” and therefore considered secure.  
D. Generate a new 4096-bit RSA key pair, re-sign the old certificates, and continue using the same hard-coded algorithm.  

Correct Answer: B  
Explanation: Dual signing with ECDSA-P256 provides a crypto-agile bridge: the existing RSA-2048 signatures remain verifiable while the stronger ECDSA layer assures long-term authenticity; RSA can be retired later without breaking compatibility. A is an availability killer. C does not strengthen the algorithm, only the storage. D doubles key size but keeps the same algorithmic weakness and may break compatibility with legacy clients that only support 2048-bit keys.

Q3. A smart-card issuance system uses a three-tier certificate authority (offline root, online policy-CA, online issuing-CA). The operations team wants to automate day-to-day issuance without weakening the root’s security posture. Which control combination best preserves the root’s offline status while allowing automated enrollment?  
A. Keep the root offline; delegate certificate issuance to the issuing-CA and use an online OCSP responder signed by the root.  
B. Issue a cross-certification certificate from the root directly to each subscriber, then bring the root online only during business hours.  
C. Generate a long-lived (20-year) CRL signed by the root so that subordinate CAs can operate without further root interaction.  
D. Place the root private key inside a network-attached HSM and restrict SSH access to two senior operators.  

Correct Answer: A  
Explanation: An offline root signs only the subordinate CA certificates; day-to-day validity information is provided by OCSP/CRL produced by the online issuing-CA or a responder, so the root never comes online. B violates the offline principle. C creates an unmanageable CRL and still requires periodic root signatures. D makes the root technically online even if access is restricted.

Q4. A micro-service mesh enforces mTLS between 800 pods. The security team wants to avoid cipher-suite downgrade attacks while ensuring forward secrecy, but also must support legacy internal clients that only support TLS 1.2. Which configuration best balances security and compatibility?  
A. Allow only TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 on the server side and reject any client hello that offers other suites.  
B. Permit any TLS 1.2 or 1.3 cipher suite that includes SHA-1 so that legacy browsers continue to work.  
C. Configure servers to prefer TLS 1.3, but still accept TLS 1.2 and offer only ECDHE or DHE suites; disable static-RSA and SHA-1.  
D. Disable TLS 1.2 entirely and mandate TLS 1.3 with ed25519 certificates.  

Correct Answer: C  
Explanation: C enforces ephemeral key exchange (forward secrecy) and removes the weakest TLS 1.2 constructs while still allowing legacy TLS 1.2 clients that support ECDHE/DHE. A is overly restrictive and may break legitimate TLS 1.2 clients that only support ECDHE-ECDSA. B keeps SHA-1, enabling downgrade and collision attacks. D is ideal cryptographically but immediately breaks all legacy clients, violating the compatibility requirement.

Q5. A company is selecting a block-cipher mode for encrypting 50 GB database backups that are streamed sequentially to object storage. The data must remain confidential and tamper-evident, but the encryption appliance has no AES-GCM hardware offload. Which mode and MAC construct is most performant and secure?  
A. AES-CBC with HMAC-SHA-256 applied over the entire ciphertext (encrypt-then-MAC).  
B. AES-GCM with a 96-bit random IV for each backup.  
C. AES-CTR with a fixed IV of 0x00 and SHA-1 for integrity.  
D. AES-ECB with PKCS#7 padding and a CRC-32 tag.  

Correct Answer: A  
Explanation: Encrypt-then-MAC with CBC gives confidentiality and integrity, can be computed in a single pass with streaming APIs, and avoids the performance penalty of GCM on hardware lacking GMAC acceleration. B is ideal if hardware offload exists, but the scenario explicitly rules it out, making GCM slow and potentially causing buffer issues on large objects. C reuses the IV with CTR, enabling keystream reuse attacks, and SHA-1 is weak. D leaks patterns and provides no cryptographic integrity.

Q6. A firmware team must implement secure boot for an ARM Cortex-M IoT device that lacks a discrete TPM. The ROM bootloader already verifies the first-stage bootloader using a vendor ECC public key. Which architectural element is most critical to prevent an attacker with physical UART access from bypassing secure boot?  
A. Store the ECC public-key hash in one-time-programmable eFuses and disable the JTAG/SWD interface via GPIO lock.  
B. Encrypt the first-stage bootloader with AES-256 and store the key in external SPI flash.  
C. Require the user to enter an 8-digit PIN before the bootloader runs.  
D. Use a larger ECC key (P-521) instead of P-256.  

Correct Answer: A  
Explanation: Anchoring the trust anchor in immutable eFuses and disabling debug interfaces closes the primary physical attack vectors. B only adds confidentiality, not integrity, and the key in external flash is easily probed. C is unusable in headless IoT and does not bind the image. D increases cryptographic strength but does not stop an attacker who simply replaces the image and public key.

Q7. A web application running in a public cloud uses server-side AES-256-CGM to encrypt PII before writing to a managed database service. The CSP holds the KMS master key in an HSM, but the application also needs to support row-level, order-preserving searches on the last-four digits of social-security numbers. Which design provides the best confidentiality while still allowing the required search functionality?  
A. Encrypt the full SSN with AES-GCM and store the last-four digits in plaintext in a separate column.  
B. Tokenize the last-four digits using a format-preserving, randomly seeded AES-FFX scheme with a separate tokenization key that is rotated annually.  
C. Use deterministic AES-GCM (IV = 0) for the last-four digits so that ciphertexts are searchable.  
D. Hash the last-four digits with SHA-256 and store the hash for comparison.  

Correct Answer: B  
Explanation: AES-FFX (NIST SP 800-38G) produces ciphertexts that retain the format and allow order-preserving queries while still being cryptographically protected with a distinct key that can be rotated. A leaves sensitive data in clear. C reuses the IV with GCM, breaking both confidentiality and integrity. D produces a high-entropy blob that no longer supports order or range queries.

Q8. A DevOps pipeline must sign container images so that runtime nodes can verify authenticity. The private signing key cannot reside on any internet-facing system. Which architecture best supports this requirement while allowing fully automated builds?  
A. Store the private key in the CI server’s “secret” environment variable and sign images immediately after build.  
B. Use a detached signing service that exposes an API gated by mutual TLS; the service holds the key inside an HSM and signs only after validating build metadata.  
C. Commit the private key into the source repo but encrypt it with GPG.  
D. Generate a new key pair for every build and embed the public key inside the image.  

Correct Answer: B  
Explanation: A dedicated signing micro-service with an HSM keeps the private key off internet-facing CI nodes while exposing a narrow API that can be invoked automatically. A leaves the key in the CI environment, a high-risk surface. C places the key in version control, visible to every developer. D makes verification impossible because no trusted public key is published in advance.

Q9. An organization wants to replace its aging RADIUS-based VPN authentication with a FIDO2/WebAuthn solution. The existing network appliances support EAP-TTLS but not FIDO2 directly. Which integration approach preserves the highest level of phishing resistance without replacing every appliance?  
A. Deploy an identity-proxy that converts FIDO2 assertions to SAML claims; forward the SAML to the RADIUS server via RadSec.  
B. Issue each user a FIDO2-certified hardware token that outputs a static 6-digit HOTP code entered into the existing RADIUS prompt.  
C. Replace RADIUS with a homemade REST API that accepts raw FIDO2 responses.  
D. Continue using passwords over EAP-TTLS but add a second login page that asks for a FIDO2 signature after the VPN tunnel is established.  

Correct Answer: A  
Explanation: A standards-based proxy translates modern phishing-resistant FIDO2 assertions into SAML that legacy RADIUS can consume over RadSec, requiring no forklift upgrade of appliances. B downgrades FIDO2 to a simple OTP, losing phishing resistance. C introduces unsupported, non-standard plumbing. D still exposes the primary password to MITM attacks and makes FIDO2 optional.

Q10. A safety-critical embedded system must execute cryptographic software routines in a fixed cycle time of 5 ms. The current RSA-2048 signature verification consumes 4.2 ms on the 200 MHz CPU, leaving insufficient headroom. Which change best preserves security while meeting the timing requirement?  
A. Replace RSA-2048 signature verification with ECDSA-P256 verification and use the same 256-bit hash.  
B. Reduce RSA key size to 1024 bits and keep the existing code.  
C. Cache previous signature-verification results and skip recalculation when the message is identical.  
D. Offload RSA verification to a general-purpose CPU core running at 100 MHz in parallel.  

Correct Answer: A  
Explanation: ECDSA-P256 verification is >10× faster than RSA-2048 on the same scalar core while maintaining comparable security (~128-bit strength), easily fitting inside 5 ms. B weakens RSA below acceptable security thresholds. C introduces replay and cache-poisoning vulnerabilities. D moves workload to a slower core, exacerbating the problem.
Q1. A multinational bank is designing a new public-key infrastructure to support digitally-signed SWIFT messages. The architecture team wants the highest assurance that the root CA’s private key can never be reconstructed, even if all HSMs in one data center are physically captured. Which key-management method BEST satisfies this requirement?  
A. Store the root private key in an online Thales HSM with dual control and split knowledge.  
B. Use a quorum-controlled, air-gapped hardware security module that performs key ceremony shredding after each use.  
C. Generate the root key using threshold cryptography (Shamir secret sharing) with five shares and a 3-of-5 policy; delete the key from all systems after shares are printed and stored in five separate bank vaults.  
D. Create the root key inside an HSM, export an encrypted backup to two off-site safes, and require smart-card–based dual control to restore it.  

Correct Answer: C  
Explanation: Threshold cryptography with physical destruction of the electronic key (keeping only the split secrets) guarantees that no single device or location ever has enough material to reconstruct the root private key, even under total physical compromise. A and D leave the full key inside an HSM that can theoretically be captured and tampered with. B still keeps the key inside the HSM between ceremonies; shredding only “after each use” does not prevent later reconstruction if the HSM is seized.

Q2. A cloud SaaS provider runs a multi-tenant micro-service that encrypts customer objects with AES-256. To minimize latency, the provider wants to perform bulk encryption in application memory without exposing plaintext keys to the hypervisor or host OS. Which CPU-based capability is MOST appropriate?  
A. Intel MPK (Memory Protection Keys)  
B. AMD SEV-ES (Secure Encrypted Virtualization-Encrypted State)  
C. Intel SGX (Software Guard Extensions)  
D. ARM TrustZone TZASC  

Correct Answer: C  
Explanation: Intel SGX creates encrypted enclaves whose memory is inaccessible to the hypervisor, OS, or any other process, allowing AES operations on plaintext keys that never leave the CPU package. MPK only isolates user-space page access rights; SEV-ES encrypts VM register state but not in-memory AES keys; TZASC is for secure-world memory partitioning on ARM, not for isolating application-level keys from the rich OS.

Q3. A defense contractor is evaluating formal evaluation models for a new weapons-guidance system that must enforce both confidentiality and integrity with strict lattice rules. Which model is the BEST fit?  
A. Biba  
B. Bell-LaPadula  
C. Chinese Wall  
D. Bell-LaPadula with Biba (Lipner or “combined” model)  

Correct Answer: D  
Explanation: The combined Bell-LaPadula (confidentiality) and Biba (integrity) model—often called the Lipner model—provides lattice-based controls for both confidentiality levels and integrity levels, mandatory for a system that processes classified data and must prevent untrusted code from modifying trusted guidance software. Bell-LaPadula alone only covers confidentiality; Biba alone only covers integrity; Chinese Wall is for conflict-of-interest, not lattice-based military classification.

Q4. An IoT manufacturer wants to ensure that only authorized firmware runs on its new thermostat. The device has a low-power Cortex-M0 microcontroller, 64 kB ROM, 32 kB RAM, and no TPM. Which root-of-trust approach is MOST feasible?  
A. Store a 2048-bit RSA public key in ROM and verify firmware signature at every boot.  
B. Use AES-CBC encryption of the firmware image and decrypt in place at boot.  
C. Implement a chain-of-trust starting with a custom bootloader that hashes the image with SHA-256 and compares it against a value fused in one-time-programmable (OTP) eFuses.  
D. Embed a symmetric key in ROM and perform a MAC check over the entire image.  

Correct Answer: C  
Explanation: An immutable hash in OTP eFuses plus a secure bootloader provides an inexpensive root-of-trust: the device refuses to run any image whose hash does not match the fused value. RSA (A) is computationally heavy for the M0 and still needs trusted key storage; AES-CBC (B) provides confidentiality but no integrity/authenticity; a ROM symmetric key (D) cannot be revoked if leaked and offers no authenticity of origin.

Q5. A company is deploying a new containerized payment-processing workload. Regulations require that cryptographic keys never exist in plaintext outside the CPU package and that memory dumps (core files) contain no key material. Which Kubernetes feature BEST satisfies the requirement?  
A. Use Kubernetes secrets mounted as tmpfs volumes.  
B. Enable Intel SGX remote attestation and run the crypto workload inside SGX enclaves.  
C. Turn on swap accounting and set memory limits to prevent core dumps.  
D. Run the container in a gVisor sandbox with encrypted swap.  

Correct Answer: B  
Explanation: Only SGX (or similar hardware enclaves) guarantees that keys are encrypted while in DRAM and inaccessible to core dumps, hypervisor, or host OS. Kubernetes secrets (A) are base64-encoded and visible to the kubelet and host. Disabling dumps (C) is a best-effort control that can be bypassed; gVisor (D) adds syscall filtering but does not encrypt memory contents.

Q6. During a security architecture review of a three-tier web application, the assessor notes that the application server uses HMAC-SHA-256 for state-data stored in a client-side cookie. The HMAC key is 32 bytes generated by java.security.SecureRandom at application start-up and shared across all instances behind a load balancer. Which threat is MOST concerning?  
A. Brute-force collision against SHA-256  
B. Replay of an old cookie when the user’s IP address changes  
C. Horizontal privilege escalation if an attacker obtains the shared key  
D. Timing-side-channel leakage of the HMAC  

Correct Answer: C  
Explanation: Because the same key is used on every node, compromise of any single application server reveals the global key, allowing an attacker to forge arbitrary cookies and impersonate any user. SHA-256 collision resistance (A) is not the weak point; replay (B) is mitigated by timestamps/nonce inside the cookie; timing attacks (D) are impractical over networks and less severe than total key compromise.

Q7. A satellite-communications vendor wants to provide over-the-air firmware updates authenticated with ECDSA-256 but must tolerate occasional bit-flips caused by cosmic radiation. Which encoding strategy BEST preserves signature verifiability?  
A. Base64 encode the entire firmware image before signing.  
B. Use a 255-bit error-correcting BCH code over the signature field.  
C. Transmit the signature separately over a TCP-based reliable control channel.  
D. Apply Reed-Solomon forward-error-correction to the combined image-plus-signature packet.  

Correct Answer: D  
Explanation: Reed-Solomon FEC can correct multiple symbol errors in the composite blob, ensuring the signature is still bit-exact even after radiation-induced flips. Base64 (A) is just encoding, not error correction. BCH (B) only protects the signature field, leaving the image itself vulnerable. TCP (C) retransmits on loss but does not fix single-bit corruptions that pass the TCP checksum.

Q8. A large retailer is replacing its legacy WPA2-PSK Wi-Fi for staff handhelds. Requirements are: (1) mutual authentication of device and network, (2) no stored passwords on devices, (3) support for corporate MDM onboarding of 30 kBYOD devices per day. Which 802.1X credential combination is the BEST fit?  
A. EAP-TLS with device certificates issued via SCEP  
B. PEAP-MSCHAPv2 with randomly pre-shared keys  
C. EAP-TTLS with PAP inner method  
D. EAP-FAST with anonymous provisioning  

Correct Answer: A  
Explanation: EAP-TLS gives strong mutual authentication using X.509 certificates, eliminates passwords, and scales via SCEP/EST enrollment integrated with MDM. PEAP-MSCHAPv2 (B) still requires a password hash on the device/supplicant; TTLS-PAP (C) sends cleartext password equivalent; EAP-FAST (D) allows anonymous provisioning but relies on PAC secrets that can be copied if the device is rooted.

Q9. A zero-trust architecture working group must choose a secure design for internal service-to-service RPC traffic that traverses a shared Layer-3 network. Requirements are mutual authentication, session confidentiality, and perfect-forward secrecy. All services already have x.509 certs from the corporate CA. Which approach BEST meets the goals with the LEAST operational change?  
A. IPsec in tunnel mode with IKEv2 and ECDHE  
B. Mutual TLS (mTLS) with TLS 1.3 and ECDHE key exchange  
C. GRE over DMVPN with pre-shared keys  
D. L2TPv3 with certificate-based EAP-TLS  

Correct Answer: B  
Explanation: mTLS with TLS 1.3 natively provides mutual authentication, session encryption, and ECDHE-based perfect-forward secrecy using the existing certificates and requires no new tunnel overlay. IPsec tunnel (A) adds extra headers and complexity; DMVPN (C) is designed for site-to-site, not east-west service traffic, and pre-shared keys violate PFS if ever leaked; L2TPv3 (D) is a Layer-2 tunnel rarely used for service mesh and lacks native crypto.

Q10. A chipmaker is taping-out a custom ASIC that will store a device-unique 256-bit private key for cryptocurrency wallets. To resist invasive attacks (decapping, FIB, micro-probing) the silicon vendor offers: (1) a passive metal mesh, (2) a SRAM-PUF-based key derivation block, (3) embedded flash, or (4) laser-programmed fuses. Which option gives the STRONGEST protection against key extraction?  
A. Laser fuses blown at test and read-locked by the boot ROM.  
B. AES-256 key stored in embedded flash encrypted by a fixed obfuscation key.  
C. SRAM PUF that regenerates the key at boot, with helper data stored in off-chip EEPROM.  
D. Passive top-layer metal mesh with tamper sensors that trigger zeroization of embedded flash.  

Correct Answer: C  
Explanation: A Physically-Unclonable Function (PUF) produces the key only when powered, leaving no persistent stored value to extract with decapping or FIB; helper data alone cannot reconstruct the key. Laser fuses (A) are visible in SEM imaging. Encrypted flash (B) still contains ciphertext that can be brute-forced if the obfuscation key leaks. A mesh (D) is a detection mechanism, but if bypassed the flash still yields ciphertext; it does not remove the target.
Q1. A multinational bank is designing a new public-cloud-based payment platform that must remain available 24×7 even if an entire AWS region fails. The solution must guarantee that no customer’s ledger record can ever be lost or rolled back after a transaction is acknowledged to the customer.  
Which of the following architectural decisions BEST satisfies both requirements?  
A. Deploy the ledger service in Multi-AZ RDS with automated daily snapshots.  
B. Use a containerized ledger micro-service fronted by an ALB and backed by S3 cross-region replication.  
C. Replicate the ledger across three regional DynamoDB tables that use global tables with write-through to an immutable write-ahead log stored in S3 Object Lock.  
D. Mirror the ledger database to a standby EC2 instance in a second AZ using block-level replication.  
Correct Answer: C  
Explanation: Global tables give multi-region active-active availability; S3 Object Lock with write-through logging provides non-repudiation and prevents loss or rollback. A and D are single-region and can lose data during a regional outage. B offers no strong consistency or durability guarantee for financial records.

Q2. During a security architecture review of an IoT-based smart-manufacturing line, you discover that each programmable logic controller (PLC) accepts unsigned ladder-logic downloads on TCP/18245 without authentication. The OT network is air-gapped from the corporate IT network except for a unidirectional serial-to-Ethernet data diode that exports telemetry to the SIEM.  
Which control BEST mitigates the risk of malicious ladder-logic injection while preserving the air-gap?  
A. Deploy a next-generation firewall on the OT segment to block TCP/18245.  
B. Install a code-signing requirement in the PLC bootloader and enforce signing in the engineering workstation.  
C. Implement MAC address whitelisting on the OT switches.  
D. Tunnel all programming traffic through IPSec VPN to the corporate network.  
Correct Answer: B  
Explanation: Code signing assures only authorized logic runs on the PLC and does not require two-way IP connectivity, preserving the air-gap. A breaks needed functionality. C is trivial to spoof. D violates the air-gap principle by adding bidirectional IP.

Q3. A company is selecting a public-key algorithm to protect firmware updates for devices that may remain in the field for 15 years. The firmware image is distributed on USB sticks by technicians who occasionally visit remote sites with no Internet. The processor is an ARM Cortex-M4 with 256 kB RAM and no hardware AES accelerator.  
Which algorithm suite provides the BEST long-term confidentiality and authenticity while staying within hardware constraints?  
A. RSA-4096 with SHA-256  
B. ECC P-256 with ECDSA and AES-128-CCM  
C. ECC P-384 with SHA-384  
D. RSA-2048 with 3DES-CBC and HMAC-SHA-1  
Correct Answer: B  
Explanation: P-256 gives ~128-bit security with small key size (256b vs 4096b RSA), fitting RAM and CPU; AES-128-CCM provides authenticated encryption for bulk data. A and D lack authenticated encryption; C’s P-384 is overkill and slower on the M4; D uses deprecated SHA-1 and 3DES.

Q4. A cloud SaaS vendor offers a “zero-knowledge” file-sync product. During a due-diligency walk-through you learn that each user’s files are encrypted on the client with a 128-bit AES key that is randomly generated and then encrypted under the user’s login password (SHA-256) before being stored in the vendor’s MySQL database.  
Which architectural change MOST reduces the risk of offline brute-force attacks on user data?  
A. Increase AES key length to 256 bits.  
B. Add PBKDF2 with 100 000 iterations and per-user salt before storing the password wrap.  
C. Store the encrypted AES key in an HSM instead of MySQL.  
D. Switch to RSA-2048 to wrap the AES key.  
Correct Answer: B  
Explanation: PBKDF2 slows brute-force attempts against the password-derived wrap key. A does not protect the key wrap. C moves but does not strengthen the wrap. D adds no benefit because the RSA private key would still be protected by the same password.

Q5. A large retailer is implementing a new point-of-sale (POS) architecture. The PCI-DSS QSA insists that the devices must undergo “dual control” and “split knowledge” for any key-loading ceremony that injects the initial symmetric key into the secure keypad.  
Which implementation satisfies BOTH requirements?  
A. Two senior managers each enter a 16-character password that XORs to the transport key; the key is then decrypted inside the device and loaded.  
B. A smart-card holding the full key is inserted by employee A, and employee B types a 6-digit PIN to unlock it; the terminal then loads the key.  
C. The key is split into three 64-bit parts using Shamir’s Secret Sharing with threshold 2; any two key custodians enter their shares at the same terminal.  
D. Employee A types half of the 128-bit key and employee B types the other half; both halves are concatenated and injected.  
Correct Answer: C  
Explanation: Shamir’s scheme enforces that no single person ever knows the full key (split knowledge) and requires at least two people (dual control). A allows one person to learn the full key after XOR. B gives the full key to the smart-card holder. D exposes each half to the terminal software.

Q6. A start-up is building a blockchain-backed medical-records system. Regulations require that any personal data must be erasable on request. The chief architect proposes storing only the AES-encrypted record on-chain while keeping the key in an off-chain key vault.  
Which additional control is CRITICAL to satisfy the erasure requirement?  
A. Use a 256-bit key for AES.  
B. Ensure the AES key is randomly generated per record and cryptographically shredded (wiped) when erasure is requested.  
C. Store the encrypted record in IPFS instead of directly on-chain.  
D. Use ECC instead of RSA for the node-to-node TLS channels.  
Correct Answer: B  
Explanation: Erasure is achieved by destroying the only decryption key (crypto-shredding). A, C, and D do not address data remanence on an immutable ledger.

Q7. A government agency is designing a classified network that must process information up to the SECRET level and also provide secure voice and video conferencing. The network must comply with CNSSP-11.  
Which of the following media encryption solutions is ACCEPTABLE without additional waivers?  
A. SRTP with AES-256-GCM and 128-bit tags using pre-shared keys delivered by a PKI that is certified at the SECRET level.  
B. WebRTC secured by TLS 1.3 and AES-256-GCM running over an IPSec tunnel.  
C. SDES-SRTP with AES-256-CTR and 80-bit authentication tag.  
D. Proprietary VoIP encryption using Twofish with 256-bit keys and 64-bit MAC.  
Correct Answer: A  
Explanation: CNSSP-11 (and NSD-42) explicitly approve Suite-B algorithms; AES-GCM with 256-bit keys and 128-bit tags is listed. B adds unnecessary double encryption and WebRTC is not on the approved list. C’s 80-bit tag is below the 96-bit minimum. Twofish is not an approved algorithm.

Q8. A company runs a legacy CORBA application that uses GIOP/SSL for mutual authentication. A penetration test showed that the app accepts any certificate signed by a public CA whose root is in the default Java truststore, allowing an attacker to mint a valid certificate for a subdomain and perform a man-in-the-middle attack.  
Which fix BEST preserves legacy compatibility while enforcing that only internally issued certificates are trusted?  
A. Replace the default truststore with a custom one containing only the corporate root CA.  
B. Enable certificate revocation list (CRL) checking.  
C. Re-issue all certificates with extendedKeyUsage=serverAuth only.  
D. Pin the public key of the server certificate in the client binary.  
Correct Answer: A  
Explanation: Limiting the truststore to the corporate root closes the attack window without changing GIOP/SSL code. CRL only helps if the attacker’s cert is revoked. EKU does not stop a CA-signed impersonating cert. Pinning breaks when certs rotate and requires code changes.

Q9. An enterprise wants to move its on-prem PKI to a hybrid model where the root CA is kept offline in a Faraday-caged vault and online subordinate CAs issue certificates to 50 000 employees and 100 000 IoT sensors. The security policy mandates that if a subordinate CA is ever compromised, any fraudulently issued certificates must be un-trusted within one hour.  
Which architecture BEST meets the one-hour requirement?  
A. Use short-lived 7-day certificates and force daily renewal.  
B. Operate the subordinates with a local CRL published every 30 minutes to CDNs.  
D. Require OCSP stapling with a 5-minute cache validity and an OCSP responder signed by the root.  
C. Enable the “must-staple” extension and run an OCSP responder with a 10-minute cache validity; additionally pre-publish a 6-hour CRL as a fail-safe.  
Correct Answer: C  
Explanation: Must-staple forces TLS clients to reject certs without a fresh OCSP response, giving <10 min revocation window; CRL provides backup. A imposes huge operational load and still leaves a 7-day window. B’s 30-minute CRL alone can miss the one-hour SLA. D’s 5-minute cache is better but lacks must-staple enforcement.

Q10. A carmaker is designing the firmware update process for the ECU that controls emergency braking. The ECU has 1 MB flash, 128 kB RAM, and runs AUTOSAR. The threat model includes an attacker who can briefly obtain physical access to the car’s OBD-II port.  
Which countermeasure MOST effectively prevents the attacker from installing rogue firmware?  
A. Require that updates be delivered only through the car’s cellular modem with TLS 1.3.  
B. Store firmware images in an encrypted partition of the ECU flash.  
C. Implement an OEM boot-loader that verifies an ECDSA-256 signature over the entire firmware image using a public key hashed in one-time-programmable eFuses.  
D. Use a password-protected JTAG interface on the ECU.  
Correct Answer: C  
Explanation: Secure boot with ECDSA and an immutable public-key hash guarantees only OEM-signed firmware runs, even if the attacker can flash via OBD. A blocks remote attacks but not physical. B encrypts but does not authenticate. D can be bypassed with hardware probes.
Q1. A multinational bank is designing a new public-cloud-based payment platform that must process transactions in 28 countries with differing data-sovereignty laws. The lead architect proposes a single “unified data fabric” that replicates all transaction logs to five global zones for performance and resiliency. The CISO objects, arguing the design violates several jurisdictional requirements that forbid certain account data from leaving its country of origin. Which security principle is MOST clearly at risk if the design is approved as proposed?  
A. Layering  
B. Abstraction  
C. Privacy as a component of security  
D. Least common mechanism  

Correct Answer: C  
Explanation: Privacy as a component of security requires that personal data be handled according to the legal privacy rules of the jurisdiction in which it is collected. Replicating data across borders without regard to sovereignty laws directly threatens this principle. Layering (A) is about multiple controls, not data residency. Abstraction (B) hides complexity but does not address legal data placement. Least common mechanism (D) is about avoiding shared resources that can create single points of compromise, irrelevant here.

Q2. A startup is selecting a cryptographic scheme for firmware updates delivered over the Internet to low-power IoT devices. Each device has a hardware AES-256 engine but only 8 kB of free RAM. Updates must be authenticated and any downgrade attack prevented. The team is debating whether to use AES-CBC with HMAC-SHA-256, or AES-GCM, or ECDSA with SHA-256, or RSA-4096 with PKCS#1 v1.5 signatures. Which option BEST meets the integrity, authenticity, and resource constraints?  
A. AES-CBC with HMAC-SHA-256 (encrypt-then-MAC)  
B. AES-GCM with 96-bit IV and 128-bit tag stored in update header  
C. ECDSA with SHA-256 over the plaintext image  
D. RSA-4096 with PKCS#1 v1.5 signature and no encryption  

Correct Answer: B  
Explanation: AES-GCM provides authenticated encryption with a single key, fits the on-chip AES accelerator, needs only ~128 bytes of additional RAM for the tag/IV, and prevents downgrade if the version is inside the authenticated data. AES-CBC+HMAC (A) requires two keys and two passes, doubling RAM usage. ECDSA (C) offers only a signature, leaving the image unencrypted in transit and still needs a separate confidentiality mechanism. RSA-4096 (D) signature verification is CPU-heavy and does not encrypt the image.

Q3. A government agency runs a legacy relational database that stores classified mission data in rows labelled TOP SECRET, SECRET, and CONFIDENTIAL. The agency now wants to host this database in a virtualized, multi-tenant data center cleared to SECRET. The VM cluster uses a type-1 hypervisor certified to Common Criteria EAL-4. Which security architecture concept is MOST violated by this plan?  
A. The *-integrity property (Bell-LaPadula)  
B. The simple security property (Bell-LaPadula)  
C. The *-property (star property) of Bell-LaPadula  
D. The strong tranquility property  

Correct Answer: C  
Explanation: The *-property (no write down) prevents a subject cleared to SECRET from writing TOP SECRET data to a container whose classification level is SECRET or lower. Hosting a TOP SECRET row in a SECRET-cleared hypervisor allows exactly that violation. Simple security (B) is no read up, not the issue here. *-integrity (A) is Biba, not Bell-LaPadula. Strong tranquility (D) deals with dynamic class changes, not the hosting level mismatch.

Q4. During a hardware penetration test, an attacker extracts the firmware from a point-of-sale terminal and locates a hard-coded 512-bit RSA private key used for TLS client authentication to the payment gateway. The corresponding public key is embedded in the gateway’s allow-list and cannot be changed without a firmware update on thousands of deployed terminals. The company wants a short-term workaround until terminals are replaced next year. Which control BEST reduces the immediate risk without altering the terminals?  
A. Enable perfect-forward-cipher suites only on the gateway  
B. Deploy a TLS-terminating reverse proxy that requires an additional client certificate issued by a fresh CA  
C. Add the leaked public key to a certificate-revocation list (CRL) and configure the gateway to check it  
D. Rate-limit TLS handshakes from any single terminal to five per minute  

Correct Answer: B  
Explanation: A reverse proxy can demand a second, uncompromised certificate while still accepting the old one on the outer layer, effectively creating a dual-factor authentication that blocks anyone who only has the leaked key. Forward secrecy (A) does not stop authentication with the stolen key. Revoking the key (C) would brick every legitimate terminal. Rate-limiting (D) slows but does not stop fraudulent connections.

Q5. A company is implementing a zero-trust network architecture. All user-to-server and server-to-server traffic must be encrypted and mutually authenticated. Performance testing shows that 100% TLS with mutual RSA-2048 certificates drives CPU on micro-services to 80% and adds 40 ms latency. The security team must choose an alternative that preserves mutual authentication and confidentiality while lowering CPU and latency. Which technology offers the BEST trade-off?  
A. TLS 1.3 with ECDHE-X25519 and ECDSA P-256 certificates  
B. IPsec tunnel mode with pre-shared IKEv2 keys  
C. QUIC with 0-RTT resumption and server-only RSA certs  
D. mTLS with static RSA key transport and TLS 1.2  

Correct Answer: A  
Explanation: TLS 1.3 with ECDHE and ECDSA uses faster elliptic-curve key exchange and authentication, cutting CPU roughly in half and removing one round-trip, meeting both security and performance goals. IPsec (B) still requires crypto but adds complex IKEv2 negotiation and is not application-aware. QUIC 0-RTT (C) saves latency but the scenario requires mutual auth, which is absent. Static RSA (D) is obsolete, lacks forward secrecy, and still bears RSA computational cost.
