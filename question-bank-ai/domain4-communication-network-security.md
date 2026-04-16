Q1. A multinational bank is deploying an SD-WAN to connect 200 branches to two redundant data centers. The security team must ensure that every packet is authenticated and encrypted between endpoints without requiring full-mesh IKEv2 tunnels. Which technology best meets the requirement while preserving the SD-WAN’s dynamic-path selection?  
A. MACsec on the WAN edge switches  
B. TLS 1.3 inside VXLAN overlays  
C. DMVPN with PKI-based AES-GCM  
D. IEEE 802.1X on the branch LAN ports  

Correct Answer: C  
Explanation: DMVPN provides dynamic, on-demand IPsec tunnels (PKI-based AES-GCM) that authenticate and encrypt every packet between any two endpoints without a full mesh of pre-configured IKEv2 SAs. MACsec and 802.1X are Layer-2 controls that do not traverse provider WANs, while TLS 1.3 inside VXLAN lacks native multicast support and does not scale for 200-site full encryption.

Q2. During a red-team exercise, an attacker on the corporate Wi-Fi sends forged beacon frames advertising a malicious SSID with the same name as the legitimate network. Client devices automatically associate and receive an EAP-TLS handshake that terminates in the attacker’s laptop, allowing credential theft. Which 802.11 enhancement would prevent this attack?  
A. 802.11k (Neighbor Report)  
B. 802.11w (Protected Management Frames)  
C. 802.11r (Fast BSS Transition)  
D. 802.11i (RSN)  

Correct Answer: B  
Explanation: 802.11w cryptographically protects de-authentication, disassociation, and beacon/action frames, preventing attackers from forging beacons or tearing clients off the legitimate AP so they re-connect to a rogue twin. 802.11i provides only data-frame encryption; 802.11k and 802.11r optimize roaming but do not protect management frames.

Q3. A zero-trust architect must secure RDP access to Windows jump hosts in AWS VPCs. Users already authenticate to the corporate SAML IdP via browser. Which sequence provides the strongest assurance before the RDP session is established?  
A. Site-to-site VPN + NLA + local AD passwords  
B. Clientless SSL VPN + RDP gateway with cached credentials  
C. SAML-to-OIDC proxy + short-lived signed JWT + AWS Systems Manager Session Manager  
D. GRE tunnel + LDAP bind + RDP file signed by CA  

Correct Answer: C  
Explanation: Session Manager uses IAM-based OIDC tokens derived from SAML assertions; no inbound RDP port is ever open, credentials are short-lived, and every command is logged to CloudTrail. Options A and B still expose RDP to the network and rely on passwords, while GRE provides no encryption or authentication.

Q4. A manufacturing plant uses PROFINET over Ethernet/IP to control robotic arms. The plant manager wants to segment the industrial network from the corporate LAN but still allow historians to poll PLC data in real time. Which architecture best balances security and deterministic timing?  
A. Dual-homed firewalls with deep-packet inspection on every PROFINET frame  
B. Converged network using 802.1Qbv (Time-Sensitive Networking) and a data-diode unidirectional gateway  
C. Air gap with nightly USB sneaker-net of CSV logs  
D. IPSec VTI tunnels between corporate routers and plant switches  

Correct Answer: B  
Explanation: 802.1Qbv schedules traffic classes so that PROFINET cycle frames meet hard-real-time bounds, while a data diode allows read-only, unidirectional flow of telemetry to corporate historians, eliminating feedback attack paths. Deep-packet inspection adds jitter, air gaps break real-time visibility, and IPSec tunnels do not provide deterministic latency.

Q5. A company’s VoIP vendor states that SIP TLS is enabled, yet a packet capture shows call-setup in clear text. Which misconfiguration is the MOST likely cause?  
A. SDP offer contains RTP/AVP instead of RTP/SAVP  
B. SIP ALG rewrote the Contact header port  
C. Certificates use CN=IP address instead of FQDN  
D. The phone’s SIP transport is still set to UDP  

Correct Answer: D  
Explanation: SIP TLS requires the SIP layer to run over TCP/TLS. If the phone is configured for UDP, it will fall back to clear-text SIP even if the server supports TLS. RTP/AVP versus RTP/SAVP affects media encryption (SRTP), not signaling. SIP ALG and certificate CN mismatches break TLS but do not downgrade to UDP automatically.

Q6. An organization is migrating from 100 Gbps MPLS to 2 × 100 Gbps dedicated waves between data centers. They need to encrypt at Layer-2 with latency <5 µs and no jumbo-frame fragmentation. Which solution fits?  
A. IPsec ESP in transport mode  
B. MACsec on 802.3bj-compliant switches  
C. GETVPN with 9K MTU  
D. L2TPv3 over IPsec  

Correct Answer: B  
Explanation: MACsec (IEEE 802.1AE) encrypts at the Ethernet frame level, adds only 16–32 bytes, and operates under 5 µs in hardware. IPsec transport mode still requires Layer-3 lookup and adds more latency; GETVPN and L2TPv3 are Layer-3 tunnels that can fragment or add excessive overhead.

Q7. A developer deploys a containerized microservice mesh on Kubernetes. The security team requires mTLS between every pod with automatic key rotation every 24 h and attestation of pod identity against a SPIFFE ID. Which Istio component enforces these requirements?  
A. Citadel (Istio-CA)  
B. Pilot (Control-plane)  
C. Galley (Configuration validation)  
D. Ingress Gateway  

Correct Answer: A  
Explanation: Citadel (now part of istiod) acts as the private CA, issuing short-lived SPIFFE-based certificates to every sidecar proxy (Envoy) and orchestrating daily rotation. Pilot distributes policy but does not issue certs; Galley validates YAML; Ingress Gateway terminates TLS to outside traffic, not pod-to-pod mTLS.

Q8. A global CDN needs to prevent BGP hijack attacks that could redirect traffic to a rogue AS. Which combination of standards provides the strongest practical mitigation today?  
A. RPKI ROV + IRR route objects signed by RIR  
B. BGPsec + IPsec tunnels between edge routers  
C. AS_PATH prepending + max-prefix limits  
D. BGP community strings + MD5 passwords on TCP 179  

Correct Answer: A  
Explanation: Resource Public Key Infrastructure with Route Origin Validation (RPKI ROV) filters invalid origin AS advertisements, while signed IRR objects add prefix-level validation. BGPsec is not yet widely deployed, MD5 only protects the TCP session, and prepending/max-prefix do not validate ownership.

Q9. A security analyst notices that IPv6-enabled workstations are autoconfiguring public addresses and bypassing the corporate proxy, leaking DNS queries to external resolvers. The IPv4 egress firewall rules do not apply. Which control closes the gap with the LEAST operational friction?  
A. Disable IPv6 on every host via GPO  
B. Deploy RA-Guard + DHCPv6 Guard and force all traffic through a dual-stack proxy that blocks direct TCP/53 and UDP/53  
C. Block protocol 41 at the border router  
D. Enable NAT64 so that all IPv6 flows are translated to IPv4 and hit existing rules  

Correct Answer: B  
Explanation: RA-Guard and DHCPv6 Guard prevent rogue router advertisements and unauthorized DHCPv6 servers, ensuring hosts receive only corporate DNS and proxy settings. Diverting all flows through an explicit dual-stack proxy applies policy uniformly without breaking IPv6 connectivity. Disabling IPv6 is brittle, protocol-41 blocks only 6to4, and NAT64 still allows direct IPv6 unless proxy enforcement is added.

Q10. A financial exchange offers colocated traders 10 Gbps access to matching engines. The exchange mandates that every multicast market-data packet be timestamped at ingress and delivered to all hosts within 50 µs with proof of non-repudiation. Which technology satisfies both timing and security requirements?  
A. PTP with hardware timestamping and AES-256-GMAC on every multicast frame  
B. NTP in broadcast mode with HMAC-SHA-1  
C. FTPS to pull files every 100 ms  
D. IPSec tunnel mode between each trader and the exchange  

