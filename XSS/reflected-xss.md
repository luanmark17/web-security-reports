# Reflected Cross-Site Scripting (XSS)

## General Information

| **Field** | **Information** |
|---|---|
| Vulnerability | Reflected Cross-Site Scripting (XSS) |
| Category | Injection |
| Platform | PortSwigger Web Security Academy |
| Lab | Reflected XSS into HTML context with nothing encoded |
| Tools | Google Chrome and Chrome DevTools |
| Languages | HTML and JavaScript |
| Status | Solved |
| Difficulty | Apprentice |

## Description

A Reflected Cross-Site Scripting (XSS) vulnerability was identified in a search functionality.

The application directly reflected user-supplied input in the HTML response without proper output encoding.

The input was inserted inside an HTML `<h1>` element, allowing user-supplied HTML and JavaScript code to be interpreted by the browser.

## Testing Environment

- Platform: PortSwigger Web Security Academy.
- Browser: Google Chrome.
- Analysis tool: Chrome DevTools.
- Tested functionality: Website search feature.

## Identification Procedure

1. Access the lab provided by PortSwigger.
2. Locate the search functionality.
3. Enter a test string into the search field.
4. Inspect the HTML using the DevTools Elements tab.
5. Locate the reflected input in the HTML structure.
6. Identify that the input was inserted into an HTML context inside an `<h1>` element.

## Proof of Concept (PoC)

Payload used:

```html
<script>alert(1)</script>
```

After submitting the payload through the search field, the application reflected the content in the HTML response.

The browser interpreted the `<script>` tag and executed the JavaScript, displaying an alert dialog containing the value `1`.

**Result:** JavaScript execution successfully confirmed.

## Potential Impact

Depending on the application's context, an XSS vulnerability may allow:

- JavaScript execution in other users' browsers.
- Manipulation of page content.
- Actions performed on behalf of authenticated users, depending on their permissions and existing security protections.
- Access to information available within the application's context, when not protected by security mechanisms.

The execution of `alert(1)` confirms JavaScript execution but does not independently demonstrate account compromise or access to sensitive information.

## Remediation Recommendations

- Implement context-appropriate output encoding for HTML.
- Avoid inserting untrusted data directly into HTML.
- Use safe APIs for DOM manipulation.
- Implement a Content Security Policy (CSP) as an additional layer of protection.
- Properly validate and handle user-supplied input.

## Evidence

### 1. HTML Reflection

[View HTML reflection](01-html-reflection.png)

### 2. JavaScript Execution

[View alert execution](02-xss-poc.png)

### 3. Lab Completion

[View lab completion evidence](03-lab-solved.png)

## References

- [PortSwigger - Cross-Site Scripting](https://portswigger.net/web-security/cross-site-scripting)
- [OWASP - Cross-Site Scripting](https://owasp.org/www-community/attacks/xss/)

---

**Disclaimer:** This report documents an educational exercise performed in the controlled PortSwigger Web Security Academy environment. It does not represent a vulnerability discovered in a production system.
