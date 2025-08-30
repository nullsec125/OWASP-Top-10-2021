# OAuth Authentication  

## Metadata  
- **OWASP Category (2021):** A07 Broken Authentication  
- **PortSwigger Link:** [OAuth 2.0 authentication vulnerabilities | Web Security Academy](https://portswigger.net/web-security/oauth)  

---

## 💡 Concept  
- **What is it?**  
> OAuth 2.0 is an authorization framework that allows third-party applications to obtain limited access to user accounts without exposing credentials.  
> Vulnerabilities arise when OAuth is implemented incorrectly, allowing attackers to steal access tokens, hijack sessions, or escalate privileges.  

- **Impact**  
> - **Confidentiality:** Attackers can steal access tokens or authorization codes to read sensitive data.  
> - **Integrity:** Exploiting flow may let attackers forge identities or tamper with permissions.  
> - **Availability:** Abuse of OAuth endpoints or CSRF flaws can disrupt authentication flows, lock accounts, or cause DoS.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - Authorization URLs (`/authorize?client_id=...`)  
> - Redirect URLs (`redirect_uri` parameters).  
> - Access tokens in headers, fragments, or cookies.  
> - Parameters in OAuth flows: `state, scope, response_type, client_id, redirect_uri`  

- **Tricks used:**  
> - Improper implementation of Implicit Flow: Steal access tokens from URL fragments.  
> - Flawed CSRF protection: Reuse OAuth authorization requests to force-link accounts.  
> - Leaking authorization tokens: Tokens appear in logs, referrer headers, or exposed redirects.  
> - Forced linking attacks: Victim’s session linked to attacker-controlled account.  
> - Open redirects in redirect_uri: Abuse redirects to capture tokens or codes.  

---

## 🔍 Detection  
> - Look for OAuth flows in login pages (`Sign in with Google/Facebook`).  
> - Inspect redirects and `state` handling; missing `state = CSRF risk`.  
> - Check tokens stored in URL fragments or cookies.  
> - Test for open redirects in `redirect_uri` parameter.  
> - Try forced linking by manipulating requests in Burp Repeater.  

---

## 🛡️ Mitigation  
> - Always use authorization code flow instead of implicit flow.  
> - Enforce strict redirect URI validation (whitelist exact URIs).  
> - Implement strong CSRF protection with the `state` parameter.  
> - Store tokens securely (not in URL/local storage).  
> - Use short-lived access tokens + refresh tokens.  
