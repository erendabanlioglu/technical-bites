## More

- Brotli, shrinkRay

- Find not encoded resources.
	Network -> Search -> -has-response-header:Content-Encoding

### HTTP Caching

**Cache-Control vs ETag**

- Should I go to the server vs Should I send asset to the client
- Etag controls if there is a new version of the content/asset
- Response Header - Etag, If-None-Match

￼![image3](https://user-images.githubusercontent.com/8245836/124277457-5a59e800-db45-11eb-9f29-01bfb841d205.png)



####Choose the Cache-Control Strategy

￼![http-cache-decision-tree](https://user-images.githubusercontent.com/8245836/124277497-63e35000-db45-11eb-9977-8d895b5546f5.png)


More https://csswizardry.com/2019/03/cache-control-for-civilians/


### Resource Hints

preconnect | prefetch | preload  
`<link rel="preload" … >`  
Link: `rel=preload; </app/script.js>;  as=script; nopush`  

- preload - force browser to download. For current page - 2016
- prefetch - hint browser to download. For next page - 2006
- preconnect -

_Some prefetching solutions: Quicklink, Guess.js, instant_page_

Client Hints - 
Priority Hints - https://developers.google.com/web/updates/2019/02/priority-hints

navigator.connection.effectiveType
navigator.connection.saveData


### CDN Usage

Netlify - static
Heroku - dynamic
Github as CMS



Custom Performance Metric - Time to First Tweet

https://web.dev/

Save for overrides, chrome web tool

Find unused and remove css - Purifycss.online  



### Navigation Timing API

<img width="1653" alt="Pasted Graphic" src="https://user-images.githubusercontent.com/8245836/124277618-85443c00-db45-11eb-9181-9a1b5678eed3.png">


https://www.w3.org/TR/navigation-timing-2/timestamp-diagram.svg

Avoid Redirect

### TCP

connectstart - connectEnd  
secureConnectionStart - connectEnd

### Request/Response

Request Start - response start  
Resposnse Start - Response End

<img width="330" alt="Pasted Graphic 1" src="https://user-images.githubusercontent.com/8245836/124277686-9f7e1a00-db45-11eb-9130-1d32de56f328.png">


### Resource Timing API 

https://www.w3.org/TR/resource-timing-1/resource-timing-overview-1.png


- https://Perfume.js is library of pollyfill for all important metrics

https://www.webpagetest.org/

GitHub actions