Correct Answer: A  
Explanation: Precision Time Protocol (PTP/IEEE 1588) achieves sub-microsecond sync, allowing hardware-based NIC timestamping. AES-256-GMAC (authenticated encryption) adds only 8 bytes of ICV and can be processed at 10 Gbps line rate in FPGA-based NICs, preserving the 50 µs latency budget while providing non-repudiation. NTP lacks accuracy, FTPS is pull-based and too slow, and IPSec tunnel mode introduces encapsulation latency unsuitable for micro-second market data.
Q1. A global manufacturer has deployed an SD-WAN overlay that rides over multiple ISP circuits. The security team wants to guarantee that a breach of any single ISP does not allow an attacker to learn the clear-text payload of traffic between plants. Which control BEST meets this requirement?  
A. Enable AES-256-GPM on the SD-WAN edge appliances and pre-share 256-bit keys out-of-band.  
B. Run GETVPN inside the SD-WAN tunnels so that packets retain their original IP headers.  
C. Force all traffic into TLS 1.3 sessions terminated at each plant’s local proxy.  
D. Require GRE-over-IPsec with ESP-NULL to gain encapsulation without encryption overhead.  

Correct Answer: A  
Explanation: The scenario demands confidentiality of payload even if an ISP is compromised. Native SD-WAN encryption (AES-256-GCM) with out-of-band key distribution provides end-to-end encryption independent of the underlay ISP. GETVPN (B) encrypts only payload but still exposes original IPs and is seldom supported natively by SD-WAN. TLS 1.3 (C) is application-layer and would need to be implemented by every endpoint, which is impractical for plant-to-plant Layer-3 traffic. GRE-over-IPsec with ESP-NULL (D) offers encapsulation but zero encryption, violating the confidentiality requirement.

---

Q2. While reviewing firewall logs, an engineer sees repeated inbound TCP packets with the SYN flag set and the FIN flag simultaneously set, arriving from random source IPs to the company’s public web server. Which attack is MOST likely occurring?  
A. SYN flood  
B. Christmas-tree scan  
C. TCP session hijack  
D. Low-rate DoS  

Correct Answer: B  
Explanation: A packet with SYN and FIN both set is nonsensical in normal TCP operation and is characteristic of a “Christmas-tree” or “X-mas” scan (flags lit up like a Christmas tree). The goal is to probe how the target TCP stack responds to illegal flag combinations, thereby inferring open/closed ports. A pure SYN flood (A) would not set FIN. Session hijack (C) requires an existing connection, and low-rate DoS (D) manipulates timing, not flags.

---

Q3. A cloud-first enterprise uses a virtual firewall cluster in an IaaS VPC. The vendor states the cluster supports “active-active high availability using gratuitous ARP.” During a patch window, both nodes briefly go offline because the cloud provider’s L2 fabric drops the gratuitous ARP frames. Which cloud networking characteristic caused the failure?  
A. Multicast is not propagated inside the VPC.  
B. The virtual switch ignores unsolicited ARP replies.  
C. BGP route reflectors reset the ARP cache.  
D. The provider uses proxy ARP with static MAC locking.  

Correct Answer: B  
Explanation: Most public-cloud virtual networks silently discard gratuitous ARP to prevent MAC spoofing between tenants. The HA feature depended on G-ARP to move the floating MAC, so failover failed. Multicast (A) is unrelated to ARP. BGP (C) is Layer-3. Proxy ARP (D) would actually answer ARP, not drop it.

---

Q4. A company routes all Internet-bound traffic through a secure web gateway (SWG) using an explicit proxy PAC file. Remote users now report that TLS 1.3 websites intermittently fail to load. Packet captures show the SWG returns a TCP RST immediately after the ClientHello. Which change will MOST reliably restore connectivity while maintaining inspection?  
A. Downgrade the browser to TLS 1.2 only.  
B. Deploy a client-side SSL/TLS forward-proxy certificate and force cipher suites that support RSA key exchange.  
C. Enable TLS 1.3 middlebox compatibility on the SWG and push the latest trusted CA certificate to endpoints.  
D. Configure the PAC file to bypass the proxy for any site advertising TLS 1.3 in the SNI extension.  

Correct Answer: C  
Explanation: TLS 1.3 encrypts most of the handshake, breaking legacy “pass-through-then-re-encrypt” proxies. Modern SWGs implement TLS 1.3 middlebox compatibility (RFC 8446 Appendix D.4) that rewrites the ClientHello to indicate an earlier version so the proxy can still perform MITM inspection with its own certificate. Downgrading browsers (A) is a temporary hack and reduces security. RSA key exchange (B) is deprecated in TLS 1.3. Bypassing (D) defeats inspection policy.

---

Q5. A data-center network uses VXLAN with BGP EVPN for Layer-2 extension. The security architect is concerned that broadcast, unknown-unicast and multicast (BUM) traffic is traversing the underlay unencrypted. Which technology BEST provides encryption for VXLAN BUM traffic without adding new headers visible to the underlay routers?  
A. MACsec on every leaf switch port facing the spine.  
B. IPSec tunnels between VTEPs using the underlay IPs as endpoints.  
C. TLS 1.3 between the EVPN route reflectors.  
D. Control-plane only security with BGP MD5 passwords.  

Correct Answer: B  
Explanation: VXLAN itself has no encryption. Encrypting the packet flow between VTEP IPs with IPsec (transport or tunnel mode) secures the encapsulated VXLAN frames, including BUM traffic, while remaining transparent to the underlay. MACsec (A) encrypts only on the wire between two switches and stops at each hop, so spines would decrypt/encrypt, adding complexity. TLS 1.3 (C) protects only application data, not VXLAN packets. BGP MD5 (D) covers only BGP sessions, not data plane.

---

Q6. A developer uploads an AWS Lambda function that needs to reach an on-premises REST API inside a private RFC1918 subnet. The organization policy forbids any inbound firewall rules from the Internet. Which AWS networking setup satisfies the requirement with LOWEST operational overhead?  
A. Assign a public Elastic IP to the Lambda ENI and whitelist that IP on the on-prem firewall.  
B. Deploy an API Gateway edge-optimized endpoint that uses a VPN tunnel to the data center.  
C. Create a VPC-enabled Lambda function inside a private subnet attached to a VPC endpoint powered by AWS PrivateLink, then backhaul via AWS Direct Connect VIF.  
D. Launch a NAT Gateway in a public subnet, whitelist its EIP on-prem, and route Lambda traffic through it.  

Correct Answer: C  
Explanation: VPC-enabled Lambda inside a private subnet keeps traffic off the Internet. AWS PrivateLink (powered by Interface VPC Endpoints) can expose the on-prem API as an AWS service endpoint; the data traverses Direct Connect/VPN without inbound firewall rules, and there are no public IPs to maintain. Option A violates the “no inbound rule” policy. B forces API Gateway to proxy calls, adding latency and cost. D requires outbound NAT whitelisting, which still needs an inbound rule on the on-prem side for return traffic (stateful but still disallowed by policy).

---

Q7. A security administrator needs to prevent attackers from using IPv6 router advertisements (RA) to redirect endpoints to a rogue gateway. All switches are Layer-2 only and do not support Layer-3 ACLs. Which switch feature BEST mitigates this threat?  
A. RA Guard  
B. DHCPv6 Snooping  
C. IPv6 Source Guard  
D. Secure Neighbor Discovery (SeND)  

Correct Answer: A  
Explanation: RA Guard filters ICMPv6 RAs at the switch port, allowing only legitimate routers to advertise. It operates purely at Layer-2 and is widely supported. DHCPv6 Snooping (B) blocks rogue DHCPv6 servers but not RAs. IPv6 Source Guard (C) verifies source addresses, not gateway info. SeND (D) is cryptographic but requires endpoint and switch support that rarely exists in pure L2 switches.

---

