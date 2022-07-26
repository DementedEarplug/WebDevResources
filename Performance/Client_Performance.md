# Client Side optimizations (front-end)
In order to perform client side optimizations we need to have some understanding of how the DOM is formed. Once we have the HTML client reads the file in order and stops to fetch files that it needs to render something, be it js, css, or images. This might cause a bottleneck if the files being fetched are not being used right away. Thus is necesarry to learn about the critical render path.

## Critical Render Path
DOM (HTML) -> CSSOM (CSS) ->[[DOM CONTENT LOADED]] Render Tree -> Layout -> Paint [[Loaded]]
CRP quick optimizations [HTML(1-2), CSS(3-6), JS(7-10)]:
1. Always put CSS tags at the top of the html (bottom of the head tag).
2. Always put JS tags at the end of the HTML file (just at the top of the closing body tag).
3. Load only what you need.
4. Above the fold loading (load only what is visible, and the rest as it becomes vissible).
5. Media attributes (Load styles according to media attributes).
6. Use less specificity in css names, takes less work to build the CSSOM.
7. Load scripts asynchronously.
8. Defer loading of scripts.
9. Minimize DOM manipulation.
10. Avoid long running scripts.

CSS is Render Blocking. 

JS is Parser blocking.
![script tags execution within critical render path](https://i.stack.imgur.com/wfL82.png)
- `<script>` - blocks html parsing while it downloads and executes scripts. There are critical app scripts and above the fold scripts.
- `<script async>` - downloads the script without blocking html parsing. However there is a caveat, the script can execute at any time (long after the page actualy loads, before the page finishes loading). Use async in scripts that do not affect the DOM. Use it in scripts that require no knowledge of our code and arent essential to UX. I.e Tracking script, Analytics scripts. Third party scripts that dont affect DOM.
- `<script defer>` - does not block loading of the page while downloading scrip. Waits until the html finished loading to execute the script and it executes in order of appearance. Its good for scripts that manipulate the DOM/Render tree, and are not needed for above the fold loading. Third party scripts that arent critical and arent above the fold.



## Optimizing Code 
In order to deliver a performant webapp, you need to ensure your JS code is optimized in order to  achieve a fast *time to first meaningful paint* and *time to intetactive*. You also need to improve the execution of the JS once its on the page.
### Delivering JS files on the most efficeient way possible
Use codesplitting (progressive bootstraping) reduce the ammount of work being done during execution time by breaking down your JS and sending only what is needed for a page to run. Basically, send the necessary JS to load the home page, and lazy load the rest of the JS as you visit the pages that use it. You can also lazy load components that are not in the view and load the JS when an event triggers the component.

### Sumary
- Only load whats needed (codesplitting, treeshaking)
- Avoid blocking main thread
- Avoid memory leaks
- Avoid multiple re-rendering


## PWAs (TBD after react)
