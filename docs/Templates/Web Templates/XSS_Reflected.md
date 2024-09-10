---
layout: default
title: XSS - Reflected
parent: XSS
grand_parent: Templates
---


<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vulnerability Report Template</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            border: 1px solid #a09aa3; /* Default light gray border */
            background-color: #a09aa3;
            box-sizing: border-box;
        }
        th, td {
            border: 1px solid #a0a0a0; /* Default light gray border */
            padding: 8px;
            text-align: left;
            box-sizing: border-box;
            column-span: 6;
            text-align: justify;
        }
        th {
            background-color: #f2f2f2;
        }
        table b, table strong {
            color: #7253ed;
        }
    </style>
</head>
<body>



<h1>Vulnerability Report Template</h1>
<table id="VulnTable">
    <tr>
        <td colspan="6" style="border: none; font-weight: bold; text-align: center;">
            Reflected Cross-Site Scripting
        </td>
    </tr>
    <tr>
        <td colspan="6"><b>Summary:</b></td>
    </tr>
    <tr>
        <td colspan="6">
            Reflected Cross-Site Scripting (XSS) is a vulnerability where attackers inject malicious scripts via user inputs that are immediately reflected in the website's response. This allows the attacker to steal data, hijack sessions, or trick users. The issue arises from improper validation of user inputs and can be prevented through proper input sanitization and output encoding.
        </td>
    </tr>
    <tr>
        <td><b>Criticity:</b> High/Medium</td>
        <td><b>Endpoints:</b>
            <ul>
                <li>https://www.vulnerable_endpoint.com</li>
                <li>10.10.10.1/24</li>
                <li>/specific_page_endpoint</li>
            </ul>
        </td>
        <td><b>CVE:</b> N/A</td>
    </tr>
    <tr>
        <td colspan="6"><b>Description:</b></td>
    </tr>
    <tr>
        <td colspan="6">
            Reflected XSS occurs when user input, such as query parameters or form data, is reflected in the server's response without proper sanitization or encoding. In [Affected Company], endpoints like [Vulnerable Endpoint 1] and [Vulnerable Endpoint 2] allow attackers to inject malicious scripts, which are executed in the victim’s browser. This can lead to session hijacking, data theft, or unauthorized actions. 
        </td>
    </tr>
    <tr>
        <td colspan="6"><b>Remediation:</b></td>
    </tr>
    <tr>
        <td colspan="6">
            <ul>
                <li>Implement X-XSS-Protection Header</li>
                <li>Use Security-Focused Libraries</li>
                <li>Input Validation</li>
                <li>Output Encoding</li>
                <li>Implement Content Security Policy(CSP)</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td colspan="6"><b>Resources:</b></td>
    </tr>
    <tr>
        <td colspan="6">
            <ul>
                <li>https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html</li>
                <li>https://portswigger.net/web-security/cross-site-scripting/reflected</li>
            </ul>      
        </td>
    </tr>
</table>

*Adapt the table values to your test and context*

</body>
</html>





