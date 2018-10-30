# Browser

## What is CORS?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell a browser to let a web application running at one origin (domain) have permission to access selected resources from a server at a different origin.

## How to cross origin?
[more details](https://segmentfault.com/a/1190000011145364)
since the same-origin-policy, we cannot send a request to get data from different origin
1. CORS mechanism: it is decided by server of the requested source(the server decides Access-Control-Allow-Origin)
2. JSONP
3. proxy server- nginx
4. websocket(HTML5)
5. nodejs as middleware

## Event delegation:
* define: add a event listener to a single common parent rather than each child, based on the event bubbling mechanism
* when to use?
   we want some code to run when you click on any one of the child elements, we can set the event listener on their parent and have the effect of the event listener bubble to each child, rather than having to set the event listener on every child individually.
[more details here](https://www.cnblogs.com/bfgis/p/5460191.html)

## Event flow
1. event  flow  includes capture phase, target phase and bubble phase.
2.	Capturing phase – the event goes down to the element.
3.	Target phase – the event reached the target element.
4.	Bubbling phase – the event bubbles up from the element
5.  capture and bubble phase are event propagation
6. we can use stopPropogation to stop
## Critical Rending Path
1. Constructing the DOM Tree
2. Constructing the CSSOM Tree
3. Running JavaScript  - parser blocking resource
4. Creating the Render Tree
5. Generating the Layout
6. Painting
## Frame
* FPS: frame per second, for current browser, it's 60 fps
* so, every frame takes 1000/60 = 16.667ms
* the higher, the better user feel
