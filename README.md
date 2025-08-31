![OWASP](https://img.shields.io/badge/OWASP-Top%2010-blue)  
![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Stars](https://img.shields.io/github/stars/nullsec125/OWASP-Top-10-2021?style=social)


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
- [Broken Access Control](A01-Broken-Access-Control/Broken-Access-Control.md)

### A02 – Cryptographic Failures
- [Information Disclosure](A02-Cryptographic-Failures/Information-Disclosure.md)
- [JWT Attacks](A02-Cryptographic-Failures/JWT-Attacks.md)

### A03 – Injection
- [Command Injection](A03-Injection/Command-Injection.md)
- [NoSQL](A03-Injection/NoSQL.md)
- [SQL Injection](A03-Injection/SQL-Injection.md)
- [Server-Side Template Injection (SSTI)](A03-Injection/SSTI-Server-Side-Template-Injection.md)
- [Cross-Site Scripting (XSS)](A03-Injection/XSS-Cross-Site-Scripting.md)
- [XML External Entities (XXE)](A03-Injection/XXE-XML-External-Entities-Injection.md)

### A04 – Insecure Design
- [Business Logic Vulnerabilities](A04-Insecure-Design/Business-Logic-Vulnerabilities.md)
- [Race Conditions](A04-Insecure-Design/Race-Conditions.md)

### A05 – Security Misconfigurations
- [CORS (Cross-Origin Resource Sharing)](A05-Security-Misconfigurations/CORS-Cross-Origin-Resource-Sharing.md)
- [File Upload Vulnerabilities](A05-Security-Misconfigurations/File-Upload-Vulnerabilities.md)
- [HTTP Host Header Attacks](A05-Security-Misconfigurations/HTTP-Host-Header-Attacks.md)
- [Path Traversal](A05-Security-Misconfigurations/Path-Traversal.md)
- [Web Cache Deception](A05-Security-Misconfigurations/Web-Cache-Deception.md)
- [Web Cache Poisoning](A05-Security-Misconfigurations/Web-Cache-Poisoning.md)

### A06 – Vulnerable and Outdated Components
- [Vulnerable and Outdated Components](A06-Vulnerable-and-Outdated-Components/Vulnerable-and-Outdated-Components.md)

### A07 – Identification & Authentication Failures
- [OAuth Authentication](A07-Broken-Authentication/OAuth-Authentication.md)

### A08 – Software & Data Integrity Failures
- [Insecure Deserialization](A08-Software-and-Data-Integrity-Failures/Insecure-Deserialization.md)
- [Prototype Pollution](A08-Software-and-Data-Integrity-Failures/Prototype-Pollution.md)

### A09 – Security Logging & Monitoring Failures
- [Security Logging and Monitoring](A09-Security-Logging-and-Monitoring/Security-Logging-and-Monitoring.md)

### A10 – Server-Side Request Forgery (SSRF)
- [Server-Side Request Forgery](A10-Server-Side-Request-Forgery/Server-Side-Request-Forgery.md)
