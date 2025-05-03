# **Penetration Testing Report**

## **Introduction**

### **Purpose of the Report**
This report summarizes the penetration testing performed on the user registration module of the Booking System (Phase 1). 
The objective was to uncover potential security vulnerabilities and assess compliance with security best practices, with a specific focus on input validation and data encryption mechanisms.

### **Testing Schedule and Environment**
- **Testing Date:** 25-04-2025
- **New Testing Date:** 05-02-2025

- **Environment:** Localhost (`http://localhost:8000/register`)
- **Testing Methodology:**  Both automated scanning using ZAP and manual analysis.
- **Testing User:** Created a test account (`joker/joker123`) for testing.

### **Scope of Testing**
- **Tested Component:** User Registration Page (only)
- **Excluded:** Login, Resource Booking, Administrator Functions (not implemented in Phase 1)
- **Focus Areas:**
  - Input Validation (SQL Injection)
  - Data Encryption & Storage Security

### **Methods and Tools Used for Testing**
- **ZAP** – Automated scanning & active attack testing.
- **Kali Linux** – Environment for penetration testing.
- **Chromium Developer Tools** – Inspecting HTTP requests.
- **PostgreSQL Queries** – Analyzing database security.

---

## **. Summary**

### **Key Findings and Recommendations**
1. **SQL Injection in Registration Form (Critical)**  
   - The registration form is vulnerable to **SQL Injection**, allowing attackers to manipulate database queries.  
   - **Fix:** Use **prepared statements** and **input sanitization**.

2. **Passwords Stored in Plaintext (Critical)**  
   - The database stores **plaintext passwords**, which is a **major security risk** and **GDPR non-compliant**.  
   - **Fix:** Implement **bcrypt** or **Argon2** hashing for password storage.

### **General Assessment**
The system contains serious security vulnerabilities, such as SQL Injection and unencrypted password storage.
These issues pose a high risk of data breaches, unauthorized access, and non-compliance with security standards, and must be addressed immediately.
---

## **3. Findings and Categorization**

### ** 1. SQL Injection in Registration Form (High)**
**Risk Level:**  **High**  
**Description:**  
The registration form lacks proper input validation, making it vulnerable to SQL Injection attacks.

This allows attackers to alter SQL queries, potentially exposing, modifying, or deleting sensitive data from the database.

**Evidence:**  
SQL Injection payload tested:  
```sql
username=admin' OR '1'='1' -- &password=test123
```

The output of the query was as follows:

| username | password  |
|----------|-----------|
| joker    | joker123  |
| admin    | admin123  |

The passwords are stored in plaintext, making the system susceptible to unauthorized access.

### Recommendations:
Use prepared statements (parameterized queries) to safely handle user input and prevent SQL injection.

Sanitize and validate all user input to ensure it does not contain SQL control characters or malicious content.

### ** 2. Passwords Stored in Plaintext (High)**
**Risk Level:**  **High**  
**Description:**  
- The database **stores passwords in plaintext**, which is **a major eccurity risk**.
- If an attacker gains access to the database, they can see all user passwords.

**Evidence:**  
Query to database:  
```sql
SELECT username, password FROM xyz123_users;
```

Returned:

| username | password  |
|----------|-----------|
| joker    | joker123  |
| admin    | admin123  |

The passwords are stored in plaintext, making the system susceptible to unauthorized access.

### Recommendations:
- Hash passwords using bcrypt or Argon2.
- Never store raw passwords in the database.

### ** 3. Content Security Policy Header Not Set (Medium)**  
**Risk Level:**  **Medium**  
**Description:**  
The application lacks a Content Security Policy (CSP) header.

CSP (Content Security Policy) is an important security feature that helps protect against Cross-Site Scripting (XSS) and data injection attacks by allowing only content from trusted sources to be loaded and executed by the browser.

**Evidence:**  
When reviewing the HTTP response headers for the /register page, it was found that the Content-Security-Policy (CSP) header is not set, exposing the application to XSS and data injection risks.
- **URL:** `http://localhost:8000/register`
- **Method:** `GET`
- **Response Headers:**  
    ```
    content-encoding: br
    content-length: 357
    content-type: text/html; charset=UTF-8
    date: Thu, 20 Feb 2025 08:23:48 GMT
    vary: Accept-Encoding
    ```

### **Recommendations:**
-  Add a Content-Security-Policy header to all HTTP responses.

-  Define a strict policy to allow content only from trusted sources.

## ** Refs**

### **ZAP report in the Booking system - Phase 1 folder**

### **Commands during testing (manual SQL queries)**
