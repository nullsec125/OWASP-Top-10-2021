# CSRF (Cross-Server Request Forgery)

### Metadata
- **OWASP Category (2021): A01 Broken Access Control**
- **PortSwigger Link:** https://portswigger.net/web-security/csrf

---

### 💡 Concept
- **What is it?**
 >  CSRF tricks an authenticated user’s browser into submitting unwanted actions on a web application in which they are currently authenticated.
 >
 > It exploits the trust a web app places in a user’s browser, forcing state-changing actions without the user’s knowledge.

- **Impact:**
> - Confidentiality: Attacker can steal sensitive user data indirectly if CSRF leads to account takeover.
> - Integrity: Can modify user data
> - Availability: Limited impact, but could disable accounts or lock users out.

---

### 🛠 Exploitation Notes
- **Where to test:**
> - Forms or endpoints that perform sensitive actions (password reset, fund transfers, email change, etc).
> - Look for requests that rely only on cookies/session IDs without requiring extra tokens or re-authentication.

- **Payloads/Tricks used:**
 > - Malicious HTML forms with hidden fields that auto-submit.
 >   **Example:**
 >   ```html
 >   <form action="https://vulnerable-website.com/changeEmail" method="POST">
 >     <input type="hidden" name="email" value="attacker@example.com" />
 >     <input type="submit" />
 >   </form>
 >   <script>document.forms[0].submit();</script>
 >   ```
 > - GET requests embedded in `<img>` or `<script>` tags when state-changing actions use GET.

---

### 🔎 Detection
- **How to identify in apps:**
> - Check whether important state-changing requests can be forged without a CSRF token.
> - See if authentication relies solely on cookies automatically sent by the browser.
> - Use tools like Burp Suite to replay sensitive requests without a CSRF token — if they succeed, the app is vulnerable.

---

### 🛡 Mitigation
> - Use Synchronizer tokens (CSRF tokens) tied to user sessions and validated server-side.
> - Prefer SameSite cookies with `Lax` or `Strict` settings to limit cross-site request contexts.
> - Require re-authentication or MFA for high-risk actions.
> - Avoid using GET requests for state-changing actions.
> - Implement secure request headers (e.g., `X-Requested-With`) and check origin/referrer headers when possible.
