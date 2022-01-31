# Network Performance
Network latency comes from request sent through the wire. There are two main factor that help you maximize the network performance and they can be done rather easily.
  
## Minimize Files
Minimizing files reduces the amount of shit you send throught the wire thus improving latency and in turn performance. You'll wantr to  reduce your text files and your media files.
### Reducing text files
  In order to reduce your text files namely JS, HTML and CSS, you can run them trhough a minifier like uglify. This gets rid of all the unnesessary extra whitespace needed for humans 
  to read and understand the code better. By doing this you can greatly reduce the sice of text files thus improving network request performance.
### Reducing Image files
The primary way to change an image size is to change the file format. Thus, you have to pick the file format that is correct for the job and crompress them as much as possible without
minimizing ther quality. You have to explore the pros and cons
of using
- **JPEG** -> used for complex images that contain many colors, like photographs. They dont allow for transparency, they tend to be big in file size.
- **PNG** -> limit the number of colors used, and tend to be smaller than JPES. They allow transparency, ussualy employed with logos.
- **SVG** -> vector graphics. You can expand svgs without quality loss and are quite small for they're quality. Can be modified with css. They tend to be simplistic, with few colors
like icons and such.
- **GIFs** -> limit the colors that are display between 2-256. Reduced color coun leads to huge file savings but the quality is not always the best on complex scenarios.
  
#### Help deciding between file formats
  - If you want transparency: jpeg
  - If you want animation: gif
  - If you want colorfoul images: jpeg
  - If you want simple icons, logos, and illustrations: svg
    
#### Compression Tools and tips
There's propably tools that can achieve this programatically (maybe webpack) but here are some online tools to use for simple stuff.
- Reduce PNG with [TinyPNG](https://tinypng.com/)
- Reduce JPEG with [JPEGOptimizer](https://imageoptimizer.cc/en/jpeg-optimizer)
  - Always reduce jpeg img quality 30-60% with things like photoshop (save quality)
- Remove image metadata with [verexif](https://www.verexif.com/en/)
- Use CDNs like [imgix](https://imgix.com/)
- Try to choose simple illustrations over highly detailed photos
- Resize img based on the screen size it will be displayed with ***media queries***
- Also use mediaqueries for backgrounds images.
  
## Delivery Optimizations
Reducing the number of components that a page needs to load will in turn reduce the http request needed to load the page. Thus, it's also important reducing the transfer frequency by structuring content efficiently (not by ommiting content) to improve website performance.
I.E: Using bundlers like ***webpack*** and ***parcel***.

 
Consider using native alternatives to libaries in order to reduce data transfer. If you determine that a libary is absolutely necesary, consider using ones that are lightweight if there is one abailable. 

Browser's have a limited number of files they can fetch at a time, so it's not an option just getting all the files at once, not to mention that would greatly hinder performance. More info on [browser Limits](https://stackoverflow.com/questions/985431/max-parallel-http-connections-in-a-browser).