Q8. A company runs an internal DNS resolver that validates DNSSEC for all outward queries. Users complain that a newly registered domain (example.pk) resolves on mobile networks but returns SERVFAIL internally. Which DNSSEC failure is the MOST likely cause?  
A. The parent zone (.pk) contains a DS record that does not match the DNSKEY digest in example.pk.  
B. The resolver’s trust anchor for .pk is missing.  
C. The resolver’s clock is skewed more than 24 h, breaking RRSIG validity checks.  
D. The domain uses CNAME to a cloud provider that has not published DNSKEY records.  

Correct Answer: A  
Explanation: A SERVFAIL from a validating resolver usually indicates a broken chain of trust. If the DS record in the parent zone does not match the DNSKEY in the child zone (e.g., because the registrar published the DS but the operator rolled the DNSKEY), validation fails. Missing trust anchor (B) would break all domains, not just one. Large clock skew (C) would affect every query. CNAME (D) is allowed in DNSSEC as long as the target is signed or the zone proves the non-existence of DNSKEY via NSEC/NSEC3.

---

Q9. A SOC analyst captures the following packet on the DMZ wire (hex dump):  
`00 50 56 c0 00 08 00 0c 29 3d 62 3d 08 00 45 00 … 11 04 05 09 00 00 00 00 00 00 00 00`  
The IP header protocol field shows 17, and the payload starts with 00 00 00 00 00 01 00 00 00 00. Which evasion technique is the sender MOST likely attempting?  
A. DNS tunneling using NULL encoding  
B. IPv4 fragmentation with overlapping offsets  
C. Protocol hopping via port 53 to bypass a firewall that allows only UDP/53.  
D. Sending a DNS query with an oversized TXID to trigger a buffer overflow.  

Correct Answer: A  
Explanation: Protocol 17 is UDP, destination port 53 (implicit). Payload starts with five zeroed bytes followed by 00 01—typical of a DNS header where transaction ID and flags are zero, then one question. The long tail of zeros is a hallmark of NULL-encoded data exfiltration in DNS tunnels. Overlapping fragmentation (B) would show more fragments and offset anomalies. Protocol hopping (C) is meaningless here—port 53 is DNS by definition. Oversized TXID (D) is not evident in the dump.

---

Q10. A satellite-office router connects to HQ through two parallel IPSec tunnels: one over a 5G provider, the other over DSL. The design mandates that video traffic must traverse 5G only if DSL latency exceeds 150 ms; otherwise 5G should remain idle. Which routing feature BEST enforces this policy on the router?  
A. Policy-Based Routing with an IP-SLA tracker pinging the DSL next-hop and setting next-hop 5G when jitter > 150 ms.  
B. EIGRP variance using a latency-based composite metric.  
C. BGP multipath with DMZ-bandwidth and BFD.  
D. Static floating routes with administrative distance 10 for 5G and 5 for DSL.  

Correct Answer: A  
Explanation: Policy-Based Routing (PBR) combined with IP-SLA (or similar SLA probes) allows real-time measurement of latency; when the tracked SLA exceeds 150 ms, PBR can switch the next-hop to 5G for video traffic only. EIGRP variance (B) balances per flow, not on dynamic latency thresholds. BGP multipath (C) requires both paths to be equal and does not react to latency alone. Floating static (D) fails over only when the primary route disappears, not when latency degrades.
Q1. A global manufacturing firm is replacing its MPLS WAN with an SD-WAN overlay that will send all branch-to-branch traffic through encrypted tunnels across the public Internet. The CISO wants to ensure that the change does not create a “passive-decrypt-then-re-encrypt” point inside the provider’s cloud. Which architectural control best meets this requirement?  
A. Require TLS 1.3 with perfect-forward-secrecy cipher suites on every overlay tunnel.  
B. Mandate end-to-end encryption that originates and terminates inside the enterprise-owned SD-WAN appliances at each site.  
C. Choose a provider that offers FIPS-140-3-certified Layer-2 encryption on every physical link.  
D. Deploy a cloud-based next-generation firewall that performs deep TLS inspection for all overlay traffic.  

Correct Answer: B  
Explanation: End-to-end encryption that originates and terminates inside the enterprise’s own SD-WAN appliances guarantees that no intermediate SD-WAN controller or service-provider element ever sees plaintext. Option A only protects application sessions, not the overlay itself. Option C encrypts the physical hop but still allows the SD-WAN controller to hold the tunnel keys. Option D intentionally breaks encryption for inspection, creating the exact “decrypt-then-re-encrypt” point the CISO wants to avoid.

---

Q2. A penetration-test report shows that an attacker on the corporate guest Wi-Fi sent forged 802.1X EAPOL-Logoff frames, forcing user laptops to re-authenticate and capturing the EAP identity response in clear text. The company uses WPA2-Enterprise with PEAP (EAP-PEAPv0/EAP-MSCHAPv2) and has no endpoint NAC agent. Which hardening step removes this specific attack vector?  
A. Enable 802.11w (Management Frame Protection) on all access points and require it in the WLAN profile.  
B. Replace PEAP with EAP-TLS and deploy machine certificates to all corporate laptops.  
C. Move the guest network to a separate VLAN and enforce MAC ACLs on the APs.  
D. Reconfigure the RADIUS server to require EAP-TTLS with PAP inside the TLS tunnel.  

Correct Answer: A  
Explanation: 802.11w cryptographically protects de-authentication and disassociation frames, making forged EAPOL-Logoff frames impossible. Option B stops credential theft but does not prevent the forced re-auth itself. Option C is segmentation, not a Wi-Fi-layer control. Option D still allows the attacker to force re-authentication and see the EAP identity in clear text.

---

Q3. The network team wants to deploy IPv6 throughout the data centre but must support legacy IPv4-only ICS sensors that cannot be upgraded for at least five years. The security policy forbids dual-stack on the sensor VLAN because of the added attack surface. Which transition technology best preserves the “no IPv6 on the VLAN” policy while still giving IPv6-only servers access to the sensors?  
A. NAT64 with stateful DNS64 in a separate DMZ segment.  
B. 6to4 tunnels between the core router and each sensor.  
C. ISATAP tunnels terminated on the sensors’ first-hop switch.  
D. Dual-stack lite (DS-Lite) on the sensor VLAN.  

Correct Answer: A  
Explanation: NAT64/DNS64 allows IPv6-only hosts to initiate sessions toward IPv4-only nodes without ever putting IPv6 on the sensor VLAN. The sensors remain pure IPv4, satisfying the policy. Options B, C and D all place IPv6 packets (or tunnel headers) on the sensor VLAN, violating the requirement.

---

Q4. A SaaS provider offers a managed site-to-site VPN service that terminates IPSec inside its multitenant gateway. The provider supplies customers with a pre-configured ASA image that uses IKEv2, AES-GCM-256, PFS-group-21 and SHA-256 for integrity. The customer’s CISSP-certified architect is concerned that the provider could decrypt the traffic. Which IKEv2 parameter must the customer insist on generating and managing themselves to prevent provider decryption?  
A. The DH-group-21 public value exchanged in IKE_SA_INIT.  
B. The pre-shared-key (PSK) used in IKE_AUTH.  
C. The ESP initialization vector (IV) for each SA.  
D. The traffic-selective proxy certificate used for TLS inspection.  

Correct Answer: B  
Explanation: With IKEv2 the pre-shared key (or the private key of a certificate) is the sole secret used to derive all session keys. If the provider knows the PSK it can derive the keys and decrypt the ESP traffic. The DH public value (A) is public by design; the IV (C) is random but not secret; TLS inspection certs (D) are irrelevant for IPSec.

---

Q5. A company’s cloud-first strategy forces all Internet-bound traffic through a single Secure Web Gateway (SWG) using a GRE tunnel from the on-prem firewall. During a regional ISP outage the GRE tunnel stays up but the SWG becomes unreachable, creating a black-hole that isolates the entire enterprise from the Internet. Which BGP feature provides sub-second failover to a secondary SWG in another region while keeping the GRE tunnel intact?  
A. BGP graceful restart.  
B. BGP multipath with equal-cost load balancing.  
C. BGP Bidirectional Forwarding Detection (BFD) with route-map conditional advertisement.  
D. BGP route reflector with next-hop-self.  

