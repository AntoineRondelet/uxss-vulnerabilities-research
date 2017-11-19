# UXSS recorded vulnerabilities

This folder contains some of the UXSS patterns (see ./patterns) that have been used against Browsers in the past. We record some of them in this repository to try to extract valuable information from the study of these previous attacks. Hopefully, we might be able to draft our own attack based on this record.

## UXSS Studied:

### Chrome:
- CVE-2017-5069: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
- CVE-2017-5045: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
- CVE-2017-5020: https://bugs.chromium.org/p/chromium/issues/detail?id=668653&desc=2
- CVE-2017-5018: https://bugs.chromium.org/p/chromium/issues/detail?id=668665
- CVE-2017-5010: https://bugs.chromium.org/p/chromium/issues/detail?id=663476
- CVE-2017-5008: https://bugs.chromium.org/p/chromium/issues/detail?id=668552
- CVE-2017-5007: https://bugs.chromium.org/p/chromium/issues/detail?id=671102

### Edge/IE
- https://www.brokenbrowser.com/sop-bypass-uxss-tweeting-like-charles-darwin/
- https://www.brokenbrowser.com/sop-bypass-uxss-stealing-credentials-pretty-fast/
- https://www.brokenbrowser.com/sop-bypass-abusing-read-protocol/
- https://www.brokenbrowser.com/uxss-edge-domainless-world/
- https://blog.innerht.ml/ie-uxss/

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
|  |  | Internet Explorer |  |  | https://blog.innerht.ml/ie-uxss/ |

### Conclusion

[TODO]
Say how many UXSS attacks we studied, and try to classify all these attacks into groups in order to get some insightful statistics and try to get the most used vulnerabilities to carry out UXSS attacks.
