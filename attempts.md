# UXSS-Vulnerabilities-Project

This project is carried by Antoine Rondelet and Ndeye Khady Ngom. 
It aims to study and find UXSS vulnerabilities in the Brave Browser.

## Working environment

### Machine used to carry out the research

MacBook Air (13-inch, Early 2014), running macOS Sierra v10.12.6

### Version of Brave

![Brave version](.github/BraveVersion.png)

### Extension of our work to other web browsers

- Whale browser by Naver: Version 1.0.37.16 (64-bit), released in October 23, 2017
- Firefox Quantum by Mozilla: Version 57.0 (64 bits), released in November 14, 2017
- Safari by Apple: Version 10.1.2

## List of our attempts to find vulnerabilities:

*Note*: The list of malicious HTML pages we crafted in order to carry out this research can be found in the `./playground/` repository.

- __XMLHTTPRequest__: Embed a website into an iFrame using `XMLHttpRequest`, by trying to modify the HTTP headers of the request. For instance, we could try to modify the `Referer` and `User-Agent` headers. Such modifications would allow us to bypass the `X-Frame-Options` policy of a victim website.

- __Fetch__: Embed a website into an iFrame using the `Fetch` API, by trying to modify the HTTP headers of the request. For instance, we could try to modify the `Referer` and `User-Agent` headers. Such modifications would allow us to bypass the `X-Frame-Options` policy of a victim website.

