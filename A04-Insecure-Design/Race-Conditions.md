# Race Conditions

## Metadata
- **OWASP Category (2021):** A04 Insecure Design  
- **PortSwigger Link:** [Race conditions | Web Security Academy](https://portswigger.net/web-security/race-conditions)

---

## 💡 Concept
- **What is it?**  
> - Race conditions occur when the outcome of a process depends on the timing or order of operations.  
> - Attackers exploit "race windows" by making multiple requests simultaneously or in rapid succession, causing the application to behave in unintended ways.  

- **Impact**  
> - **Confidentiality:** May allow attackers to read sensitive data through unintended concurrent execution.  
> - **Integrity:** Enables double-spending, balance manipulation, or bypassing authorization checks.  
> - **Availability:** Could overload systems, cause corruption of states, or denial of service.  

---

## 🛠 Exploitation Notes
- **Where to test:**  
> - Endpoints with state-dependent logic (checkout, balance updates, coupon redemption).  
> - Multi-step processes (e.g. basket add + payment confirm).  
> - APIs where operations must be sequential.  

- **Payloads**  
> - Limit overrun exploitation: Reusing a discount code multiple times by firing requests in parallel.  
> - Multi-endpoint race: Exploit delays across related endpoints (`/addItem` + `/checkout`).  
> - Single-endpoint race: Sending parallel password reset requests to hijack sessions.  
> - Partial construction race: Interfering during object creation (e.g. API keys, hashes).  
> - Time-sensitive attacks: Exploiting predictable timestamps used for validation.  

---

## 🔍 Detection
- **How to identify in apps:**  
> - Look for functionality with business logic limits (e.g. coupons, balance updates).  
> - Send simultaneous requests and analyze server responses for inconsistencies.  
> - Probe for state transitions (two "success" results where only one should exist).  

---

## 🛡 Mitigation
> - Use atomic database operations (transactions, row-level locks).  
> - Apply synchronization/locking mechanisms for critical operations.  
> - Validate state changes at each step (double-check after updates).  
> - Avoid predictable identifiers (e.g. timestamps) for sensitive actions.  
