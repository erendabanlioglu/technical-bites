# Web Performance


DOMContentLoaded: 75 ms. Load: 175 ms  
DOMContentLoaded: 8.53 s   Load: 43.22 s

* 11.7 - Text
* 30.1 - Image
* 34.2 - Font


! 6 TCP connection max for 1 domain HTTP1



## CSS MIN

7.5kb - 437.61 ms  
5kb - 311.83 ms

_No Change_



## JS MIN

261 KB - 8.31 s [jquery].   ——  134 KB - 4.34s  
1.4 KB - 140ms [scripts]    —— 1.1 KB - 138ms

DOMContentLoaded: 4.50 s  Load: 41.83 s
- 7.52 - Text
- 19.77 - Image



## Text Compression

- HTML- accept-encoding: gzip
- JSON and compressed HTML effectively is same
- Only Encode HTML, JS, CSS. Excepts small ones


DOMContentLoaded: 1.50 s  Load: 40.78 s 
- 4.52 - Text
- 11.41 - Image



## Image Compression 

- Used tiny png

DOMContentLoaded: 1.49 sLoad: 21.70 s
- 4.52 - Text
- 8.76 - Image


Automation = Npm + parcel.js  
Removed the Web Font = DOMContentLoaded: 1.24 s. Load: 17.86 s  . Less than 1s to see text.



### Optimized Web Fonts

https://github.com/fontello/ttf2eot
https://github.com/fontello/ttf2woff
https://github.com/nfroidure/ttf2woff2

### Automating

"generate:eot": "ls fonts/*.ttf | sed -e 's/\\.ttf//g' | xargs -I % ttf2eot %.ttf %.eot",

sed - search and replace
explainshell.com


@font-face {
    font-family: 'Raleway';
    font-style: normal;
    font-weight: 400;
    src: local('Raleway'),   ——> Check if this font exist on users machine
    local('Raleway-Regular'),
    url("../fonts/Raleway-Regular.woff2") format("woff2"),
    url("../fonts/Raleway-Regular.woff") format("woff"),
    url("../fonts/Raleway-Regular.eot") format("embedded-opentype"),
    url("../fonts/Raleway-Regular.ttf") format("truetype");
}

#### Generating subset of web fonts*

We don’t nee all language characters use only the languages we support.

#### Unicode vs UTF?

fromCodePoint() take unicode and turn into the utf hex string value  Google Fonts doing this automatically 


Prevent empty page without font (Fallback font immediately available.)
- Add font-display: swap;
- Find good fallback font  https://meowni.ca/font-style-matcher/
- You can add ?display=swap parameter on google fonts as well
- 

## NOTES

#### Image Optimization

- Put image to the html if image is important and have to be there
- img@srcset -> use it to choose correct size for size of hints but browser decides. Even battery level can change the result.
- <picture> tag
- JPEG quality
- Progressive JPEG - load bad quality and load higher later [ Imagemin - tool ]
- Webp
- Client hint
- HTTP2 don’t need sprites

Lazy Loading, there is new native one


#### CSS

- Removed unused css files. Coverage section on chrome dev tool or Unused plugins
- CSS above the fold technic. Adds complexity
- critical.js switches stylesheets to preload and it doesn’t block rendering.

#### JS 
  
- Move scripts to the bottom
- JS Async vs defer. Async execute immediately after downloaded, defer is not. 
    - Defer over async
    - <script async>
    - <script defer>
- ScriptStreamerThread on chrome dev tool
    - “Parse Script” It is advanced opt. technic which pre parses the JS on separate thread.


#### 3rd Party JS
  
- Performance - Bottom Up - Group By Product
- Show Third Party Badges
https://www.thirdpartyweb.today/




