# OWASP Juice Shop Labs

This repository documents hands-on security testing performed against the **OWASP Juice Shop** application using **Burp Suite Community Edition**.

The goal of this project is to demonstrate practical understanding of common web vulnerabilities, request manipulation, and insecure API behavior.

---

## 🛠 Tools Used
- OWASP Juice Shop (Local deployment)
- Burp Suite Community Edition
- Google Chrome
- Node.js (for Juice Shop setup)

---

## 🔐 Lab 1: Authentication & Error Handling

### Objective
Observe how the application handles invalid login attempts and malformed requests.

### Steps Performed
1. Intercepted login requests using Burp Proxy
2. Sent requests to Burp Repeater
3. Modified request body to introduce unexpected data types
4. Observed server behavior and responses

### Result
- Application returned **500 Internal Server Error**
- Full stack trace was exposed in the response
- Indicates **improper error handling** and **information disclosure**

### OWASP Top 10 Mapping
- A03: Injection
- A05: Security Misconfiguration

---

## 🛒 Lab 2: Insecure Direct Object Reference (IDOR) – Basket Access

### Objective
Test whether basket IDs are properly authorized per user.

### Steps Performed
1. Created a new user account
2. Logged in and added items to basket
3. Intercepted request:
GET /rest/basket/{id}
4. Modified basket ID value in Burp Repeater

### Result
- Server returned **200 OK** for another basket ID
- Data from a different user’s basket was accessible

### Impact
- Unauthorized access to another user’s data
- Confirms **IDOR vulnerability**

### OWASP Top 10 Mapping
- A01: Broken Access Control

---

## 📌 Summary

This project demonstrates:
- Manual request tampering
- API authorization weaknesses
- Real-world vulnerability patterns
- Proper use of Burp Suite for testing

---

## 🚀 Next Steps
- Add screenshots for each lab
- Expand to additional Juice Shop challenges
- Include remediation recommendations
