# Web Cache Deception

## Metadata
- **OWASP Category (2021):** A05 Security Misconfigurations
- **PortSwigger Link:** [Web cache deception | Web Security Academy](https://portswigger.net/web-security/web-cache-deception)

---

## 💡 Concept
- **What is it?**
> A vulnerability that allows attackers to trick caching servers (CDNs, reverse proxies, etc) into storing and serving sensitive dynamic content as if it were static.  
> *This enables unauthorized users to retrieve private user data (like account pages, personal details, or session info) through crafted URLs.*

- **Impact**
> - **Confidentiality:** Exposure of sensitive user data such as personal details, session tokens, account info.  
> - **Integrity:** Manipulation of cached responses can serve incorrect or malicious data.  
> - **Availability:** Attackers can poison caches, making services unreliable or exposing private data to multiple users.

---

## 🛠 Exploitation Notes
- **Where to test:**
> - Dynamic endpoints ( `/profile`, `/account`, `/dashboard` )
> - Parameters/URLs where static vs dynamic behavior may differ
> - Cache layers like CDNs, reverse proxies

- **Tricks used**
> - Adding fake static file extensions to URLs:  
>  `/profile` ➝ `/profile/fake.js`  
>  `/account` ➝ `/account/fake.css`
> - Using cache busters (`?cb=12345`) to force variations
> - Exploiting path mapping discrepancies (ex. `/api/v1/users/123` vs `/api/v1/users/123.css`)
> - Exploiting delimiter discrepancies (ex. `/profile;jsessionid=123`)
> - Exploiting normalization differences (encoded characters like `%2e`, `%2f`)

---

## 🔍 Detection
> - Look for differences in handling between cache and origin server
> - Observe headers like `Cache-Control`, `ETag`, and `Age` to see if responses are cached
> - Add extensions or delimiters to dynamic paths and check if sensitive content is cached
> - Timing differences may indicate cached vs dynamic responses
- Burp Scanner’s Web Cache Deception checks

---

## 🛡 Mitigation
> - Ensure dynamic content is never cached (set correct headers: `Cache-Control: no-store, private`)
> - Segregate static and dynamic content under separate domains/paths
> - Validate and normalize URL paths consistently across origin and cache
