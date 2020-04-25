# Kontra Appsec Notes
***

## Server Side Request Forgery (SSRF)

* Think of this as making requests on behalf of the server, kinda like cross site request forgery
* The actual definition is: The ability of manipulating a web app into sending unauthorized requests to a 3rd party site or resource

SSRF vulnerabilities are most commonly encountered in functionality associated with: 
* PDF generation (**EX**: Generating PDF reports, credit card statements)
* File upload (**EX**: Uploading scanned documents, image files, etc)

The following demonstration is done by uploading an image to capitalten's server to customize your card:

![](/home/n9/study/cybernotes/kontra-appsec/url.png) 

As you can see, once the image is uploaded the we get a 'url=' parameter. 

To confirm we can make requests on behalf of the server, attempt to insert a domain completely unrelated to the website, in this case we use hxxp://catmemes.com/latest/cat-17439664.png

![](/home/n9/study/cybernotes/kontra-appsec/urltrick.png) 

By changing this 'url=' parameter, we are able to make requests to websites on behalf of the server. This can be abused by requesting info from internal domains.

![](/home/n9/study/cybernotes/kontra-appsec/firstcontact.png) 

As you can see, we passed an internal AWS metadata URL which returns all instance metadata associated w/Capitalten's webserver. Now from here, it's just a game of directory traversal.

![](/home/n9/study/cybernotes/kontra-appsec/2contact.png) 
