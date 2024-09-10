---
layout: default
title: XSS - Reflected
parent: XSS
grand_parent: Web
---


# Reflected XSS (Cross-Site Scripting)

 Vulnerability Reporting **[Template](https://cybergrimoire.github.io/docs/Templates/Web%20Templates/XSS_Reflected/)**



## Summary
Reflected XSS, often called non-persistent XSS, happens when a website echoes back information submitted by a user without adequately cleaning it up or escaping harmful elements. This vulnerability can be exploited by an attacker who crafts a special URL or form that includes malicious JavaScript code. When another user clicks on this link or submits the form, the embedded JavaScript runs within their browser.

This occurs because the web server uses the user's input directly in its response. For example, if you search for a term on a website, and the website immediately shows "Results for [your search term]", without checking if the input contains harmful scripts, an attacker could use this opportunity to inject a script instead of a simple search term. If the script is embedded in a URL and someone else clicks on it, the script will execute in their browser, leading to potential harm such as stealing cookies, capturing keyboard input, or other malicious activities.

The key to preventing this type of attack is for websites to sanitize any data received from users, ensuring that any potentially dangerous scripts are neutralized before they can cause harm.

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

##  How?
- **Detection:** 
    - Look for input fields, parameters, or URLs that reflect user input in the response.
- **Exploitation:**
  - **Crafting the Payload:** 
    - Inject a payload such as `<script>alert('XSS')</script>` into vulnerable parameters.
  - **Delivering the Attack:**
    - Social engineering techniques are often used to trick victims into clicking on a malicious link.
  - **Testing and Validation:**
    - If the script executes within the victim's browser without being sanitized, the vulnerability is confirmed.


Upon finding a reflection of user input within the web application, there is potential for reflected XSS. Reflection meaning that the user input is getting sent (reflected) back to the user's browser without escaping/encoding special characters such as `<>`
![](/assets/images/Web/XSS/XSS_Reflected_1.png)

After confirming the user input reflection, we can try and execute JavaScript. We caan use a simple payload like **alert('XSS')**
![](/assets/images/Web/XSS/XSS_Reflected_2.png)

And we have an **alert** pop-up show on screen, confirming the execution of JavaScript. This JavaScript will execute in the browser. When the browser loads the page, and the payload we sent, it parses it as legitimate code, and executes it.
![](/assets/images/Web/XSS/XSS_Reflected_3.png)

We can now try a more interesting payload, and get sensitive infomation from the victim, as an example we are going to use **alert(document.cookie)**
![](/assets/images/Web/XSS/XSS_Reflected_4.png)

Which gives us the cookies stored in the client/victim browser, cookies from the web application we are exploiting, within the pop-up alert box.
![](/assets/images/Web/XSS/XSS_Reflected_5.png)

If the user input parameter comes in the URL, we can send the URL with the JavaScript payloaad to the victim and it will execute the payload on the victim's browser.
![](/assets/images/Web/XSS/XSS_Reflected_6.png)

## Why?

The vulnerability arises because the application: 
- Does not adequately sanitize user-supplied input, allowing scripts to be included.
- Directly reflects user input in HTTP responses.
- Fails to encode or escape outputs when generating output in HTML, making it susceptible to script injection.

An example of such vulnerability in code:
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Reflected XSS Demo</title>
</head>
<body>
    <h1>Search</h1>
    <form action="" method="GET">
        <label for="query">Enter your search term:</label>
        <input type="text" id="query" name="query">
        <input type="submit" value="Search">
    </form>

    <p>You searched for: </p>
    <div id="results">
        <!-- This is where the reflected XSS vulnerability occurs -->
        <script>
            const urlParams = new URLSearchParams(window.location.search);
            const query = urlParams.get('query');
            if (query) {
                document.write(query);  // Use document.write to directly write user input
            }
        </script>
    </div>
</body>
</html>
<!-- Within HTML so you can see how it works locally, save the code and run it on your browser-->
```

If `query = urlParams.get('query');` is inserted without sanitization, it's vulnerable to XSS.
The simplest payload you can try and check for XSS is:
```javascript
<script>alert('XSS Vulnerability!');</script>
```

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
- [DVWA - DAMN VULNERABLE WEB APPLICATION](https://github.com/digininja/DVWA)
- [OWASP XSS Prevention CheatSheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

