IOC 11 – Malicious PDF Redirect via Embedded Link

Overview
This case study examines an obfuscated phishing attempt embedded in a PDF file. The attack relied on user interaction to initiate a hidden redirect to a typosquatted phishing domain. No malware was dropped, no process was overtly malicious, and the PDF appeared benign—until it triggered a covert network egress through a legitimate application (Adobe Reader). The attacker’s goal was credential harvesting via social engineering and DNS evasion.

Key IOC Highlights
Source of IOC: EDR (Endpoint Detection and Response) alert on suspicious PDF→browser behavior chain

Triage Type: Social Engineering / Obfuscated Link

Process Chain: AcroRd32.exe (Adobe Reader) → msedge.exe (Microsoft Edge)

Indicator Artifacts: DNS query to typosquatted domain, hyperlink embedded in PDF metadata

Cross-Layer Activity: Involved OS Layer 1 (process), Layer 6 (network egress), and Layer 5 (EDR log activity)

Attacker Tactics
Fileless delivery via trusted application

User-triggered execution

Exploitation of weak DNS filtering

Redirect chaining to mask destination

Deceptive social engineering embedded in legitimate document

Defender Response
PDF isolated and sandboxed for analysis

Embedded URL decoded and linked to malicious infrastructure

DNS logs used to confirm outbound attempt

EDR detection rule updated to flag similar behavior chains

User notified and workstation segmented from broader network

Educational Value
This IOC emphasizes the subtlety of real-world phishing techniques that do not rely on payloads, but on user behavior and overlooked telemetry paths (e.g., DNS, PDF metadata, and browser spawning). It demonstrates the necessity of:

DNS content filtering

Behavioral correlation rules

Endpoint telemetry interpretation

Deep cross-layer investigative practices
