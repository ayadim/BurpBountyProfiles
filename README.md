# BurpBountyProfiles
my custom Burp Bounty (extension) profiles

# XXE_Xinclude.bb
XInclude attacks

Some applications receive client-submitted data, embed it on the server-side into an XML document, and then parse the document. An example of this occurs when client-submitted data is placed into a back-end SOAP request, which is then processed by the backend SOAP service.

In this situation, you cannot carry out a classic XXE attack, because you don't control the entire XML document and so cannot define or modify a DOCTYPE element. However, you might be able to use XInclude instead. XInclude is a part of the XML specification that allows an XML document to be built from sub-documents. You can place an XInclude attack within any data value in an XML document, so the attack can be performed in situations where you only control a single item of data that is placed into a server-side XML document.

To perform an XInclude attack, you need to reference the XInclude namespace and provide the path to the file that you wish to include. For example:

<foo xmlns:xi="http://www.w3.org/2001/XInclude"><xi:include parse="text" href="file:///etc/passwd"/></foo> 
https://portswigger.net/web-security/xxe 

# BlindXXE_Xinclude_SSRF.bb
XInclude attacks 
the main question is can we commit a SSRF attack  using Xinclude? the profile use Burp collaborator to submit a test to the target and see if the target send back an http request to validate the existance of SSRF.

# Possible XML Request_XXE.bb
finding a way to make a request that can parse an XML syntax is very important and open up an opportunity to exploit XXE vulnerablity.

# SSTI.bb (Server Side Template Injection)
 it allows a hacker to inject template  code into the website. The effects of this can be devastating, from XSS,  all the way to RCE and also you can read internal files.

# Custom_SSRF.bb
Some times we need to customize host to perform SSRF that's way i created this profile.. before launching scan you need to change {custom_host} to Attacker:80 host.
Example : 
change {custom_host} to 10.10.10.15:9000
nc -vlp 9000
you will get request from target machine to your netcat listenner.
10.10.202.64 - - [27/Oct/2020 12:57:20] code 404, message File not found
10.10.202.64 - - [27/Oct/2020 12:57:20] "HEAD /SSRF_ATTACK_FROM_BurpSuit HTTP/1.1" 404 -