Correct Answer: C  
Explanation: BFD detects the loss of the remote GRE endpoint in milliseconds, triggering the route-map to stop advertising the primary SWG prefix and start advertising the secondary, achieving sub-second failover. Graceful restart (A) preserves forwarding state during a control-plane restart but does not speed up failure detection. Multipath (B) requires both paths to be valid simultaneously, which is not true during a black-hole. Route reflector (D) is a scalability tool, not a fast-failover mechanism.

---

Q6. A developer containerises a micro-service and exposes it on TCP/8080. The orchestration platform uses a CNI plugin that assigns each pod a routable IP address from the corporate network. The security team discovers that any compromised host on the same VLAN can reach the pod’s port directly, bypassing the service-mesh policy engine. Which Kubernetes network-policy construct enforces that only the service-mesh sidecar proxy (Envoy) may connect to TCP/8080?  
A. A NetworkPolicy with a podSelector matching the micro-service and an ingress rule allowing only pods with label app=istio-ingressgateway.  
B. A CiliumClusterwideNetworkPolicy using toPorts+HTTP rules that require JWT validation.  
C. A default-deny NetworkPolicy in the namespace plus an ingress rule from the pod’s own serviceAccount.  
D. A Calico NetworkPolicy with a global selector that enforces default-deny and an ingress rule from namespace=istio-system.  

Correct Answer: C  
Explanation: By default-denying all ingress and then allowing only traffic from the pod’s own service account (which the sidecar runs under), the policy forces every inbound packet to pass through the sidecar first. Option A incorrectly references the ingress gateway rather than the local sidecar. Option B is layer-7 and does not restrict layer-4 reachability. Option D works only if Istio is deployed in istio-system and the sidecar keeps that namespace, which is not guaranteed with CNI-routable IPs.

---

Q7. A financial institution uses 10-Gbps dark fibre between two data centres 80 km apart. The regulators require encryption of data in transit without introducing more than 100 µs of one-way latency. Which solution best meets the requirement?  
A. MACsec (IEEE 802.1AE) on the switch line cards.  
B. IPSec tunnel mode running on the WAN routers.  
C. TLS 1.3 session reuse between application servers.  
D. Quantum-safe VPN using lattice-based key exchange.  

Correct Answer: A  
Explanation: MACsec operates at the data-link layer, encrypting at wire-speed on the ASIC with sub-microsecond latency. IPSec (B) adds tens to hundreds of microseconds per packet because of tunnel header processing. TLS (C) is end-to-end and not transparent to the dark-fibre link. Quantum-safe VPN (D) is future-proof but still introduces far more latency than MACsec.

---

Q8. A company’s IoT deployment uses LoRaWAN Class A devices that only transmit after receiving two clear-channel acknowledgements. The security audit shows that an attacker with a cheap SDR can replay the join-accept message and hijack the session. Which LoRaWAN 1.1 feature prevents this replay attack?  
A. AppNonce randomised by the join server and signed with the device-specific AppKey.  
B. JoinNonce incremented by the network server and verified by the device.  
C. MIC (Message Integrity Code) computed over the entire join-request frame.  
D. AppSKey rotated every 24 hours by the application server.  

Correct Answer: B  
Explanation: LoRaWAN 1.1 mandates that the network server increment JoinNonce for every join-accept; the device rejects any JoinNonce value it has already seen, preventing replay. AppNonce (A) is random but not sequential. MIC (C) protects integrity, not replay. AppSKey rotation (D) is after session establishment and does not stop join-accept replay.

---

Q9. An enterprise is migrating its legacy three-tier web application to AWS. The security baseline requires that the presentation tier be able to initiate connections to the logic tier, but the logic tier must never initiate connections back to the presentation tier or to the Internet. Which combination of VPC constructs enforces this policy statefully and with the least operational overhead?  
A. Security-group outbound rules on the logic tier that deny 0.0.0.0/0, plus NACL rules that deny ephemeral ports inbound on the presentation subnet.  
B. Two subnets with a NAT Gateway in the presentation subnet, and security-group rules that reference each other’s group-id.  
C. Two subnets, each with its own security group; the logic-tier SG has no outbound rules, and the presentation-tier SG allows inbound from itself.  
D. Distributed firewall agents on every EC2 instance managed by an Ansible playbook.  

Correct Answer: C  
Explanation: Security groups are stateful: if the presentation tier initiates, the return traffic is automatically allowed. By simply giving the logic-tier SG no outbound rules, AWS implicitly denies every initiated egress session, satisfying the requirement with one rule. NACLs (A) are stateless and require broad ephemeral-port ranges, creating overhead. NAT Gateway (B) still allows outbound from logic tier if routes exist. Distributed agents (D) add operational complexity.

---

Q10. A multinational corporation uses SD-WAN with dynamic path selection based on SLA measurements. The security team wants to stop any branch office from learning the internal topology yet still allow dynamic routing. Which combination of OSPF controls should be enabled on the SD-WAN routers?  
A. Totally-Stubby areas with encrypted OSPF LSA packets.  
B. OSPF TTL security check plus MD5 authentication.  
C. OSPF demand circuit and passive-interface default.  
D. Not-So-Stubby-Area (NSSA) with default-information-originate and encrypted GRE.  

Correct Answer: D  
Explanation: NSSA blocks external (type-5) LSAs while still allowing branches to receive only a default route, hiding the rest of the topology. Adding encrypted GRE keeps the LSAs confidential on the transport. Totally-Stubby (A) also hides topology but is Cisco-proprietary and does not encrypt. TTL check and MD5 (B) authenticate neighbours but still flood LSAs. Demand circuit (C) reduces chatter but does not hide topology.
Q1. A global retailer is migrating its PCI-DSS in-scope payment traffic from dedicated 1 Gbps MPLS links to an SD-WAN fabric that dynamically chooses between multiple underlay transports (MPLS, DIA, LTE). The CISO is concerned that, on some paths, traffic will traverse the public Internet without encryption. Which SD-WAN feature should the architect enable to ensure continuous confidentiality no matter which path is selected?  
A. Application-aware QoS policies  
B. Always-on, transport-independent AES-256 VPN tunnels  
C. Dynamic path selection based on SLA probes  
D. Split tunneling for card-holder-data traffic  

Correct Answer: B  
Explanation: SD-WAN creates an overlay; to guarantee confidentiality when traffic may traverse untrusted networks (e.g., DIA or LTE), the overlay must be encrypted end-to-end with a cipher such as AES-256. Option B provides that persistent encryption regardless of the underlay. QoS (A) and path selection (C) do not address confidentiality. Split tunneling (D) would actually expose traffic.

---

Q2. A hospital uses IEEE 802.11ac Wi-Fi for both guest Internet and patient monitors. The monitors only support WPA2-PSK, but the hospital wants to segment them from guests and enforce per-device certificate-based access. Which option best meets the requirement while keeping the legacy monitors online?  
A. Deploy a separate SSID with WPA3-Enterprise and MAC whitelist the monitors.  
B. Put monitors on a dedicated SSID using WPA2-PSK, tunnel their traffic to a firewall via GRE, and enforce device certificates at the firewall.  
C. Keep WPA2-PSK for monitors, tag the SSID with a unique VLAN, and apply NAC with MACsec on switch ports.  
D. Deploy an EAP-TLS overlay on the same SSID; monitors fall back to WPA2-PSK while new devices use WPA3-Enterprise.  

Correct Answer: D  
Explanation: The monitors cannot do 802.1X, so WPA3-Enterprise (A) or pure EAP-TLS (D) alone will break them. Option D allows legacy devices to remain on PSK while newer devices use certificate-based EAP-TLS on the same air interface, achieving segmentation via different VLANs or ACLs pushed by the WLC. GRE tunnel (B) and MACsec (C) do not solve the Wi-Fi authentication gap.

---

Q3. A company’s cloud-first strategy forces all branch Internet traffic through a Secure Access Service Edge (SASE) provider. After cutover, VoIP Mean Opinion Score (MOS) drops and packets arrive out of order. Which SASE feature is most likely misconfigured?  
A. TLS 1.3 deep inspection  
B. MTU clamping at 1280 bytes  
C. Unequal-cost multipath load balancing without packet replication  
D. DNS sink-holing of CDNs  

