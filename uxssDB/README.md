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
- CVE-2014-1701: https://bugs.chromium.org/p/chromium/issues/detail?id=342618 -- UXSS via dispatchEvent on iframes -- The problem here is that the attacker was able to call "dispatchEvent" on iframe.contentWindow. (Note: DispatchEvent enables to "trigger" an event). In this case, some conditions had to be met for the attack to be successful (such has event handlers returning DOM nodes and so on). In such conditions, an attacker was able to trigger some events and recover the DOM nodes especially the "document" node, which enables to access any part of the embedded page.
- CVE-2013-2849: https://bugs.chromium.org/p/chromium/issues/detail?id=171392 -- Cross-Origin copy&paste / drag&drop allowing XSS -- D&D/C&P black-list doesn't cover srcdoc.
- CVE-2010-1236: https://bugs.chromium.org/p/chromium/issues/detail?id=37383 -- javascript: url with a leading NULL byte can bypass cross origin protection.
- CVE-2009-3264: https://bugs.chromium.org/p/chromium/issues/detail?id=21338 -- Same Origin Policy Bypass via getSVGDocument() method.
- CVE-2009-1414: https://bugs.chromium.org/p/chromium/issues/detail?id=9860 -- ChromeHTML URI handler vulnerability

Some sensitive data extraction can be made using the XSS auditor with X-XSS-Protection using block mode
- CVE-2013-2848: https://bugs.chromium.org/p/chromium/issues/detail?id=176137 -- more details on the XSS Auditor on http://homakov.blogspot.kr/2013/02/hacking-with-xss-auditor.html
- CVE-2013-0909: document.referrer leakage with XSS Auditor page block -- see: http://homakov.blogspot.kr/2013/02/hacking-with-xss-auditor.html


