# File Upload Vulnerabilities  

## Metadata  
- **OWASP Category (2021):** A05 Security Misconfigurations  
- **PortSwigger Link:** [File uploads | Web Security Academy ](https://portswigger.net/web-security/file-upload) 

---

## 💡 Concept  
- **What is it?**  
> When a web application improperly validates or does not restrict files uploaded by users.  

- **Impact:**  
> - **Confidentiality:** Attackers may upload and serve malware to extract sensitive data or gain unauthorized ‘read’ access.  
> - **Integrity:** Malicious uploads can overwrite or replace application files, altering site behavior.  
> - **Availability:** DoS through large/malicious files can disrupt application availability.  

---

## ⚙️ Exploitation Notes  
- **Where to test:**  
> - File upload endpoints (`/upload`, profile pictures, document upload features).  
> - Static file storage directories.  
> - MIME-type headers and file extensions ( `Content-Type:`, `.php`, `.jsp`, `.asp`, etc.).  
> - Handling of compressed archives, image metadata, or polyglot files.  

- **Payloads / Tricks used:**  
> - Web shells: Uploading a `.php` file containing `<?php echo system($_GET["cmd"]); ?>`.  
> - Bypassing extension filters: Double extensions (`file.php.jpg`), case variants (`file.PHP`), null byte injection (`file.php%00.png`).  
> - MIME-type mismatches: Sending `Content-Type: image/png` with an executable payload.  
> - Overwriting configs: Uploading `.htaccess` to allow overriding of file types.  
> - Uploading non-executable malware or scripts: For phishing or client-side exploitation.  

---

## 🔍 Detection  
> - Intercept file uploads in Burp Proxy + modify extensions, MIME type, and metadata.  
> - Upload accessible files and check if they are accessible via public URL.  
> - Test double extensions, polyglot, oversized files.  
> - Look for error messages leaking server handling (e.g., `Unsupported Media Type`).  

---

## 🛡️ Mitigation  
> - Only allow uploads of specific file types (with strict server-side MIME & magic byte checks).  
> - Scan uploaded files with AV tools to prevent direct execution.  
> - Remove uploaded executable permissions.  
> - Strip or sanitize metadata and dangerous characters.  
> - Use allowlists instead of blacklists for extensions.  

