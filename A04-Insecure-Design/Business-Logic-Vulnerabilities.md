# Business Logic Vulnerabilities

## 📄 Metadata
- **OWASP Category (2021):** A04 Insecure Design  
- **PortSwigger Link:** [Business logic vulnerabilities | Web Security Academy](https://portswigger.net/web-security/logic-flaws)

---

## 💡 Concept
- **What is it?**  
> Flaws in the design of an application that allows an attacker to cause unintended behavior.  
> This can manipulate legitimate functionality to achieve a malicious goal – in a way unintended by the application owner.  
> Usually happen from assumptions about how interactions with the application would happen, stemming from not understanding how all areas of an application work.  

- **Impact**  
> **Confidentiality:** Poorly designed flows expose sensitive data by default.  
> **Integrity:** Weak logic enables unauthorized modification of transactions or records.  
> **Availability:** Flawed designs may allow DoS.  

---

## 🛠 Exploitation Notes
- **Where to test**  
> - Parameter values in multi-step processes (order amount, discount codes, user IDs)  
> - Headers/Cookies: flags like `is_premium=true`  
> - Body: form fields in checkout, account management, workflow actions  
> - Business workflows: registration, shopping carts, password resets, payment flows  

- **Tricks used**  
> - Change product price/quantities in hidden fields  
> - Submit unconventional input (negative values, nulls, huge numbers)  
> - Skip steps in a multi-step process (e.g. jump straight to "Confirm Order").  
> - Replay expired tokens or reuse coupons.  
> - Abuse race conditions  

---

## 🔍 Detection
- **How to identify in apps**  
> - Manual testing is key (logic flaws rarely show up in scanners!)  
> - Look for trust in client-side validation (e.g. prices only checked in frontend)  
> - Check for unhandled edge cases (large input, zero, negative)  
> - Observe behavior when business steps are skipped, reordered, or repeated  
> - Look for inconsistencies in error messages/unusual forms  
 - Burp Suite (Sequencer, Intruder for parameter manipulation)  

---

## 🛡 Mitigation
> - Validate all business rules server-side, never trust the client.  
> - Enforce workflow state.  
> - Adopt "secure by design" practices in development.  
> - Use WAFs / anomaly detection to catch unusual requests (e.g. negative prices).  
> - Implement logging for repeated abuse patterns (refund requests, bulk coupon use).  
> - Longer alerting when workflows are skipped or accessed abnormally.  

---

## 📚 Extras
- **Cheat sheet / references:** [A04 Insecure Design – OWASP Top 10:2021](https://owasp.org/Top10/A04_2021-Insecure_Design/)

