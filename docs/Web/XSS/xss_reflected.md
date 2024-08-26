---
layout: default
title: XSS - Reflected
parent: XSS
grand_parent: Web
---


# Reflected XSS (Cross-Site Scripting)





## Summary
Reflected XSS, also known as non-persistent XSS, occurs when user-supplied data is immediately reflected back to the user by the web server without being properly sanitized or encoded. This type of XSS attack is typically delivered via a URL or a form submission, and the malicious script is executed within the browser of the victim who clicks on the crafted link.

## Impact
Reflected XSS attacks can have significant consequences depending on the context in which they are exploited:

  - **Data Theft:** Attackers can steal cookies, session tokens, or other sensitive data.
  - **Account Takeover:** By hijacking sessions, attackers can gain unauthorized access to user accounts.
  - **Defacement:** Malicious scripts can modify the appearance of a website.
  - **Phishing:** Attackers can redirect victims to fake login pages or other malicious sites.
  
## Severity (CVSS)
  - **Base Score:** Typically between 4.0 (Medium) to 7.5 (High), depending on the context and impact.
  - **Attack Vector:** Network
  - **Attack Complexity:** Low
  - **Privileges Required:** None
  - **User Interaction:** Required

## Detection - Exploitation
- **Detection:**
  - **Manual Testing:** 
    - Look for input fields, parameters, or URLs that reflect user input in the response.
    - Use tools like Burp Suite to analyze HTTP requests and responses.
  - **Automated Tools:**
    - **OWASP ZAP** and **Burp Suite** offer automated XSS detection.
    - Browser-based XSS auditors, such as the ones built into Chrome or Firefox Developer Tools, can help identify reflected XSS vulnerabilities.
- **Exploitation:**
  - **Crafting the Payload:** 
    - Inject a payload such as `<script>alert('XSS')</script>` into vulnerable parameters.
  - **Delivering the Attack:**
    - Social engineering techniques are often used to trick victims into clicking on a malicious link.
  - **Testing and Validation:**
    - If the script executes within the victim's browser without being sanitized, the vulnerability is confirmed.

![](/assets/images/Web/XSS/XSS_Reflected_1.png)

![](/assets/images/Web/XSS/XSS_Reflected_2.png)

![](/assets/images/Web/XSS/XSS_Reflected_3.png)

![](/assets/images/Web/XSS/XSS_Reflected_4.png)

![](/assets/images/Web/XSS/XSS_Reflected_5.png)

## Remediation
- **Input Validation:**
  - Ensure that all user inputs are validated for allowed characters and data types.
- **Output Encoding:**
  - Encode user-supplied data before displaying it in the browser. Use appropriate context-specific encoding (HTML, JavaScript, URL encoding).
- **Content Security Policy (CSP):**
  - Implement a strict CSP to mitigate the impact of XSS by restricting the sources from which scripts can be executed.
- **Security Frameworks and Libraries:**
  - Use security-focused libraries and frameworks that automatically handle input sanitization and output encoding.
- **Regular Security Audits:**
  - Perform regular security audits and penetration tests to identify and fix XSS vulnerabilities.

## References
- [OWASP Cross-Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/)
- [PortSwigger Web Security Academy: Reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected)
- [Mozilla Developer Network (MDN): XSS Prevention](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)