Correct Answer: C  
Explanation: SASE gateways often use multiple POP paths for load sharing. If packets belonging to the same 5-tuple are sprayed across paths with different latency/jitter, they arrive reordered, destroying RTP MOS. Packet replication or flow-pinning fixes this. Deep inspection (A) adds latency but not reordering. MTU clamping (B) could fragment but not reorder. DNS sinkhole (D) is unrelated.

---

Q4. A DevOps team wants to expose a new containerized microservice only to other pods in the same Kubernetes namespace. Which Kubernetes object enforces that restriction at L3/L4?  
A. Ingress  
B. NetworkPolicy  
C. Service mesh sidecar  
D. LimitRange  

Correct Answer: B  
Explanation: Kubernetes NetworkPolicy is the native L3/L4 firewall construct that selects pods via labels and controls ingress/egress to/from those pods. Ingress (A) is L7 HTTP routing into the cluster. A sidecar (C) adds mTLS and L7 policy but is not the base L3/L4 enforcement. LimitRange (D) constrains compute resources, not traffic.

---

Q5. An OT site has legacy PLCs that only support Modbus over TCP/502 and cannot be patched. The plant firewall must allow remote SCADA clients to reach the PLCs while blocking reconnaissance and exploitation attempts. Which control is MOST effective?  
A. Reverse-proxy Modbus with deep packet inspection and Stateful DPI-rules allowing only predefined function codes  
B. Migrate PLCs to Modbus/TLS  
C. Deploy a next-generation IPS in monitor-only mode  
D. Require SCADA clients to connect through an IPsec VPN and leave TCP/502 open  

Correct Answer: A  
Explanation: A reverse proxy can enforce a positive security model—whitelisting only the Modbus function codes the PLCs actually use, blocking malformed packets, and hiding the PLC firmware versions. Migration (B) is impossible on unpatchable devices. Monitor-only IPS (C) does not block. VPN (D) provides confidentiality but no application-layer filtering.

---

Q6. A security analyst reviews a Wireshark capture from a user VLAN and sees DHCP replies offering option 66 (TFTP server) and option 67 (bootfile) that did not originate from the official Windows DHCP server. Which attack is in progress and which control stops it immediately?  
A. DNS hijack; disable option 66/67 on the scope  
B. Rogue DHCP; enable DHCP snooping on the switch  
C. ARP spoofing; static ARP entries  
D. VLAN hopping; change native VLAN  

Correct Answer: B  
Explanation: An unauthorized DHCP server is a classic rogue DHCP attack used to feed malicious TFTP bootfiles (PXE hijack). DHCP snooping blocks untrusted switch ports from sending DHCP offer/ack packets, stopping the attack instantly. DNS hijack (A) is unrelated. ARP spoofing (C) and VLAN hopping (D) are different attacks.

---

Q7. A multinational firm must comply with Schrems II and keep EU personal data inside the EU. Employees worldwide need low-latency access to a SaaS HR portal hosted in the U.S. Which architecture BEST satisfies both privacy and performance?  
A. Regional MPLS to U.S. SaaS with TLS 1.3  
B. Peer the SaaS provider with a local EU IaaS, store EU data there, and use a private L2VPN between SaaS POPs  
C. Host a second instance of the HR portal in EU cloud and use geo-DNS with data-sync that keeps EU data in-region; global users hit nearest POP  
D. Force all users through a U.S. VPN concentrator and log every query  

Correct Answer: C  
Explanation: Data residency requires EU data to stay in the EU. Option C achieves this by running a separate instance in-region and using geo-DNS so EU users (and only EU data) stay local, while still giving global users low latency. Private L2VPN (B) still ships data to the U.S. VPN concentrator (D) fails residency and adds latency.

---

Q8. A company runs an internal CA and wants to prevent users from bypassing its forward-proxy by typing https://1.1.1.1 (IP address literal). Which TLS proxy feature must be enabled?  
A. SNI inspection and block when SNI is missing or equals the IP  
B. Certificate pinning  
C. OCSP stapling  
D. TLS session resumption  

Correct Answer: A  
Explanation: When a browser uses an IP literal, the TLS ClientHello either omits the SNI extension or contains the IP as SNI value. A proxy that inspects SNI can drop such handshakes, forcing the user through the proxy where policy is enforced. Certificate pinning (B) is for integrity of specific sites. OCSP (C) and session resumption (D) do not control IP-literal bypass.

---

Q9. A SOC sees lateral movement where attackers used IPv6 link-local addresses to pivot between Windows hosts that had IPv4 disabled on the NIC but still had IPv6 enabled by default. Firewalls only filtered IPv4. Which hardening step closes the gap with LEAST operational impact?  
A. Disable IPv6 protocol on every host via registry  
B. Deploy host-based firewall rules blocking all link-local (fe80::/10) inbound except RADIUS-assigned VLAN  
C. Configure RA Guard on switchports  
D. Filter IPv6 at the perimeter firewall  

Correct Answer: C  
Explanation: RA Guard drops rogue Router Advertisements and other link-local traffic at the switch, preventing on-segment pivoting without touching hosts. Disabling IPv6 (A) can break Windows services (e.g., DirectAccess). Host firewalls (B) are harder to scale. Perimeter IPv6 filters (D) do not stop internal lateral movement.

---

Q10. A zero-trust architect must choose a session-broker technology that provides mutual TLS, fine-grained policy per application, and can hide internal RFC-1918 addresses from external users. Which option fits best?  
A. IPsec VTI tunnel  
B. ZTNA / Software-Defined Perimeter (SDP) gateway  
C. L2TPv3 pseudowire  
D. GRE tunnel with IPSec transport mode  

Correct Answer: B  
Explanation: ZTNA/SDP gateways terminate mutual TLS from users, authenticate via identity provider, enforce per-app policy, and use outbound-only connections so internal IPs are never exposed. IPsec VTI (A) and GRE/IPSec (D) expose both networks. L2TPv3 (C) is L2 and lacks identity-based policy.
Q1. A global SaaS provider has deployed an anycast-based DDoS-scrubbing service that advertises the same /24 prefix from 12 scrubbing centers. During a volumetric attack, the provider’s SOC notices that traffic destined to the scrubbed IP range is being black-holed in APAC although the scrubbing nodes in that region are operational and the BGP advertisements look stable. Which of the following anycast routing characteristics is the MOST likely root cause?  
A. Local preference manipulation by an upstream APAC carrier is overriding the AS-path length.  
B. The scrubbing centers are using TCP-MD5 passwords that are mismatched with the upstream providers.  
C. A ROV (Route Origin Validation) filter is rejecting the anycast prefix in APAC because the RPKI ROA covers only the ARIN region.  
D. The anycast nodes are advertising the /24 with the BGP NO_EXPORT community, preventing propagation outside each IBGP mesh.  

Correct Answer: C  
Explanation: Route Origin Validation (RPKI) is increasingly enforced by regional carriers. If the ROA signed by the SaaS provider only lists ARIN-route origins, APAC carriers with strict ROV filters will drop the anycast announcement, causing the prefix to be unreachable (black-holed) even though the scrubbing nodes are up and the BGP session is stable. Local preference (A) would affect path selection but not cause outright black-holing. TCP-MD5 (B) would break the BGP session entirely, which the stem says is not happening. NO_EXPORT (D) would keep the prefix inside each provider’s AS, but the symptom described is black-holing, not lack of global reachability.

------------------------------------------------------------------

Q2. A multinational bank is replacing its legacy MPLS WAN with an SD-WAN overlay that uses IPsec tunnels over commodity Internet. The security architecture team must ensure that branch-to-branch traffic never traverses the data center firewalls for east-west inspection. Which SD-WAN security construct BEST achieves this requirement while still permitting centralized policy management?  
A. Force all branch tunnels to hair-pin through a cloud-based secure web gateway.  
B. Enable full-mesh dynamic tunneling with distributed firewall rules pushed by the controller.  
C. Use a hub-and-spoke topology with the data center as the sole hub.  
D. Deploy GETVPN with group controllers located in the data center.  

