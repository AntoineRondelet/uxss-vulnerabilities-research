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
https://codereview.chromium.org/2478573002/
- Vulnerability in chrome://apps: It happens when this page is open in a tab, and a malicious page is open in another one. The drag and drop to the area with the app tiles results in that malicious page can be use in an unsafe way and be assign to the innerHTML parameter of an active document element. Since the apps page has no CSP to mitigate it, this can allow the use of NTP APIs such as:
	- Enumerating the browsing history through favicons
	- Querying who is signed in in Chrome
	- Opening restricted URLs (including URLs that normally requires the user to manually type the URL, e.g. chrome://kill)
	- Disabling extensions
	- Launching apps
	- Filling the preferences database with junk (AppLauncherHandler::HandleSaveAppPageName does not validate the bounds on the parameters)  
CVE-2017-5018: https://bugs.chromium.org/p/chromium/issues/detail?id=668665
VERSION
Chrome version: 54.0.2840.90 (stable), 57.0.2933.0 (latest)
Nov 2016
- Vulnerability when link element is removed from its parent when linked to the last pending stylesheet: When a stylesheet happens to be the last pending one in the document and that a link element is aware of its removal, this can result on fragment anchor and then layout updates which are forbidden. Tthe updates may end up resolving a FontFace load promise, which allows an attacker to bypass the ScriptForbiddenScope and corrupt the DOM tree. The parent function may also endup firing a focus event that runs arbitrary code.
CVE-2017-5010: https://bugs.chromium.org/p/chromium/issues/detail?id=663476
https://www.exploit-db.com/exploits/41866/
VERSION
Chrome 54.0.2840.87 (Stable)
Chrome 55.0.2883.35 (Beta)
Chrome 56.0.2906.0 (Dev)
Chromium 56.0.2914.0 (Release build compiled today)
Apple WebKit / Safari 10.0.3 (12602.4.8)
-  CVE-2017-5008: https://bugs.chromium.org/p/chromium/issues/detail?id=668552
VERSION
Chrome 54.0.2840.99 (Stable)
Chrome 55.0.2883.59 (Beta)
Chrome 56.0.2924.3 (Dev)
Chromium 57.0.2932.0 (Release build compiled today)
- CVE-2017-5007: https://bugs.chromium.org/p/chromium/issues/detail?id=671102
#### Android
- https://bugs.chromium.org/p/chromium/issues/detail?id=144813
- https://www.cyberintelligence.in/google-play-store-vulnerable-to-xss-and-uxss-attacks/

#### Extension
- Flash Player Flaw CVE-2011-2107: This was an important vulnerability that allows remote attackers to inject arbitrary web script or HTML via unspecified vectors, when victim visits malicious website.
http://www.adobe.com/support/security/bulletins/apsb11-13.html
VERSION
Adobe Flash Player 10.3.181.16 and earlier versions for Windows, Macintosh, Linux and Solaris operating systems
Adobe Flash Player 10.3.185.22 and earlier versions for Android
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


