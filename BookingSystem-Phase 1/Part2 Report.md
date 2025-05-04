 # ZAP by Checkmarx Scanning Report

ZAP by [Checkmarx](https://checkmarx.com/).


## Summary of Alerts

| Risk Level | Number of Alerts |
| --- | --- |
| High | 2 |
| Medium | 3 |
| Low | 2 |
| Informational | 1 |


## Alerts

| Name | Risk Level | Number of Instances |
| --- | --- | --- |
| SQL Injection | High | 4 |
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
  * Attack: `  AND 1=1 -- `
  * Evidence: ``
  * Other Info: The page was successfully manipulated using Boolean conditions like [ AND 1=1 -- ] and [ AND 1=2 -- ]. The parameter value was reflected in the HTML response without being sanitized.
    The vulnerability was confirmed by altering the parameter to control the data returned, demonstrating the application's susceptibility to SQL injection.
* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `  OR 1=1 -- `
  * Evidence: ``
  * Other Info: The page output was manipulated using Boolean conditions such as [ AND 1=1 -- ] and [ OR 1=1 -- ]. The altered parameter remained in the HTML response without sanitization.
  The original data was not returned, but the vulnerability was confirmed by extracting additional data through parameter manipulation.

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: ` ' AND '1'='1' -- `
  * Evidence: ``
  * Other Info: The page output was successfully manipulated using Boolean conditions like [ ' AND '1'='1' -- ] and [ ' AND '1'='2' -- ]. The injected parameter remained visible in the HTML response.
    The vulnerability was confirmed by altering the parameter to restrict the originally returned data, demonstrating that SQL injection is possible.

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: ` ' OR '1'='1' -- `
  * Evidence: ``
  * Other Info: `The page results were successfully manipulated using the boolean conditions [ ' AND '1'='1' -- ] and [ ' OR '1'='1' -- ]
The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison.
Data for the original parameter was NOT returned.
The vulnerability was detected by successfully retrieving more data than originally returned, by manipulating the parameter.`

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `joke AND 1=1 -- `
  * Evidence: ``
  * Other Info: `The page results were successfully manipulated using the boolean conditions [joke AND 1=1 -- ] and [joke AND 1=2 -- ]
The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison.
Data was returned for the original parameter.
The vulnerability was detected by successfully restricting the data originally returned by manipulating the parameter.`

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `joke OR 1=1 -- `
  * Evidence: ``
  * Other Info: `The page results were successfully manipulated using the boolean conditions [joke AND 1=1 -- ] and [joke OR 1=1 -- ]
The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison.
Data for the original parameter was NOT returned.
The vulnerability was detected by successfully retrieving more data than originally returned, by manipulating the parameter.`

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `joke' AND '1'='1' -- `
  * Evidence: ``
  * Other Info: `The page results were successfully manipulated using the boolean conditions [joke' AND '1'='1' -- ] and [joke' AND '1'='2' -- ]
The parameter value being modified was NOT stripped from the HTML output for the purposes of the comparison.
Data was returned for the original parameter.
The vulnerability was detected by successfully restricting the data originally returned by manipulating the parameter.`

Instances: 7

### Solution

Do not trust client-side input, even if client-side validation exists.

Always validate and type-check all data on the server side.

Use parameterized queries:

In JDBC, use PreparedStatement or CallableStatement with parameters (?).

In ASP, use ADO Command Objects with strong type checking.

Prefer stored procedures when possible, but avoid string concatenation or dynamic execution like exec or exec immediate.

Never build dynamic SQL queries through simple string concatenation.

Sanitize and escape all data received from the client.

Apply an allow list (preferred) or a deny list to filter acceptable characters in user input.

Enforce the principle of least privilege:

Avoid using high-privilege database accounts like sa or db-owner.

Grant only the minimum necessary access to the application.

### Reference


* [ https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html ](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)


#### CWE Id: [ 89 ](https://cwe.mitre.org/data/definitions/89.html)


#### WASC Id: 19

#### Source ID: 1
### [ Content Security Policy (CSP) Header Not Set ](https://www.zaproxy.org/docs/alerts/10038/)



##### Medium (High)

### Description

Content Security Policy (CSP) is a security feature designed to identify and reduce specific types of attacks, such as Cross-Site Scripting (XSS) and data injection. These threats can lead to issues like data breaches, website defacement, or malware distribution. 
CSP works by using HTTP headers that let website administrators specify trusted sources for content that browsers are permitted to load, including JavaScript, CSS, frames, fonts, images, and embedded elements like Java applets, ActiveX, audio, and video.

* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: ``
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: 1

### Solution

Make sure your web server, application server, or load balancer is configured to include the Content-Security-Policy (CSP) header in responses. This helps enforce security rules for loading content and mitigates risks like XSS and data injection.

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

A Format String vulnerability arises when user-supplied input is incorrectly processed as a format directive by the application, potentially allowing execution of unintended commands or access to memory.

* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `username`
  * Attack: `ZAP%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s%n%s
`
  * Evidence: ``
  * Other Info: `Potential Format String Error. The script closed the connection on a /%s.`

Instances: 1

### Solution

Modify the background program to properly remove or sanitize invalid character strings, ensuring they cannot be misused. After making these changes, recompile the background executable to apply the updates.

### Reference


* [ https://owasp.org/www-community/attacks/Format_string_attack ](https://owasp.org/www-community/attacks/Format_string_attack)


#### CWE Id: [ 134 ](https://cwe.mitre.org/data/definitions/134.html)


#### WASC Id: 6

#### Source ID: 1
### [ Missing Anti-clickjacking Header ](https://www.zaproxy.org/docs/alerts/10020/)



##### Medium (Medium)

### Description

The response is vulnerable to 'ClickJacking' attacks as it does not implement adequate protection. 
To mitigate this risk, the response should include either a Content-Security-Policy (CSP) with the frame-ancestors directive or the X-Frame-Options header.

* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: `x-frame-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: ``

Instances: 1

### Solution

Modern web browsers support both Content-Security-Policy (CSP) and X-Frame-Options HTTP headers. Ensure that one of these headers is set on all web pages served by your site or application.

If the page is intended to be framed only by other pages on your server (part of a FRAMESET), use SAMEORIGIN.

If the page should never be framed, use DENY.

Alternatively, you can implement the frame-ancestors directive in CSP for more granular control.

### Reference


* [ https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)


#### CWE Id: [ 1021 ](https://cwe.mitre.org/data/definitions/1021.html)


#### WASC Id: 15

#### Source ID: 3

### [ X-Content-Type-Options Header Missing ](https://www.zaproxy.org/docs/alerts/10021/)



##### Low (Medium)

### Description

The X-Content-Type-Options header was not set to nosniff, which can allow older versions of Internet Explorer and Chrome to perform MIME-sniffing on the response body. 
This could cause the response body to be interpreted as a different content type than what was declared, potentially leading to security issues. On the other hand, modern versions of Firefox (as of early 2014) and other recent browsers rely on the declared content type and do not perform MIME-sniffing.

* URL: http://localhost:8000/register
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold, this scan rule will not alert on client or server error responses.`
* URL: http://localhost:8000/static/styles.css
  * Method: `GET`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold, this scan rule will not alert on client or server error responses.`
* URL: http://localhost:8000/register
  * Method: `POST`
  * Parameter: `x-content-type-options`
  * Attack: ``
  * Evidence: ``
  * Other Info: `This issue still applies to error type pages (401, 403, 500, etc.) as those pages are often still affected by injection issues, in which case there is still concern for browsers sniffing pages away from their actual content type.
At "High" threshold, this scan rule will not alert on client or server error responses.`

Instances: 3

### Solution

Ensure that the application or web server correctly sets the Content-Type header and includes the X-Content-Type-Options header with the value nosniff for all web pages. 
Additionally, encourage end users to use modern, standards-compliant browsers that do not perform MIME-sniffing, or configure the web application or server to prevent MIME-sniffing altogether.
### Reference


* [ https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85) ](https://learn.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/compatibility/gg622941(v=vs.85))
* [ https://owasp.org/www-community/Security_Headers ](https://owasp.org/www-community/Security_Headers)


#### CWE Id: [ 693 ](https://cwe.mitre.org/data/definitions/693.html)


#### WASC Id: 15

#### Source ID: 3
