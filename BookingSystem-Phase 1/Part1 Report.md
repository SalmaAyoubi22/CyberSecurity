# ZAP by Checkmarx Scanning Report

ZAP by [Checkmarx](https://checkmarx.com/).


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 1 |
| Medium | 3|
| Low | 2 |
| Informational | 1 |




## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| SQL Injection | High | 1 |
| Content Security Policy (CSP) Header Not Set | Medium | 1 |
| Format String Error | Medium | 1 |
| Missing Anti-clickjacking Header | Medium | 1 |
| X-Content-Type-Options Header Missing | Low | 2 |





## Alert Detail
### [ SQL Injection ](https://www.zaproxy.org/docs/alerts/40018/)



##### High (Medium)

### Description

SQL injection may be possible.

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `joker AND 1=1 -- `
  * Evidence: ``
  * Details: Boolean-based SQL injection confirmed. Parameter manipulation with AND 1=1 returned original data, while AND 1=2 restricted it, indicating successful injection.
    The vulnerability was detected by successfully restricting the data input returned, by manipulating the parameter.`



Instances: 1

### Solution

Never trust client-side input—validate and type-check all data on the server side.
Use parameterized queries (e.g., PreparedStatement, stored procedures) and avoid string concatenation in SQL.
Enforce least privilege by using minimally privileged database accounts and restricting access tightly.
Do not create dynamic SQL queries using simple string concatenation.
Escape all data received from the client.
If database Stored Procedures can be used, use them.

### Reference


* [ https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)


#### CWE Id: [ 89 ](https://cwe.mitre.org/data/definitions/89.html)


#### WASC Id: 19

#### Source ID: 1
### [ Content Security Policy (CSP) Header Not Set ](https://www.zaproxy.org/docs/alerts/10038/)



##### Medium (High)

### Description
Content Security Policy (CSP) is an added security layer that helps prevent attacks such as Cross-Site Scripting (XSS) and data injection, which can lead to data theft, site defacement, or malware distribution. 
CSP uses HTTP headers to specify trusted content sources, including JavaScript, CSS, HTML frames, fonts, images, and embedded objects like Java applets, ActiveX, and media files, limiting potential risks from malicious content.



* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: 1

### Solution

Ensure that your web server, application server, load balancer, etc. is configured to set the Content-Security-Policy header.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/Security/CSP/Introducing_Content_Security_Policy ](https://developer.mozilla.org/en-US/docs/Web/Security/CSP/Introducing_Content_Security_Policy)
* [ https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)
* [ https://www.w3.org/TR/CSP/ ](https://www.w3.org/TR/CSP/)
* [ https://w3c.github.io/webappsec-csp/ ](https://w3c.github.io/webappsec-csp/)
* [ https://web.dev/articles/csp ](https://web.dev/articles/csp)
* [ https://caniuse.com/#feat=contentsecuritypolicy ](https://caniuse.com/#feat=contentsecuritypolicy)
* [ https://content-security-policy.com/ ](https://content-security-policy.com/)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3

### [ Format String Error ](https://www.zaproxy.org/docs/alerts/30002/)



##### Medium (Medium)

### Description

A Format String vulnerability happens when user-provided input is interpreted as a command by the application, allowing potential misuse or exploitation.

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  * Evidence: ``
  * Other Info: `Potential Format String Error. The script closed the connection on a /%s.`

Instances: 1

### Solution

Reformulate the background program to properly handle and remove harmful character strings. This will necessitate recompiling the background executable to ensure security.

### Reference


* [ https://owasp.org/www-community/attacks/Format_string_attack ](https://owasp.org/www-community/attacks/Format_string_attack)


#### CWE Id: [ 134 ](https://cwe.mitre.org/data/definitions/134.html)


#### WASC Id: 6

#### Source ID: 1

### [ Missing Anti-clickjacking Header ](https://www.zaproxy.org/docs/alerts/10020/)


##### Medium (Medium)

### Description

The response is vulnerable to ClickJacking attacks. It should include either a Content-Security-Policy header with the 'frame-ancestors' directive or the X-Frame-Options header to mitigate this risk.

* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: 1

### Solution

New web browsers support both the Content-Security-Policy and X-Frame-Options HTTP headers. 
Ensure that one of these headers is set on all pages served by your site/app.
If the page is intended to be framed only by other pages on your server (e.g., within a FRAMESET), use the SAMEORIGIN directive. 
If the page should never be framed, use DENY. Alternatively, you can implement the "frame-ancestors" directive in the Content-Security-Policy header.
### Reference

* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)


#### CWE Id: [ 1021 ](https://cwe.mitre.org/data/definitions/1021.html)


#### WASC Id: 15

#### Source ID: 3

### [ X-Content-Type-Options Header Missing ](https://www.zaproxy.org/docs/alerts/10021/)



##### Low (Medium)

### Description

The X-Content-Type-Options header was not set to 'nosniff', which allows older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body. 
This could lead to the body being interpreted and displayed as a content type different from the declared type. 
However, current and legacy versions of Firefox (as of early 2014) will respect the declared content type and avoid MIME-sniffing.

* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:8000/static/styles.css
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`
* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold this scan rule will not alert on client or server error responses.`

Instances: 3

### Solution

Ensure the application or web server correctly sets the Content-Type header and includes the X-Content-Type-Options: nosniff header for all web pages. 
If possible, encourage the use of modern, standards-compliant browsers that either do not perform MIME-sniffing or can be instructed by server headers to avoid it.


### Reference


* [ https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85) ](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85))
* [ https://owasp.org/www-community/Security_Headers ](https://owasp.org/www-community/Security_Headers)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3
