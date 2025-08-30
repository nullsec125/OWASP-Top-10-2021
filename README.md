I created this repository for anyone interested in having a single, "cheat-sheet" styled, reference page for each vulnerability on OWASP's Top 10 (2021) list.
Hopefully this source of key details can help people become cohesive and grounded in honing Web Application PenTesting understanding. 

Each entry assumes a fundamental understanding of BurpSuite, and contains data from the relevant Portswigger rooms, and within each you can find:
- What is the vulnerability
- The CIA impact
- Where to test for the vulnerability
- Common payloads/tricks
- How to identify the vulnerability
- Mitigations for the vulnerability
- Potential cheat cheets/references

## Index

### A01 – Broken Access Control
- [Broken Access Control](A01-Broken-Access-Control/A01-Broken-Access-Control.md)

### A02 – Cryptographic Failures
- [Cryptographic Failures](A02-Cryptographic-Failures/Cryptographic-Failures.md)

### A03 – Injection
- [SQL Injection](A03-Injection/SQLi.md)
- [Cross-Site Scripting (XSS)](A03-Injection/XSS.md)
- [XML External Entities (XXE)](A03-Injection/XXE.md)
- [Command Injection](A03-Injection/Command-Injection.md)

### A04 – Insecure Design
- [Race Conditions](A04-Insecure-Design/Race-Conditions.md)
- [Business Logic Vulnerabilities](A04-Insecure-Design/Business-Logic-Vulns.md)

### A05 – Security Misconfigurations
- [CORS](A05-Security-Misconfigurations/CORS.md)
- [File Upload](A05-Security-Misconfigurations/File-Upload.md)
- [Path Traversal](A05-Security-Misconfigurations/Path-Traversal.md)
- [Web Cache Deception](A05-Security-Misconfigurations/Web-Cache-Deception.md)
- [Web Cache Poisoning](A05-Security-Misconfigurations/Web-Cache-Poisoning.md)

### A06 – Vulnerable + Outdated Components
- [Notes](A06-Using-Components-with-Known-Vulnerabilities/Notes.md)

### A07 – Identification & Authentication Failures
- [OAuth](A07-Broken-Authentication/OAuth-Authentication.md)
- [JWT](A07-Broken-Authentication/JWT-Attacks.md)

### A08 – Software & Data Integrity Failures
- [Prototype Pollution](A08-Software-and-Data-Integrity-Failures/Prototype-Pollution.md)
- [Insecure Deserialization](A08-Software-and-Data-Integrity-Failures/Insecure-Deserialization.md)

### A09 – Security Logging & Monitoring Failures
- [Notes](A09-Insufficient-Logging-and-Monitoring/Notes.md)

### A10 – Server-Side Request Forgery (SSRF)
- [Notes](A10-SSRF/Notes.md)
