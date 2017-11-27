# UXSS recorded vulnerabilities

This folder contains some of the UXSS patterns (see ./patterns) that have been used against Browsers in the past. We record some of them in this repository to try to extract valuable information from the study of these previous attacks. Hopefully, we might be able to draft our own attack based on this record.

## UXSS Studied:

### Chrome:
#### Browser
- Use of the XSS auditor blocking mode to leak information
 Xss auditor is a function use with the X-XSS-Protection HTTP header which is a non-standard header, to mitigate XSS attacks. It analyses query parameters and aims to identify malicious javascript code. Xss audito blocks server responses with such identified code to avoid injected payloads. Now this blocking mode can be exploited as a vulnerability. An attacker can use it to have some information about a blocked script that has a different origin than the webpage itself by loading it and trying to reproduce it. When XSS Auditor is triggered and blocks a page, it prevents the iframe's onload event handler to be called. So the attacker just have to check this call in order to brute force javascript variables and therefore leaks user information.
CVE-2017-5069: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
VERSION
Chrome Version: [54.0.2840.71] + [stable]
Operating System: [Ubuntu 14.04]
Jan 2017
XSS Auditor present in Google Chrome prior to 57.0.2987.98 for Mac, Windows, Linux and 57.0.2987.108 for Android
- CVE-2017-5045: https://bugs.chromium.org/p/chromium/issues/detail?id=667079
- CVE-2017-5018: https://bugs.chromium.org/p/chromium/issues/detail?id=668665
- CVE-2017-5010: https://bugs.chromium.org/p/chromium/issues/detail?id=663476
- CVE-2017-5008: https://bugs.chromium.org/p/chromium/issues/detail?id=668552
- CVE-2017-5007: https://bugs.chromium.org/p/chromium/issues/detail?id=671102
#### Android
- https://bugs.chromium.org/p/chromium/issues/detail?id=144813
- https://www.cyberintelligence.in/google-play-store-vulnerable-to-xss-and-uxss-attacks/

#### Extension
- Flash Player Flaw CVE-2011-2107: http://www.adobe.com/support/security/bulletins/apsb11-13.html
- chrome://downloads vulnerability that allows a malicious extension to run a program without user interaction: When the victim installs or upgrades a malicious extension, the XSS is perform on chrome://downloads by setting the extension name in the innerHTML assignment. This with the bypassing of CSP and safe browsing, will allow when the user click to run a program outside of chrome, the extension to run arbitrary code NS
CVE-2017-5020: https://bugs.chromium.org/p/chromium/issues/detail?id=668653&desc=2
VERSION
Chrome version: 54.0.2840.90 (stable), 55.0.2883.59 (beta), 57.0.2931.0 (Canary)

### Edge/IE
#### Browser
- https://www.brokenbrowser.com/sop-bypass-uxss-tweeting-like-charles-darwin/
- https://www.brokenbrowser.com/sop-bypass-uxss-stealing-credentials-pretty-fast/
- https://www.brokenbrowser.com/sop-bypass-abusing-read-protocol/
- https://www.brokenbrowser.com/uxss-edge-domainless-world/
- https://blog.innerht.ml/ie-uxss/
- Flaw in the XSS filters of Internet Explorer 8: http://p42.us/ie8xss/Abusing_IE8s_XSS_Filters.pdf

#### Extension
- Vulnerability in the Adobe Acrobat extension for Internet Explorer 6 (or Mozilla plugin): https://events.ccc.de/congress/2006/Fahrplan/attachments/1158-Subverting_Ajax.pdf


