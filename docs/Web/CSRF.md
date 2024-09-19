---
layout: default
title: CSRF
nav_order: 3
has_children: false
parent: Web
---


## Summary

Cross-Site Request Forgery (CSRF) is a web security vulnerability that forces an authenticated user to perform unwanted actions on a web application in which they are authenticated. By tricking the user into making requests, an attacker can carry out actions like changing account details or making transactions, without the user's knowledge or intent.


## Impact

Cross-Site Request Forgery (CSRF) attacks can lead to severe consequences, such as:

- **Unauthorized Actions:** Attackers can perform actions on behalf of authenticated users without their knowledge.
- **Account Takeover:** Attackers can change user settings, transfer funds, or modify account details.
- **Data Loss:** Sensitive user information could be modified or deleted.
- **Privilege Escalation:** In some cases, attackers could escalate privileges within the application.
- **Service Disruption:** Critical services or accounts may be impacted by unauthorized actions.


## Severity (CVSS)

Severity based on CVSS:

- **Base Score:** Typically ranges between 6.0 (Medium) to 8.8 (High) depending on the potential impact and context.
- **Attack Vector:** Network
- **Attack Complexity:** Low
- **Privileges Required:** None
- **User Interaction:** Required (victim must interact with the malicious request, e.g., by clicking a link)


## How it is Exploited

Victim Authentication: The user must be logged into the target web application.
Malicious Request: The attacker tricks the victim into visiting a malicious site or clicking a crafted link (via email, social engineering, etc.).
Silent Action: The malicious site sends an HTTP request to the legitimate web application on behalf of the user, leveraging their active session. For example:

```javascript
<img src="https://victim.com/change-email?email=hacker@evil.com" />
```
    Unintended Action: The legitimate application, assuming the request is coming from the authenticated user, executes the action.

## Why it is Vulnerable

CSRF vulnerabilities arise because web applications rely on cookies for authentication. Even if a user is unaware, their browser will automatically include these cookies in every request to the application. If the application does not verify the origin or intent of requests, it blindly executes them, allowing attackers to exploit the session of authenticated users.

## Remediation

To protect against CSRF:

Anti-CSRF Tokens: Include unique, random tokens in forms or requests. The server should validate this token before processing the request.

```javascript
<input type="hidden" name="csrf_token" value="randomlyGeneratedToken">
```

SameSite Cookies: Set the SameSite attribute on cookies to restrict cross-site requests.

```javascript
Set-Cookie: sessionId=abc123; SameSite=Strict;
```
Double Submit Cookie: Use a CSRF token in both the cookie and request header, comparing the two on the server.
Referer Validation: Ensure the Referer or Origin header matches the legitimate domain before processing requests.
Limit the use of GET for State-Changing Operations: Use POST or other methods for actions that change application state.


## Content References

- OWASP: Cross-Site Request Forgery (CSRF)
- MDN Web Docs: Cross-Site Request Forgery
- CSRF Prevention in Web Applications