Correct Answer: B  
Explanation: Dynamic full-mesh SD-WAN allows branches to build IPsec tunnels directly to one another while the controller distributes and enforces Layer-7 firewall policy on the edge devices. This keeps east-west traffic off the data-center firewalls yet retains centralized governance. Hair-pinning through a cloud SWG (A) still centralizes traffic and adds latency. Hub-and-spoke (C) deliberately forces traffic through the data center, violating the requirement. GETVPN (D) provides any-to-any encryption but still relies on a group controller and does not inherently provide firewalling or path optimization.

------------------------------------------------------------------

Q3. A company runs a real-time telemetry system on UDP port 5000 inside an AWS VPC. The security group allows 0.0.0.0/0 ingress on that port. Network ACLs are default. After enabling VPC Traffic Mirroring to an IDS appliance, the team sees only outgoing segments of the UDP flows. Which single change will cause the IDS to observe both directions?  
A. Change the mirroring session type from “after-egress” to “before-egress”.  
B. Add an inbound rule to the Network ACL permitting UDP 5000.  
C. Change the mirroring filter to bidirectional for the UDP 5000 traffic.  
D. Enable “accept” traffic mirroring instead of “reject” mirroring.  

Correct Answer: C  
Explanation: VPC Traffic Mirroring uses a filter that can be directional (ingress, egress, or bidirectional). The stem states only outgoing segments are seen, indicating the filter is set to egress only. Selecting bidirectional (C) mirrors both ingress and egress packets. “After-egress” vs “before-egress” (A) affects timing, not directionality. Network ACLs (B) are stateless and already allow all inbound by default; they do not affect mirroring scope. “Accept vs reject” (D) is not a valid Traffic Mirroring parameter.

------------------------------------------------------------------

Q4. An enterprise 802.1X WLAN uses EAP-TLS with client certificates issued by the internal PKI. A new BYOD policy allows employees to onboard their personal phones using EAP-TTLS-PAP so that only user credentials (not device certs) are required. The security team discovers that a supplicant configured with TTLS can still connect to the original SSID that is intended for EAP-TLS only. Which hardening step BEST prevents this protocol downgrade?  
A. Deploy a separate physical WLC for BYOD and anchor it to a DMZ controller.  
B. Configure the AAA server to return different Filter-Id attributes based on EAP method.  
C. Create two different RADIUS policy sets on the NPS server and enforce EAP-TLS in the first set.  
D. Enable “EAP chaining” so that both user and machine auth are mandatory.  

Correct Answer: C  
Explanation: On Microsoft NPS (or any AAA server) you can create policy sets that tie an SSID to a specific EAP type. By restricting the corporate SSID policy set to only EAP-TLS, any client attempting TTLS will hit no matching policy and be rejected. Separate WLCs (A) adds cost and complexity without addressing the protocol negotiation. Filter-Id (B) can assign VLANs post-auth but cannot reject the wrong EAP method. EAP chaining (D) is a Cisco proprietary feature that still allows TTLS if the client doesn’t support chaining, so it does not enforce TLS-only.

------------------------------------------------------------------

Q5. A zero-trust vendor claims that moving from IPsec site-to-site VPNs to a micro-tunnel overlay “eliminates the need for cryptographic agility.” Which residual risk BEST refutes that claim?  
A. The micro-tunnel still relies on IKEv2 for initial key exchange, so quantum-vulnerable DH groups remain.  
B. Micro-tunnels use session tickets that expire every 24 h, forcing re-authentication.  
C. The overlay encrypts at Layer-7, making TLS version negotiation unnecessary.  
D. Micro-tunnels are proprietary, so interoperability testing is no longer required.  

Correct Answer: A  
Explanation: Cryptographic agility is the ability to migrate to new algorithms (e.g., post-quantum) without replacing the entire stack. Most micro-tunnel overlays still bootstrap security using IKEv2 or a similar key-exchange protocol that today employs finite-field or elliptic-curve Diffie-Hellman—both quantum-vulnerable. Therefore the need to swap algorithms in the future (agility) persists. Layer-7 encryption (C) does not remove the need for agility; TLS itself must evolve. Session expiry (B) is operational, not cryptographic. Proprietary code (D) is irrelevant to the mathematical risk.

------------------------------------------------------------------

Q6. A manufacturing plant deploys 300 IIoT sensors on an internal IPv6-only network. The firewall rule “ipv6 any any allow” is intentionally used because the sensors are on an isolated L2 segment. During a penetration test, the assessor is able to reach the sensors from the corporate Wi-Fi. Which misconfiguration is the MOST likely avenue?  
A. The access switch is acting as an IPv6 router and has a global unicast address on the same VLAN.  
B. The sensors are using SLAAC with privacy extensions, creating temporary addresses.  
C. The firewall has a link-local rule that permits neighbor-discovery packets.  
D. The Wi-Fi VLAN and sensor VLAN share the same flood domain due to a missing VLAN tag.  

Correct Answer: A  
Explanation: If the switch (or any dual-homed device) has IPv6 routing enabled and an interface in both the sensor VLAN and the Wi-Fi VLAN, it can forward packets between them even when the firewall rule is “any any allow” inside only one zone. The attacker simply routes through the switch, bypassing intended segmentation. Shared flood domain (D) would require L2 adjacency, which is less common if VLANs are configured. SLAAC privacy (B) and ND rules (C) do not create cross-VLAN reachability.

------------------------------------------------------------------

Q7. A company uses DNS-over-TLS (DoT) for all internal clients via a central resolver. The SOC wants to detect malware that uses DNS-over-HTTPS (DoH) to bypass the resolver. Which control provides the BEST visibility without decrypting TLS?  
A. Block port 443 at the perimeter to prevent DoH.  
B. Use TLS fingerprinting to identify browser-based DoH client hellos.  
C. Mirror 53/udp and apply statistical analysis for beaconing.  
D. Force all browsers to disable DoH via GPO.  

Correct Answer: B  
Explanation: JA3/JA3S fingerprinting can recognize the Client Hello of known DoH providers (Cloudflare, Quad9, Google) even inside TLS. Alerts can be raised when an internal host exhibits those fingerprints, giving visibility without decryption. Blocking 443 (A) breaks all HTTPS traffic. Mirroring 53/udp (C) misses DoH entirely. GPO (D) works for managed browsers but not for malware using its own TLS stack.

------------------------------------------------------------------

Q8. A cloud-native application uses mutual TLS (mTLS) between every micro-service. The security team rotates the SPIFFE certificates every 4 hours via an automated CI/CD pipeline. Despite this, an auditor flags “lack of perfect forward secrecy.” Which artifact in the mTLS handshake is the MOST likely reason?  
A. The services reuse the same session ticket key for 7 days.  
B. The SPIFFE certs are RSA-2048 and the cipher suite is TLS_RSA_WITH_AES_256_GCM_SHA384.  
C. The private keys are stored in an HSM but are not erased after each handshake.  
D. The CA certificate has a 15-year validity and a 4096-bit key.  

Correct Answer: B  
Explanation: TLS_RSA key exchange encrypts the premaster secret with the server’s RSA public key; if that RSA key is ever compromised, all past traffic can be decrypted (no PFS). Even with short-lived certificates, the key exchange method governs PFS, not the cert lifetime. Session tickets (A) affect resumption but not the original handshake’s PFS. HSM storage (C) and long-lived CA (D) do not change the cipher-suite choice.

------------------------------------------------------------------

Q9. A satellite-office router has two uplinks: an MPLS circuit and an Internet-based IPsec tunnel. EIGRP is run inside the MPLS cloud, while the tunnel runs BGP with the HQ data center. The site loses reachability to certain RFC 1918 subnets at HQ whenever the MPLS link fails, even though the IPsec tunnel stays up. Which design issue BEST explains the outage?  
A. The IPsec tunnel uses proxy identities that exclude the missing subnets.  
B. The BGP neighbor is configured with “bgp bestpath compare-routerid” which deprioritizes those routes.  
C. EIGRP has a lower administrative distance than BGP, so those prefixes are unreachable when EIGRP disappears.  
D. The tunnel interface has “ip tcp adjust-mss 1250” which fragments BGP packets.  

