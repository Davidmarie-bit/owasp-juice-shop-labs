# OWASP Juice Shop Labs

This repository documents hands-on security testing performed against the **OWASP Juice Shop** application using **Burp Suite Community Edition**.

The goal of this project is to demonstrate practical understanding of common web vulnerabilities, request manipulation, and insecure API behavior.

---

## 🛠 Tools Used
- OWASP Juice Shop (Local deployment)
- Burp Suite Community Edition
- Google Chrome
- Node.js (for Juice Shop setup)


## 🔐 Lab 1: Authentication & Error Handling

### 🎯 Objective
Assess how the application handles invalid authentication attempts and malformed login requests.

### 🧪 Steps Performed
1. Intercepted login requests using Burp Proxy  
2. Sent captured requests to Burp Repeater  
3. Modified request body to introduce unexpected data types  
4. Observed server responses and error handling behavior  

### ✅ Result
- Application returned **500 Internal Server Error**
- Full stack trace was exposed in the response
- Indicates **improper error handling** and **information disclosure**

### ⚠️ Impact
- Internal application details exposed to attackers
- Increases risk of further exploitation and attack chaining

### 🧭 OWASP Top 10 Mapping
- A03: Injection  
- A05: Security Misconfiguration  

### 🛠️ Remediation Recommendations
- Implement strict input validation and schema enforcement
- Replace verbose error messages with generic responses
- Disable stack trace exposure in production environments
- Apply centralized error handling and logging mechanisms

---

## 🛒 Lab 2: Insecure Direct Object Reference (IDOR) – Basket Access

> This lab demonstrates a **Broken Object Level Authorization (BOLA)** vulnerability through an IDOR exploit.

### 🎯 Objective
Verify whether basket resources are properly authorized on a per-user basis.

### 🧪 Steps Performed
1. Created a new user account  
2. Logged in and added items to the basket  
3. Intercepted the request:
GET /rest/basket/{id}

markdown
Copy code
4. Modified the basket ID parameter using Burp Repeater  

### ✅ Result
- Server returned **200 OK** for a basket ID belonging to another user
- Data from a different user’s basket was accessible

### ⚠️ Impact
- Unauthorized access to another user’s data
- Confirms **IDOR vulnerability**
- Demonstrates **Broken Object Level Authorization (BOLA)**

### 🧭 OWASP Top 10 Mapping
- A01: Broken Access Control  
- OWASP API Security Top 10: BOLA  

### 🛠️ Remediation Recommendations
- Enforce object-level authorization checks on every request
- Validate ownership of resources server-side
- Avoid trusting client-supplied object identifiers
- Bind access decisions to authenticated user context
- Log and alert on unauthorized access attempts

---

## 📌 Summary

This project demonstrates:
- Manual request tampering using Burp Suite
- Authentication and authorization weaknesses
- Common API security flaws mapped to OWASP standards
- Real-world vulnerability testing techniques

---

## 🔜 Planned Additional Juice Shop Challenges

The following challenges will be explored in future updates:

- SQL Injection via search and login endpoints
- Cross-Site Scripting (XSS) in user input fields
- JWT token manipulation and privilege escalation
- Missing rate limiting on authentication endpoints
- Password policy weaknesses and account enumeration
- Business logic flaws in order and payment workflows