Actually many reported vulnerabilities used the about:blank URL that inherits the parent's origin to carry out attacks. This endpoint is pretty used to carry out attacks to bypass the SOP (see how many of the CVE we studied used this endpoint in their PoC), also lots of attacks based on extensions exploit/vulerabilities, some attacks use interesting tricks to execute javascript in another origin (such as \u0000 in front of javascipt in a URL, or even white spaces in host IP that lead to a bypass of SOP).
--> Things we mentionned, in some cases, it was ambiguous to know who to the vulnerability belonged to (i.e: Who is responsible for this vulnerability, and who should invest time in trying to solve it -- https://bugzilla.mozilla.org/show_bug.cgi?id=1199430 for instance)
--> Some interesting attacks are based on the inheritance of some properties from one domain to another.

### Edge/IE
- https://www.brokenbrowser.com/sop-bypass-uxss-tweeting-like-charles-darwin/
- https://www.brokenbrowser.com/sop-bypass-uxss-stealing-credentials-pretty-fast/
- https://www.brokenbrowser.com/sop-bypass-abusing-read-protocol/
- https://www.brokenbrowser.com/uxss-edge-domainless-world/
- https://blog.innerht.ml/ie-uxss/ -- Freeze the browser using alert box or synchronous AJAX call (use XMLHTTPRequest.open() with false as 3rd parameter: synchronous call). The goal here is to achieve thread blocking. Before redirecting to target resource, script execution does not break SOP because redirect.php is still on the same origin of the attacker's. However, once the target resource finished loading on frame 1, Internet Explorer will update the origin information accordingly. As a result, the previous script execution will suddenly be executed on the targets' origin. As a side note, the attack has to be done using two frames because Internet Explorer will remove all the object references once navigation occurs. The suggested fix would be either terminate the script execution or remain the origin information when navigation occurs. More details about this attack: http://danielebellavista.blogspot.kr/2015/02/uxss-multiple-targets-poc-cve-2015-0072.html

### Mozilla Firefox

- CVE-2016-5262: https://bugzilla.mozilla.org/show_bug.cgi?id=1277475 -- XSS out of iframe sandbox, iframe disabled javascript. marquee
- CVE-2015-7188: https://bugzilla.mozilla.org/show_bug.cgi?id=1199430 -- White-spaces in host IP address, leading to same origin policy bypass
- CVE-2015-7187: https://bugzilla.mozilla.org/show_bug.cgi?id=1195735 -- To disable JS, set { script: false } when creating the panel, but inline JS is still executing (POC: create a browser extension)
- CVE-2014-1530: https://bugzilla.mozilla.org/show_bug.cgi?id=895557 -- It's possible to set a document's URI to a different document's URI by confusing docshell
- CVE-2014-1504: https://bugzilla.mozilla.org/show_bug.cgi?id=911547 -- data-URI + Firefox restart = CSP bypass -- This attack scenario uses the fact that some part of the context is saved by the Browser when the Browser is restarted. Such context save might be used to bypass CSP
- CVE-2013-5612: https://bugzilla.mozilla.org/show_bug.cgi?id=871161 -- Potential XSS with cross-domain (cross-origin) inheritance of charset
- CVE-2013-1714 -- https://bugzilla.mozilla.org/show_bug.cgi?id=879787 -- Cross Domain Policy override using webworkers -- Web Workers makes it possible to run a script operation in background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.
- 


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

- We leanrt many things about web dev in this project: marquee html tag, X-XSS-PROTECTION, Many security mechanism, many attack scenarios, we also saw most of (not to say all) notions that have been presented this semester in this course (clickjacking, XSS, CSRF, UI timing attacks, browser extensions and so on) while we studied the previous attacks in the CVE record, 

What we conclude from this study: UXSS will always occur/new vulns will always be found... --> Many =/= platforms, iOS, Android, Laptop (=/= OS) and so on + Browsers are extremely complicated software. The area for attackers to exploit potential vulnerabilities is really big (many things that can be exploited by attackers --> extensions, =/= internal components of the browser, third party component (cf: Blink/Webkit for instance), and so on...). The diversity of attacks is really really big. We though it would be easy to come up with patterns used to bypass the SoP, but it was not as simple as that. Some patterns can be detected, but this is not as obvious as we first thought.
We learnt a lot, we are not a team specilized/familiar with web development, but througout this study we were able to learn many things about UXSS attacks and about web development in general.
Moreover, while browsers provide users with a way to access resources plublished on the Web, they also ambed a very large number of features that make our web surfing way more agreable. In addition, they implement all sort of security mechanisms to prevent our personal/sensitive data from being accessed leaked out. Nevertheless, some of these mechanisms can be bypassed by attackers. Thus, these malicious users can tehn gain access to victim's sensitive data. That is the reason why web application developpers should not rely on browsers to secure their customer's data. Security on the web has to be handled and taken into consideration by everyone. Web app devs should define strict CSPs, use HTTPONLY cookies to prevent some javascript code from accessing them, do frame busting using the X-FRAME-OPTIONS header, use session IDs for a small amount of time, be careful with quick change of IP address when a user uses a webservice (at login and so on), use strong keys and encryption scheme for encrypted communications (see the paper "How DH fails in practice"), and keep on following the news in the web security areas while keeping their security infrastructure up to date.

-- We saw that a simple small error/lack of check of in a feature in a browser could lead to dramatic vulnerabilities that would threaten all users. A simple Drag and Drop and some malicious code could be added in an embedded/victim page and thus, some malicious code could be executed on his behalf.


To go further: Browsers developers might need to handle discrepancies in network traffic (see paper of SCA based on packet size), since personal data can also be leaked out further to network analysis of a passive attacker. So, despite all encrytpion and security mechanisms that are being implemented by browser developers, they might need to go a step further and hide our network trace to keep our data completelly safe. + (See paper about DH "How DH fails in practice" --> browser developers need to do a perpetual surveillance of what's going on in the security area and stop supporting deprecated Encryption schemeand so on.)

[TODO]
Say how many UXSS attacks we studied, and try to classify all these attacks into groups in order to get some insightful statistics and try to get the most used vulnerabilities to carry out UXSS attacks.