Correct Answer: A  
Explanation: Proxy IDs in crypto maps or VTI must match the interesting traffic. If the ACL defining the proxy identity does not include the missing RFC 1918 subnets, the tunnel will not encrypt/decrypt them, rendering them unreachable. Administrative distance (C) would affect route selection but not packet encapsulation. MSS clamping (D) affects TCP, not BGP reachability. Compare-routerid (B) is a tie-breaker and would not cause outright loss.

------------------------------------------------------------------

Q10. A developer deploys a containerized gRPC service on Kubernetes and exposes it via a NodePort. A NetworkPolicy allows ingress only from the API-Gateway namespace on TCP 9000. During testing, pods in the default namespace can still reach the service. Which Kubernetes networking behavior is the MOST probable cause?  
A. The container runtime is using host networking, bypassing the veth pair enforced by the NetworkPolicy.  
B. The gRPC service uses HTTP/2 which NetworkPolicies cannot inspect.  
C. The NodePort range is exempted from NetworkPolicy enforcement by the kube-proxy iptables rules.  
D. The CNI plugin is Calico in policy-only mode, which does not enforce ingress rules.  

Correct Answer: A  
Explanation: When a pod runs with hostNetwork: true it shares the node’s network namespace; traffic enters the node’s TCP stack before reaching the veth bridge where NetworkPolicy is enforced, effectively bypassing the policy. NodePort (C) is subject to policy as soon as the packet enters the pod’s namespace. HTTP/2 (B) is still TCP 9000 and is not exempted. Calico policy-only mode (D) enforces policy just fine; the issue is the pod’s network mode, not the CNI.
Q1. A multinational bank runs a legacy SWIFT gateway that still negotiates TLS 1.0 because two correspondent banks have not upgraded. The security team has placed the gateway in an isolated VLAN with strict ACLs, full-packet capture, and an inline TLS-aware IPS that can strip weak ciphers. During a routine audit, which residual risk remains the HIGHEST despite these compensating controls?  
A. Downgrade attacks that force the session to SSL 3.0, exposing the transaction to POODLE  
B. The IPS certificate-outage causing asymmetric routing and transaction replay  
C. VLAN hopping via double-tagged 802.1Q frames that lets an attacker reach the gateway  
D. Weak 3DES keys that let an attacker recover the plaintext after collecting 2³² blocks  
Correct Answer: A  
Explanation: The IPS can strip weak ciphers but cannot prevent a man-in-the-middle from downgrading the handshake to SSL 3.0 if both ends still offer it (TLS 1.0 implementations often retain SSL 3.0 for “interop”). POODLE then recovers session cookies or credentials. The VLAN ACLs and packet capture do not stop ciphertext recovery at the endpoints; they only limit lateral movement and provide evidence. 3DES risk (D) is real but requires huge volumes; VLAN hopping (C) is mitigated by the switch configuration; IPS outage (B) is operational, not cryptographic.

------------------------------------------------------------------

Q2. A zero-trust architecture project requires that every east-west flow between containerized microservices is mutually authenticated with SPIFFE IDs and encrypted with mTLS. The DevOps team complains that CPU spikes 35 % when service-A calls service-B 4 000 times per second. Which control BEST preserves the security model while reducing load?  
A. Replace mTLS with IPSec tunnels between worker nodes so payloads remain encrypted  
B. Issue 24-hour SPIFFE SVIDs and cache the TLS session with session-resumption tickets  
C. Terminate mTLS at a sidecar proxy and run clear-text HTTP/2 over the loopback interface  
D. Move authentication to JWT signed by the node-level Envoy and disable TLS inside the cluster  
Correct Answer: B  
Explanation: Session-resumption (RFC 8446) reduces full-handshake RSA/ECDSA operations by ≈80 % while keeping mutual authentication and short-lived SVIDs. IPSec (A) still encrypts but does not give per-service identity; loopback cleartext (C) violates the zero-trust “encrypt every hop” principle; JWT without TLS (D) leaks metadata and is replayable if keys rotate slowly.

------------------------------------------------------------------

Q3. A hospital uses IEEE 802.11ac for VoWiFi handsets and MRI trolleys. The network team enables 802.11r (fast BSS transition) to avoid call drops during roaming. A red-teamer demonstrates she can decrypt 30 seconds of RTP traffic without ever possessing the PSK. Which design flaw MOST likely enabled this?  
A. 802.11r’s FT handshake reuses the same pairwise master key identifier across APs, letting an attacker recover the PTK via nonce reuse  
B. The handsets accept any AP advertising the same SSID and channel, enabling an evil-twin  
C. The PSK is printed on a label on every handset, simplifying insider threat  
D. 802.11k neighbor reports leak the PSK in the information element  
Correct Answer: A  
Explanation: 802.11r’s FT protocol short-cuts re-authentication by deriving new PTKs from the same PMK-R1. If the AP increments the ANonce incorrectly (or the supplicant reuses SNonce), the PTK can be solved from two frames. Evil-twin (B) would still need the PSK to enter the network; printed PSK (C) is social engineering, not a protocol flaw; 802.11k (D) carries no key material.

------------------------------------------------------------------

Q4. A cloud-native company uses QUIC for its public API. The CISO wants to block outbound data exfiltration without decrypting end-to-end encrypted streams. Which control gives the BEST trade-off between privacy and visibility?  
A. Deploy a transparent proxy that strips QUIC and falls back to HTTP/2 for inspection  
B. Force UDP/443 to TCP/443 via a firewall and inspect standard TLS  
C. Use eBPF on the host to sample QUIC SNI and entropy of first application data to detect tunneling  
D. Block QUIC entirely and whitelist only CDNs that support TCP-TLS  
Correct Answer: C  
Explanation: eBPF can read unencrypted parts of QUIC (SNI, length, timing) and apply heuristics (high entropy, long duration) to flag C2 or exfil without full MiTM, preserving end-to-end encryption. Stripping QUIC (A) breaks the protocol and user experience; TCP fallback (B) is unreliable and still needs certificates; blanket block (D) harms performance and does not stop other UDP tunnels.

------------------------------------------------------------------

Q5. A manufacturer deploys 10 000 IP-based security cameras that boot with manufacturer-signed firmware but use unsigned TR-069 configurations downloaded every night. An attacker on the ISP link flips a single bit in the config, causing cameras to send their RTSP streams to an attacker-controlled multicast group. Which control would have PREVENTED the compromise?  
A. TLS 1.3 with mutual certificate pinning for TR-069 sessions  
B. A firmware update that validates the config file signature against the manufacturer’s public key  
C. 802.1X on every camera port to stop rogue DHCP servers  
D. IPSec tunnels from each camera to the management VRF  
Correct Answer: B  
Explanation: The root cause is lack of integrity check on the configuration blob itself. Even with TLS (A) or IPSec (D), the file can still be modified at the ACS server or in transit if not signed. 802.1X (C) only controls network admission, not post-connect data integrity. Only a signature check at boot/parse time guarantees the config has not been altered.

------------------------------------------------------------------

Q6. A global SD-WAN uses dynamic IPSec tunnels with IKEv2 and 60-minute rekeys. A branch in Nairobi experiences 800 ms RTT and 2 % packet loss; tunnels flap every 3–4 minutes, causing VoIP drops. Which IKEv2 feature should be tuned FIRST to stabilize the tunnel?  
A. Enable IKEv2 make-cookie for DoS protection  
B. Increase DPD (Dead-Peer-Detection) interval from 10 s to 60 s  
C. Switch from main mode to aggressive mode to reduce round trips  
D. Lower the IPSec SA lifetime to 5 minutes to recover faster  
Correct Answer: B  
Explanation: Aggressive DPD on lossy links falsely declares the peer dead when replies are simply delayed. Raising the interval reduces premature teardowns. Make-cookie (A) is anti-DoS, not anti-flap; aggressive mode (C) saves one RTT at setup but does not help rekeys; shorter lifetime (D) increases rekey frequency, making the problem worse.

