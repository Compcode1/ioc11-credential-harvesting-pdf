🧾 IOC 11 – Credential Harvesting via Embedded PDF Redirect
Goal: Analyze a fileless phishing attack triggered by a user opening a deceptive PDF. The attack chain involved browser redirection to a typosquatted Microsoft login page without dropping malware. This case emphasizes detection through behavior analysis, EDR process chains, and network telemetry.

🎯 Project Objective
Investigate a fileless credential harvesting attempt embedded within a legitimate-looking PDF.

Validate cross-layer telemetry from EDR, DNS logs, and host process chains.

Map detection opportunities to Cybersecurity Battlefield telemetry layers.

🧪 Attack Simulation Summary
A malicious PDF contains an invisible hyperlink pointing to a shortened redirect URL.

Upon user click, Adobe Reader (AcroRd32.exe) spawns Microsoft Edge (msedge.exe) to open the link.

The browser performs a DNS lookup to trackupdate[.]info, which redirects to micros0ft-verify[.]com (a typosquatted phishing site).

The phishing site mimics a Microsoft login and collects user credentials.

No files were dropped; all activity occurred through legitimate processes.

🧱 Battlefield Framework Mapping
Host Layer Alignment:

Layer 1 – Process Execution

AcroRd32.exe launches msedge.exe

Triggered from user interaction via Adobe Reader

Layer 5 – Event Monitoring

EDR correlation flagged the unusual PDF → browser chain

Behavioral telemetry used to detect process flow anomalies

Layer 6 – Network Communication

DNS request to redirect domain

HTTP POST to phishing site captured in DNS/network logs

OSI Model Alignment:

Layer 7 – Application: PDF file and browser activity

Layer 4 – Transport: TCP-based HTTP POST

Layer 3 – Network: IP traffic routing to phishing domain

🔍 Detection Details (Telemetry Sources)
EDR Alert Triggered

Abnormal process chain: AcroRd32.exe → msedge.exe

DNS Logs

Resolution of trackupdate[.]info and micros0ft-verify[.]com

PDF Metadata Analysis

Embedded hyperlink located in a hidden text layer

No malware detected

Entire execution path remained fileless and relied on trusted tools

🚩 Tactics and Techniques
Phishing (Social Engineering)

Relied on user trust in PDF documents

Used visual familiarity and typosquatting to deceive

Redirect Obfuscation

URL shortener and multi-hop redirection masked final destination

Fileless Execution

No payloads; attack leveraged legitimate apps to evade AV

🧠 Lessons Learned
Unexpected PDF → browser behavior should be triaged immediately.

DNS filtering is critical for detecting and blocking typosquatted domains.

Behavior-based rules (EDR) are effective against fileless attacks.

Redirect chaining is a common technique for masking destination domains.

User education alone is not sufficient — telemetry-based defenses are essential.

🛠️ Tools and Data Sources
Endpoint Detection and Response (EDR) platform

DNS logs and firewall telemetry

PDF analysis tools (metadata inspection)

Browser process behavior tracking

🧭 Enterprise Analogy
This attack is like receiving an official-looking envelope from HR. It contains a form, but the link leads to a convincing fake login page. The system didn’t detect malware—because there wasn’t any. Instead, it had to detect that a trustworthy messenger took the user to the wrong building.


