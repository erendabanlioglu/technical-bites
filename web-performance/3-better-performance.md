https://httparchive.org/


### Runtime Performance

Chrome Dev tools > Performance > Record 
    - With CPU throttling 
    - Without Refresh
    
Click Function call and go to script from Summary

<img width="265" alt="Pasted Graphic" src="https://user-images.githubusercontent.com/8245836/124278408-8164e980-db46-11eb-96bc-4eaeb0c3f482.png">


- Paint Profiler fo paint chunk

- Chrome Dev tools > ESC > Rendering 
    - Paint Flashing


#### How we can Fix Paint Flashing?

- Transform and opacity css could be used in separate layer than layout frame. IT is composite layer
    - Use will-change in css
    - RequestAnimationFrame

`element.style.top = serviceHeight * currentPosition / bodyHeight + "px";`
to   
`element.style.transform = "translateY("+ serviceHeight * currentPosition / bodyHeight + "px" + ")";`


`.services__overlay {
    …
    will-change: transform;
}`



Chrome Dev tools > Command + Shift -> Layer



JS Bytes =! Image Bytes  
Takes more time to parsing JS!


- Html render will be blocked till daha (json) arrived and compiled. Streaming json slow!
- Traspiled code could be costly. 

Windowing, keying, lazy


### Early Flush technique



### HTTP2


Single connection - Multiple Streams - Frames
Lookup table for headers
Package loss hurts HTTP2 performance