------------------------------------------------------------------

Q7. A company runs IPv6 internally with RA-guard enabled on access switches. A new IoT kettle, which is SLAAC-only, still manages to announce itself as a default router and redirects all traffic through it. What is the MOST plausible explanation?  
A. The kettle tunnels IPv6 inside IPv4 GRE to bypass RA-guard  
B. The switch is misconfigured to check only the source MAC, and the kettle uses forged ICMPv6 RAs with the same MAC as the legitimate router  
C. RA-guard drops only RAs with hop-limit ≠ 255, and the kettle sets hop-limit 255  
D. The kettle uses DHCPv6 to request option 25 (IPv6 routes) which RA-guard does not police  
Correct Answer: B  
Explanation: Many switches implement RA-guard by comparing the Ethernet source MAC to an allowed list. If the kettle spoofs the same MAC as the real router, the frame passes. GRE (A) is overkill for a kettle; hop-limit 255 (C) is the expected value and would be allowed; DHCPv6 (D) is not used by SLAAC devices and option 25 is rare.

------------------------------------------------------------------

Q8. A financial exchange offers colocated traders 10 Gbps Ethernet with sub-100 ns latency. The exchange recently added MACsec (IEEE 802.1AE) between every server and the top-of-rack switch. A high-frequency trading firm claims that latency increased 6 µs per hop and wants to remove encryption. Which argument BEST justifies keeping MACsec without violating the 100 ns budget?  
A. Enable MACsec confidentiality-only (no integrity check) to save time  
B. Use a hardware-security-module (HSM) offload on the NIC so encryption overlaps cut-through switching  
C. Switch to 256-bit GCM to reduce tag size and latency  
D. Disable MACsec and move encryption to the application to regain latency  
Correct Answer: B  
Explanation: Modern 10 G NICs perform MACsec in ASIC with cut-through; the added latency is <40 ns when offloaded, well under the 100 ns budget. Confidentiality-only (A) is non-standard and breaks integrity; longer GCM (C) increases latency; application crypto (D) adds CPU context switches and jitter, harming determinism more than MACsec.

------------------------------------------------------------------

Q9. A SaaS provider gives each customer a dedicated VRF and uses MPLS L3VPN from the provider’s PE routers. A new customer insists on end-to-end encryption because they fear label spoofing by other tenants. Which technology gives encryption that is terminate-to-terminate across the provider cloud without requiring customer-managed IPSec on every site?  
A. MACsec on provider edge links  
B. GETVPN with group-shared keys managed by the provider  
C. L2TPv3 over MPLS  
D. DMVPN with PKI certificates  
Correct Answer: B  
Explanation: GETVPN preserves the provider’s native routing (no tunnels) while encrypting customer packets at the CE or PE with group keys, so every site can decrypt without pairwise IPSec SAs. MACsec (A) is link-layer and hop-by-hop; L2TPv3 (C) is a pseudowire, not L3VPN; DMVPN (D) builds overlay tunnels, defeating MPLS optimization and requires customer PKI.

------------------------------------------------------------------

Q10. A satellite ISP uses a bent-pipe geostationary link (RTT 550 ms) to connect cruise ships to the Internet. The operator wants to deploy TLS 1.3 for guest Wi-Fi but finds that many Android 6 phones take 4–5 seconds to complete the handshake. Which TLS 1.3 extension offers the BIGGEST reduction in handshake time for these legacy devices?  
A. 0-RTT early data  
B. Server-sent session-tickets for resumption with PSK  
C. HelloRetryRequest to pick a mutually supported group  
D. Certificate compression  
Correct Answer: B  
Explanation: Session resumption with PSK reduces the handshake to one RTT (550 ms) on the second connection even on old Android, and works without 0-RTT support (which those phones lack). 0-RTT (A) is not available on Android 6; HelloRetryRequest (C) adds an extra RTT; cert compression (D) saves ~4–6 kB, insignificant on a 1 Mbps satellite channel compared with latency.
Q1. A global retailer is migrating its legacy MPLS WAN to an SD-WAN architecture that uses IPSec tunnels over the public Internet. Each branch currently has a single CE router that connects to two different ISPs. The security team is asked to recommend a control that will prevent an attacker in one ISP from replaying traffic into the other ISP and corrupting the retailer’s central inventory database.  
A. Enforce 802.1X on every CE router port to stop unauthorized devices from injecting frames.  
B. Configure the SD-WAN edge to negotiate IKEv2 with AES-GCM, enabling built-in anti-replay.  
C. Deploy a private 5G overlay so that traffic never touches the public Internet.  
D. Add SHA-256 HMAC on top of the existing IKEv1 policy to detect tampering.  

Correct Answer: B  
Explanation: AES-GCM (used automatically when IKEv2 negotiates ESP with AES-GCM) provides confidentiality, integrity, and a 32-bit sequence number that functions as an anti-replay window. Any duplicated packet outside the window is dropped by the receiving SD-WAN edge, neutralizing the replay threat described. 802.1X (A) is a Layer-2 access control and does nothing against WAN-level replay. A private 5G overlay (C) is extremely costly, still requires IPSec for confidentiality, and does not itself stop replay. SHA-256 HMAC (D) adds integrity but IKEv1 still relies on manual crypto maps that lack an integrated anti-replay mechanism; without a sequence-number window the receiver cannot detect replays.

Q2. A hospital uses IEEE 802.11ac Wi-Fi for both guest Internet and patient-monitors that transmit HL7 messages. The CIO wants to segment the two traffic types without deploying a second set of APs. The solution must prevent a guest user from sending malicious packets to a patient-monitor and must work with existing tablets that only support WPA2-PSK.  
A. Broadcast two SSIDs, map each to a different VLAN, and use a firewall between VLANs.  
B. Deploy WPA3-Enterprise on the same SSID and assign group policies through a NAC.  
C. Force all tablets to use 802.1X with EAP-TLS, then tag traffic with VXLAN.  
D. Enable Wi-Fi Multimedia (WMM) power-save to reduce the duty cycle of guest traffic.  

Correct Answer: A  
Explanation: Dual-SSID designs are the simplest way to achieve Layer-3 segmentation on a single AP infrastructure. Each SSID is mapped to a unique VLAN; an inline firewall filters inter-VLAN traffic, blocking guests from reaching the medical device subnet. WPA3-Enterprise (B) and 802.1X/EAP-TLS (C) are incompatible with the stated tablet limitation (WPA2-PSK only). WMM power-save (D) affects battery life, not segmentation or security policy.

Q3. A company is implementing IPv6 throughout its campus. Network engineers plan to use SLAAC so that workstations can configure themselves without DHCPv6. The CISO is concerned that rogue routers could advertise incorrect prefixes and redirect traffic through an attacker-controlled on-path device. Which control provides the strongest mitigation while still allowing SLAAC?  
A. RA-Guard on all access-layer switches, enforced on ports facing end-stations.  
B. SeND (Secure Neighbor Discovery) with CGAs and RSA signatures on router advertisements.  
C. Require DHCPv6 instead of SLAAC so that only the authorized server gives out addresses.  
D. Disable IPv6 on all user VLANs and tunnel it inside IPv4 GRE to the core.  

Correct Answer: B  
Explanation: SeND cryptographically validates router advertisements using RSA signatures and CGAs (Cryptographically Generated Addresses), making it impossible for an attacker to forge a valid RA while still permitting stateless address configuration. RA-Guard (A) is helpful but can be bypassed by double-tagging or if the switch is misconfigured; it is a filtering, not a cryptographic, control. Moving to DHCPv6 (C) abandons the SLAAC requirement in the scenario. Tunneling IPv6 inside GRE (D) adds complexity and does not stop rogue RAs once the tunnel is decapsulated.
