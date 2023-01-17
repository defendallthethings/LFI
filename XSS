# HARDERING
# Front-End
```
function validateEmail(email) {
    const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test($("#login input[name=email]").val());
}
```
# Imput Sanitization
https://github.com/cure53/DOMPurify
```
<script type="text/javascript" src="dist/purify.min.js"></script>
let clean = DOMPurify.sanitize( dirty );
```

# Direct Input

Finally, we should always ensure that we never use user input directly within certain HTML tags, like:
1. JavaScript code <script></script>
2. CSS Style Code <style></style>
3. Tag/Attribute Fields <div name='INPUT'></div>
4. HTML Comments <!-- -->
If user input goes into any of the above examples, it can inject  malicious JavaScript code, which may lead to an XSS vulnerability. In  addition to this, we should avoid using JavaScript functions that allow  changing raw text of HTML fields, like:
- DOM.innerHTML
- DOM.outerHTML
- document.write()
- document.writeln()
- document.domain
An the following jQuery functions:
- html()
- parseHTML()
- add()
- append()
- prepend()
- after()
- insertAfter()
- before()
- insertBefore()
- replaceAll()
- replaceWith()
As these functions write raw text to the HTML code, if any user input  goes into them, it may include malicious JavaScript code, which leads  to an XSS vulnerability.

# Back-End
```
if (filter_var($_GET['email'], FILTER_VALIDATE_EMAIL)) {
    // do task
} else {
    // reject input - do not display it
}

```
For example, for a PHP back-end, we can use the addslashes function to sanitize user input by escaping special characters with a backslash:
Code: php
```
addslashes($_GET['email'])
```
For a NodeJS back-end, we can also use the DOMPurify library as we did with the front-end, as follows:
Code: javascript
```
import DOMPurify from 'dompurify';
var clean = DOMPurify.sanitize(dirty);

```

# Output HTML Encoding

Another important aspect to pay attention to in the back-end is Output Encoding.  This means that we have to encode any special characters into their  HTML codes, which is helpful if we need to display the entire user input  without introducing an XSS vulnerability. For a PHP back-end, we can  use the htmlspecialchars or the htmlentities functions, which would encode certain special characters into their HTML codes (e.g. < into &lt), so the browser will display them correctly, but they will not cause any injection of any sort:
Code: php
```
htmlentities($_GET['email']);

```
For a NodeJS back-end, we can use any library that does HTML encoding, like html-entities, as follows:
Code: javascript
```
import encode from 'html-entities';
encode('<'); // -> '&lt;'

```
Once we ensure that all user input is validated, sanitized, and  encoded on output, we should significantly reduce the risk of having XSS  vulnerabilities.

Server Configuration

In addition to the above, there are certain back-end web server configurations that may help in preventing XSS attacks, such as:
- Using HTTPS across the entire domain
- Using XSS prevention headers, like X-XSS-Protection.
- Using the appropriate Content-Type for the page, like X-Content-Type-Options=nosniff.
- Using Content-Security-Policy options, like script-src 'self', which only allows locally hosted scripts.
- Using the HttpOnly and Secure cookie flags to prevent JavaScript from reading cookies and only transport them over HTTPS.
In addition to the above, having a good Web Application Firewall (WAF)  can significantly reduce the chances of XSS exploitation, as it will  automatically detect any type of injection going through HTTP requests  and will automatically reject such requests.
In the end, we must do our best to secure our web applications  against XSS vulnerabilities using such XSS prevention techniques. Even  after all of this is done, we should practice all of the skills we  learned in this module and attempt to identify and exploit XSS  vulnerabilities in any potential input fields, as secure coding and  secure configurations may still leave gaps and vulnerabilities that can  be exploited. If we practice defending the website using both offensive and defensive techniques, we should reach a reliable level of security against XSS vulnerabilities.
