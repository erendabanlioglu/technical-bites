## More

- Brotli, shrinkRay

- Find not encoded resources.
	Network -> Search -> -has-response-header:Content-Encoding

### HTTP Caching

**Cache-Control vs ETag**

- Should I go to the server vs Should I send asset to the client
- Etag controls if there is a new version of the content/asset
- Response Header - Etag, If-None-Match



Choose the Cache-Control Strategy



More https://csswizardry.com/2019/03/cache-control-for-civilians/


Resource Hints

preconnect | prefetch | preload  
`<link rel="preload" … >`  
Link: `rel=preload; </app/script.js>;  as=script; nopush`  

- preload - force browser to download. For current page - 2016
- prefetch - hint browser to download. For next page - 2006
- preconnect -

Some prefetching solutions: Quicklink, Guess.js, instant_page

Client Hints - 
Priority Hints - https://developers.google.com/web/updates/2019/02/priority-hints

navigator.connection.effectiveType
navigator.connection.saveData


CDN Usage

Netlify - static
Heroku - dynamic

Github as CMS



Custom Performance Metric - Time to First Tweet

https://web.dev/

Save for overrides, chrome web tool

Find unused and remove css - Purifycss.online  

 Navigation Timing API  
￼

https://www.w3.org/TR/navigation-timing-2/timestamp-diagram.svg

Avoid Redirect

TCP  connectstart - connectEnd secureConnectionStart - connectEnd

Request/Response 
Request Start - response start Resposnse Start - Response End

￼

Resource Timing API 

https://www.w3.org/TR/resource-timing-1/resource-timing-overview-1.png


- https://Perfume.js is library of pollyfill for all important metrics

https://www.webpagetest.org/

GitHub actions
