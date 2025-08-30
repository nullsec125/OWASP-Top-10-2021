# JWT Attacks

---

## Metadata
- **OWASP Category (2021):** A02 Cryptographic Failures  
- **PortSwigger Link:** [JWT attacks | Web Security Academy](https://portswigger.net/web-security/jwt)

---

## 💡 Concept
- **What is it?**  
> Occurs when flaws in JWT implementation, misconfiguration, or weak key management allow attackers to forge/manipulate tokens. Exploits authentication or session mismanagement.  
> * JSON Web Tokens are compact, URL-safe formats for representing claims (used for authentication and access management).  
> * JWTs are cryptographically signed to prevent tampering.

- **Impact:**  
> - **Confidentiality:** Attacker may read or forge tokens to gain unauthorized access to sensitive user data.  
> - **Integrity:** Forged JWTs allow attackers to modify claims (privilege escalation).  
> - **Availability:** Weak implementations may be exploited for brute-force/denial-of-service attacks (signature validation).  

---

## 🛠 Exploitation Notes
- **Where to test:**  
> - Authentication headers (`Authorization: Bearer <JWT>`)  
> - Cookies carrying JWTs  
> - Query parameters or body fields containing tokens  
> - Token storage  

- **Tricks used:**  
> - **None/alg=none attacks:** Changing JWT header to `"alg": "none"` → some servers may accept unsigned tokens.  
> - **Weak secret brute-force:** If HMAC is user-supplied in application incorrectly, attackers can brute force with tools like `jwtcrack`.  
> - **Key confusion attacks:** Swap algorithm types (e.g., `RS256` → `HS256`) with weak secret.  
> - **Claim abuse:** Modify token claims (role: admin, user: X) and bypass access control.  
> - **Expiration tampering:** Change `exp` to extend session validity.  
> - **JWK injection:** Supplying a malicious JSON Web Key via `jku` or `kid` pointing to attacker-controlled domain.  

---

## 🔍 Detection
> - Decode JWTs (Base64 decode header & payload) → check for suspicious claims.  
> - Modify `alg` values → test if server accepts HS256/RS256 swaps or `none` algorithm.  
> - Check logs & session behavior for unusual token acceptance.  
> - Try manipulating claim values (role=admin, user=id).  
> - JWT fuzzers / Burp extensions useful for brute-forcing weak secrets.  

---

## 🛡 Mitigation
> - Always enforce strong signing algorithms (RS256 with strong secret, HS256 with correct validation).  
> - Validate `alg` → **must** be explicitly configured.  
> - Block `"none"` and algorithm downgrades.  
> - Validate JWT claims: issuer, subject, audience, expiration.  
> - Rotate & revoke keys regularly.  
> - Enforce strict server-side session & role validation.  
> - Use libraries with secure defaults, not DIY JWT implementations.  
> - Ensure secure key storage (no JWT secret in code / .git).  

---

## Extras
- Cheat sheet / references: [https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/JSON_Web_Token_for_Java_Cheat_Sheet.html)