- __Extensions__: Study Brave's extensions in order to find a vulnerability. According to the small number of extensions supported by Brave, and looking at the reported vulnerabilities on Adobe Reader, we tried to find vulnerabilities in the "PDF viewer" plugin. Thus, we added JS payload after anchors in URLs, in the form of `testwebsite.com/test.pdf#<javascriptPayload>`, in order to see the behavior of the pdf viewer. Such attempts allowed us to see if malicious code could be executed. To do so, we tested multiple methods to write our payloads:
  - For the first attempt, we didn't use character escaping for the payload. We just wrote it as is (ex: `<script>alert(1)</script>`)
  - Then, we used character escaping technics specified in (https://www.owasp.org/index.php/XSS_Filter_Evasion_Cheat_Sheet) in order to craft a malicious paylaod. Note that none of these attempts lead to satisfactory results.
  - Finally, we tried to generate an XSS condition by "encoding" our payloads in "JSFuck" (http://www.jsfuck.com). This method consisted in bypassing all XSS filters mechanisms by writing javascript code with only 6 characaters. For instance `alert(1)` is equivalent to `[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]((![]+[])[+!+[]]+(![]+[])[!+[]+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]+(!![]+[])[+[]]+(![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[!+[]+!+[]+[+[]]]+[+!+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[!+[]+!+[]+[+[]]])()` is JSFuck syntax.

- __Variable Clobbering__: In this attack scenario, we wanted to see whether it was possible to prevent frame busting scripts from working by over writing some global javascript variable commonly used to write frame busting scripts (the assumption here was that victim web apps didn't defined `X-Frame-Options` policies.) (reference: "Busting Frame Busting: a Study of Clickjacking Vulnerabilities on Popular Sites"). __Note that__ we extended this technique by trying to redefine the `window` javascript variable or some of its methods. Our idea here was to over-write methods of this object that are likely to be called by an embedded website in an iFrame. Such scenario would enable use to have some javascript (the body of the method we redefine) to be executed in the context of the victim's website.

- __Bypassing javascript schemes__: We realized thats `javascript:` URIs were handled in a special manner in the Brave browser. This handling is done thanks to a regular expression that matches the word `javascript` in the URL. The idea here was to bypass this security mechanism, and try to define a `javascript` URI whch would not be detected by the regular expression. Such scenario could expose the browser to some vulnerabilities, adn help us building refined attack scenarios on top of it. In order to bypass the regular expression check, we tried to define `javascript` URI by:
    - Using upper case scheme: `JAVASCRIPT`
    - Splitting the scheme into 2 parts seprated by a space: `JAVA%20SCRIPT`
    - Using URL encoding to encode "javascript" `%4A%41%56%41%53%43%52%49%50%54`

- __Freeze the browser to execute malicious code__: The idea here was to try to embed a page with a `X-Frame-Options:` header set to `SAMEORIGIN`. Then, we tried to change the `location` of the parent page to the same origin as the page we wanted to embed. Newt, we blocked the browser directly via a javascript event. In that case, we wanted to see whether the parent's origin could match the origin of the website we wanted to embedded. The idea here was to benefit from the fact that the browser was frozen to set the `origin` of the parent page to the `origin` of the victim website, while blocking the redirect and being able to execute malicious code in the context of the victim webpage. This would have led to a full SOP bypass.

- Find more information about "Fuzzing" and try to see whether we could apply this method in our case (generate semi-valid JS to corrumpt V8 for instance) **--> TODO**
  - See: https://github.com/v8/v8/tree/master/test/fuzzer
  - Video Talk: https://www.youtube.com/watch?v=qTkYDA0En6U

- __Change the domain maliciously__: This attempt was a bit naive but is worth mentionning here as part of the record of our work. The idea here was to try to make the parent origin match the origin of a victim/embedded website. In our case, the domain was not a prefix of the targeted website's domain, so te attempt was rejected. However, we know that when we called the `document.domain` setter, the port number was erased. Thus we tried to see whether we could maliciously set the port number in the `document.domain`. The idea here was to run `document.domain="victim.com%3A80"` (with `%3A` the URL encoding of `:`) to try to set the port number, and maybe find a way to make origins match.

- __Bookmark feature__: We investigated whether we could trigger a malicious behavior after bookmarking a page launched from a maliciously crafted URL. The idea here was to bookmark a page like `www.example.com/<script>alert(1)</script>`, and see whether we could trigger an XSS condition by "bookrmarking" this malicious URL. Moreover, we tried to input malicious javascript code in the multiple fields available on the bookmark setting pag of Brave. Thsi idea was to see whether the user inputs were handled/sanitized properly. If this wasn't the case, this would have been the opportunity for us to try and run malicious code with the priviledges of the browser.

- __Domainless page__: Here, we tried to create a domainless `about:blank` page. The purpose of this scenario was to see whether a domainless page could actually bypass the SOP mechanism of the browser. We wanted to see whether the origin checks included the case of a `null` origin.
While trying to reproduce this scenario, we realized different behaviors between Safari (first image) and Brave (second image):
![About Blank in Safari](.github/AboutBlankSafari.png)
![About Blank in Brave](.github/AboutBlankBrave.png)


After further research, we found that `about:blank` pages inherited the security mechanisms from the pag they were called from. Thus, as Brave "home"/"default" page actually comes from a chrome extension, the `about:blank` page inherited its origin.


In the case of Safari, `about:blank` called from the "home" page has not origin. 
We then decided to continue the attack scenario with Safari. We managed to include `bing.com` into an iFrame on our `about:blank` page. 
From this point, we tried many commands to try to execute code in this victim iFrame:

A first idea was to define malicious events on the iframe and see if the associated functions could be executed in the context of the iframe:

```
var frame = document.getElementsByTagName('iframe')[0]

frame.onmouseover = function() {
  var script = document.createElement('script'); 
  script.type = 'text/javascript'; 
  var code = 'alert("hello world!");'; 
  script.appendChild(document.createTextNode(code)); 
  document.body.appendChild(script);
}
```

or

```
frame.onmouseover = function() {
  var script = document.createElement('script'); 
  script.type = 'text/javascript'; 
  var code = 'var string = "cookie: " + document.cookie; alert(string);'; 
  script.appendChild(document.createTextNode(code)); 
  document.body.appendChild(script);}
```

Without surprise, such events were executed in the context of the parent. In fact, when we tried to access the actual content of the iframe, by doing:
`var innerDoc = frame.contentDocument || frame.contentWindow.document`, the browser threw exceptions to block our actions.

Then we tried to copy the variable `frame` into another variable to see whether we could find ways to access the value of the frame's `contentDocument`: 
```
var mFrame = Object.create(frame);
var tfrBody = HTMLBodyElement(mFrame.contentDocument);
```

We finally tried to block the browser while trying to change the location and access the HTML elements inside the iFrame:
```
window.setTimeout('alert("Blocking"); 
document.location.protocol = "http:"; 
var frame = document.getElementsByTagName("iframe")[0]; 
var bodyTarget = frame.contentDocument.getElementsByTagName("body")[0]; 
document.getElementById("savedValue").innerHTML = bodyTarget.innerHTML', 400);
```

- __Data URI__: We realized that if we entered: `data:text/html,<script>alert("test")</script>`, this code was executed in the Brave browser. From this observation, we tried a myriad of manipulations to see to which extend we could use this URI to create a XSS condition. We set the URL to `data:text/html,`, and then opened the developer console. We then embedded a website into an iframe by doing `document.body.innerHTML = '<iframe src="http://www.bing.com/images/search?q=microsoft+edge"></iframe>'`. However, at this point we were in the same situation as we were in Safari with the domainless `about:blank` URI. Unfortunately, we couldn't find concrete attack scenarios in which we could use this URI to bypass the SOP

- __History API__: We tried to use the "history API" to change the URL of the page without reloading it. The idea here was to see whether we were able to change the origin without actually being redirected or without reloading the page (`window.history.pushState("test", "Title", "about:passwords");`). Reference: https://stackoverflow.com/questions/3338642/updating-address-bar-with-new-url-without-hash-or-reloading-the-page.

- __About URI__: We tried to use the different setting pages provided by the browser (like `about:bookmarks`, `about:passwords`) to see whether we could embed other setting pages. The idea here was to see whether an attacker can start an attack from the `about:bookmarks` page, and manage to embed the `about:passwords` into this page. Our first idea was to benefit from the fact that this pages had the same origin, for the attacker to access all the victim's passwords from the bookmark page. Unfortunately, this scenario was a bit far fetched and proved to be unsuccessful. 

- __Drag and Drop API__: The idea here was to find a way to drag some malicious JS code and drop it into the victim iframe. In such case, we would have  chance that the malcious would be executed in the context of the victim page. 

- __Events (2)__: We tried to use events a second time, but without creating script nodes this time. The idea here was to trigger an event from the inside of the frame each time the user's mouse went over the frame (onmouseover for instance). Such scenario is detailled below:
  - Open Brave and go to `data:text/html,`
  - Embed Bing in an iFrame on the page: `document.body.innerHTML = '<iframe src="http://www.bing.com/images/search?q=microsoft+edge"></iframe>'`
  - Select the iFrame: `var iframe = document.getElementsByTagName('iframe')[0];`
  - Define your event: `iframe.onmouseover = alert(iframe.innerHTML);` (Note that here, we can also try to append a script into the iFrame, but we realized that the script was actually appended outside the actual document (before the `head` and `body` tags...))

- __Malicious (custom) header names and values__: The idea here was to "fool" the browser by defining custom "malicious" HTTP headers. We realized that we were able to set custom HTTP headers whose names were set as value of the `access-control-request-headers:` HTTP header (in the case of `no-cors` mode). Thus, we tried to define malicious header names and see whether we could use this information to add malicious data in our request.
Below the screenshot of the attempt to modify the Headers VALUES (`cors` mode):

![Try to forge malicious Headers' values](.github/maliciousHeadersValues.png)

Below the screenshot of the attempt to modify the Headers NAMES (`no-cors` mode):

![Try to forge malicious Headers' names](.github/maliciousHeadersNames.png)

- __Web workers and service workers__: Web workers enable to run scripts in background thread that are separated from the main execution thread of a web application. So we tried to see how the browser behaved when an `XMLHTTPRequest`/`Fetch` request trying to alter HTTP headers was triggered from a web worker. Indeed, the idea here was to see whether the SOP checks were applying to web workers in the same extend as they apply when a request is initiated by the main thread. Later, we defined a service worker dedicated to intercept all our requests, and which aimed to modify the request with malicious headers, leading to a full bypass of CORS mechanisms. If this bypass were possible, we would have been able to implement a function to modify the responses in the service worker, and maybe, we would have been able to inject malicious scripts in the response, which could have lead to a full SOP bypass.

## Contact

If you detected any mistake, or have any question about our research, please do not hesitate to contact us at: rondelet.antoine@gmail.com
