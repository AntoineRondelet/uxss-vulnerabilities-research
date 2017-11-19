# UXSS recorded vulnerabilities

This folder contains some of the UXSS patterns (see ./patterns) that have been used against Browsers in the past. We record some of them in this repository to try to extract valuable information from the study of these previous attacks. Hopefully, we might be able to draft our own attack based on this record.

## UXSS Studied:

### Chrome:
- CVE-2017-5069: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
- CVE-2017-5045: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
- CVE-2017-5020: https://bugs.chromium.org/p/chromium/issues/detail?id=668653&desc=2
- CVE-2017-5018: https://bugs.chromium.org/p/chromium/issues/detail?id=668665
- CVE-2017-5010: https://bugs.chromium.org/p/chromium/issues/detail?id=663476
- CVE-2017-5008: https://bugs.chromium.org/p/chromium/issues/detail?id=668552 -- Vulnerability in WebKit/Blink
- CVE-2017-5007: https://bugs.chromium.org/p/chromium/issues/detail?id=671102 -- Vulnerability in WebKit/Blink
- CVE-2017-5006: https://bugs.chromium.org/p/chromium/issues/detail?id=673170 -- Vulnerability in WebKit/Blink
- CVE-2016-5226: https://bugs.chromium.org/p/chromium/issues/detail?id=639750 -- XSS using Dropjacking -- Because of JS, selected character is replaced with javascript:alert(1) therefore XSS occurs. This only happens in Chrome. See below video for better understanding. -- The idea here is to drag and drop a text from one tab to another and replace the actual text by some malicious javascript that will be executed in the context of the victim's domain
- CVE-2016-5208: https://bugs.chromium.org/p/chromium/issues/detail?id=658535 -- Vulnerability in WebKit/Blink
- CVE-2016-5207: https://bugs.chromium.org/p/chromium/issues/detail?id=655904 -- Vulnerability in WebKit/Blink
- CVE-2016-5204: https://bugs.chromium.org/p/chromium/issues/detail?id=630870 -- Vulnerability in WebKit/Blink
- CVE-2016-5191: https://bugs.chromium.org/p/chromium/issues/detail?id=639126 -- UXSS introduced through bookmark containing user information -- The idea here is to craft a malicious URL and trick the user so that he bookmarks it. Then, the malicious URL which contains some JS code, is going to lead to the execution of the malicious JS in the context of whichever domain is currently loaded in the active tab.
- CVE-2016-5181: http://www.cvedetails.com/cve/CVE-2016-5181/ -- Vulnerability in WebKit/Blink
- CVE-2016-5165: https://bugs.chromium.org/p/chromium/issues/detail?id=618037 -- Devtools old remote frontend allows running privileged scripts via overwriting localStorage settings -- Attacker can run arbitrary javascript code via watchExpression that runs in the context of the website when DevTools is launched.
- CVE-2016-5164: http://www.cvedetails.com/cve/CVE-2016-5164/ -- Vulnerability in WebKit/Blink
- CVE-2016-5148: http://www.cvedetails.com/cve/CVE-2016-5148/ -- Vulnerability in WebKit/Blink
- CVE-2016-5147: http://www.cvedetails.com/cve/CVE-2016-5147/ -- Vulnerability in WebKit/Blink
- CVE-2015-1286: http://www.cvedetails.com/cve/CVE-2015-1286/ -- Vulnerability in WebKit/Blink
- CVE-2015-1285: http://www.cvedetails.com/cve/CVE-2015-1285/ -- Vulnerability in WebKit/Blink
- CVE-2015-1264: https://bugs.chromium.org/p/chromium/issues/detail?id=481015 -- XSS in the bookmark button
- CVE-2014-3197: https://bugs.chromium.org/p/chromium/issues/detail?id=396544 -- XSS filter information leak -- The idea here is to try to guess a secret that is on a victim's page by writing a malicious script after a anchor in the URL and see whether the XSS Filters reacted.
- CVE-2014-1747: https://bugs.chromium.org/p/chromium/issues/detail?id=330663 -- UXSS from a local MHTML file
- CVE-2014-1701: https://bugs.chromium.org/p/chromium/issues/detail?id=342618 -- UXSS via dispatchEvent on iframes

### Edge/IE
- https://www.brokenbrowser.com/sop-bypass-uxss-tweeting-like-charles-darwin/
- https://www.brokenbrowser.com/sop-bypass-uxss-stealing-credentials-pretty-fast/
- https://www.brokenbrowser.com/sop-bypass-abusing-read-protocol/
- https://www.brokenbrowser.com/uxss-edge-domainless-world/
- https://blog.innerht.ml/ie-uxss/ -- Freeze the browser using alert box or synchronous AJAX call (use XMLHTTPRequest.open() with false as 3rd parameter: synchronous call). The goal here is to achieve thread blocking. Before redirecting to target resource, script execution does not break SOP because redirect.php is still on the same origin of the attacker's. However, once the target resource finished loading on frame 1, Internet Explorer will update the origin information accordingly. As a result, the previous script execution will suddenly be executed on the targets' origin. As a side note, the attack has to be done using two frames because Internet Explorer will remove all the object references once navigation occurs. The suggested fix would be either terminate the script execution or remain the origin information when navigation occurs. More details about this attack: http://danielebellavista.blogspot.kr/2015/02/uxss-multiple-targets-poc-cve-2015-0072.html

### Vulnerabilities classifier

| Attack vector | Consequences of the attack | Browser | Browser Version | Operating System | Link |
| ------------- | -------------------------- | ------- | --------------- | ---------------- | ---- |
| Exploit XSS Auditor's blocking mode (brute force) | Leaking information of any webpage from a different origin | Chromium | 54.0.2840.71 | Ubuntu 14.04 | CVE-2017-5045: https://bugs.chromium.org/p/chromium/issues/detail?id=667079 |
| Malicious extension | There is a XSS vulnerability in chrome://downloads that allows an extension to run a program without user interaction: launches an external program, performs XSS in chrome://downloads, bypasses the dangerous file check --> Note: This is not really a UXSS, here the SOP is not bypassed, but extensions can run any program| Chromium | 54.0.2840.90 | / | CVE-2017-5020: https://bugs.chromium.org/p/chromium/issues/detail?id=668653&desc=2 |
| Use result of drag and drop in an unsafe way (XSS) | Launching apps, Enumerating the browsing history, Disabling extensions | Chromium | 54.0.2840.90 | / | CVE-2017-5018: https://bugs.chromium.org/p/chromium/issues/detail?id=668665 |
| Universal XSS through removing link elements | Attacker can bypass the ScriptForbiddenScope and corrupt the DOM tree | Chromium | 54.0.2840.87 | / | CVE-2017-5010: https://bugs.chromium.org/p/chromium/issues/detail?id=663476 |
| Universal XSS by polluting private scripts with named properties | return a DOM node if there's one named "privateScriptController". If the node is a plugin element then |privateScriptControllerObject->Get(context, v8String(isolate, "import"))| will run an interceptor. This allows an attacker to run script in the middle of node adoption and corrupt the DOM tree. | Chromium | 54.0.2840.99 | / | CVE-2017-5008: https://bugs.chromium.org/p/chromium/issues/detail?id=668552 |
| Universal XSS through bypassing ScopedPageSuspender with closing windows | Allows an attacker to circumvent the suspender and perform synchronous loads in unexpected circumstances | Chromium | 55.0.2883.75 | / | CVE-2017-5007: https://bugs.chromium.org/p/chromium/issues/detail?id=671102 |
| SOP bypass using about:blank | Create about:blanks without domains. Thus we can access every about:blank regardless of its domaini. The top window containing an about:blank iframe has access to the sub-iframes also containing about:blank sub-iframes, completely bypassing the SOP | Edge | / | / | https://www.brokenbrowser.com/sop-bypass-uxss-tweeting-like-charles-darwin/ |
| A server-redirect combined with a data-uri end up bypassing the Same Origin Policy | The bug happens because we can force a window to change its location as if the initiator were the window itself. Edge confused the real initiator of the request | Edge | / | / | https://www.brokenbrowser.com/sop-bypass-uxss-stealing-credentials-pretty-fast/ |
| SOP bypass using Reading mode |  | Edge |  |  | https://www.brokenbrowser.com/sop-bypass-abusing-read-protocol/ |
| SOP bypass using about:blank | The about:blank is a very special URL that sometimes gets confused and it does not know where it belongs to | Edge |  |  | https://www.brokenbrowser.com/uxss-edge-domainless-world/ |
| Freeze browsers' process with alert()/synchronous XMLHTTPRequest due to JavaScript's single-threaded nature |  | Internet Explorer |  |  | CVE-2015-0072: https://blog.innerht.ml/ie-uxss/ |

### Conclusion

[TODO]
Say how many UXSS attacks we studied, and try to classify all these attacks into groups in order to get some insightful statistics and try to get the most used vulnerabilities to carry out UXSS attacks.
