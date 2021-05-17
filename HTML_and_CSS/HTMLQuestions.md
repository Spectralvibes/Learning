# What is web storage API?
- Storage objects
Storage objects are simple key-value stores, similar to objects, but they stay intact through page loads. The keys and the values are always strings (note that, as with objects, integer keys will be automatically converted to strings). You can access these values like an object, or with the `Storage.getItem()` and `Storage.setItem()` methods. These three lines all set the colorSetting entry in the same way:
```javascript
localStorage.colorSetting = '#a4509b';
localStorage['colorSetting'] = '#a4509b';
localStorage.setItem('colorSetting', '#a4509b');
```
> Note: It's recommended to use the Web Storage API (`setItem`, `getItem`, `removeItem`, `key`, `length`) to prevent the pitfallsassociated with using plain objects as key-value stores.
- It should be noted that data stored in either localStorage or sessionStorage is specific to the protocol of the page.
- The keys and the values are always strings (note that, as with objects, integer keys will be automatically converted to strings).
The two mechanisms within Web Storage are as follows:
- **sessionStorage** maintains a separate storage area for each given origin that's available for the duration of the page session (aslong as the browser is open, including page reloads and restores).
- **localStorage** does the same thing, but persists even when the browser is closed and reopened.

```javascript
// Save data to sessionStorage
sessionStorage.setItem('key', 'value');
// Get saved data from sessionStorage
var data = sessionStorage.getItem('key');
// Remove saved data from localStorage
localStorage.removeItem('key');
// Remove all saved data from sessionStorage
sessionStorage.clear();
```
[More...](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API)


# What are cookies?
An HTTP cookie (also called web cookie, Internet cookie, browser cookie, or simply cookie) is a small piece of data sent from a website and stored on the user's computer by the user's web browser while the user is browsing.
[More...](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)


# What is canvas in HTML5?
- The HTML `<canvas>` element provides an empty graphic zone on which specific JavaScript APIs can draw (such as Canvas 2D or WebGL). 
[More...](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Basic_usage)
________________________________________________________________________________________________________________________________________


# What is SVG?
- Scalable Vector Graphics (SVG) is a 2D vector image format based on an XML syntax.
- Based on an XML syntax, SVG can be styled with CSS and made interactive using JavaScript. HTML5 now allows direct embedding of SVGtags in an HTML document.

SVG has some advantages over conventional bitmapped graphics, such as JPEG, GIF, and PNG, used in the browser environment, because ofseveral reasons:
- The files are generally much smaller than bitmaps, resulting in quicker download times.
- The graphics can be scaled to fit different display devices without the pixelation associated with enlarging bitmaps.
- The graphics are constructed within the browser, reducing the server load and network response time generally associated with webimagery. 

That is, a typically small formulaic description is sent from the server to the client. The client then reconstructs theimagery based on the formulas it receives.
- The end-user can interact with and change the graphics without need for complex and costly client-server communications.
- It provides native support for SMIL (Synchronized Media Integration Language) meaning that animations, for example, are supported witha more analog notion of timing, hence freeing the programmer from timed loops typically used in JavaScript-based animations.
- It responds to JavaScript: the same scripting language used in the HTML environment. This means the two types of documents mayconverse, share information and modify one another.

SVG is an XML language. This is important for at least three reasons. First, the code tends to adhere to agreed upon standards of howSVG should be written and how client software should respond. Second, like all XML, it is written in text, and can generally be read notonly by machines but also by humans. Third, and perhaps most importantly, JavaScript can be used to manipulate both the objects and theDocument Object Model, in ways quite similar to how JavaScript is used in conjunction with HTML. If you already know how to useJavaScript and HTML for web-programming, the learning curve will be pretty gentle, particularly in view of the benefits to be gained.
> [More...](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial)


# What is IndexDB?
IndexedDB is a way for you to persistently store data inside a user's browser. Because it lets you create web applications with rich query abilities regardless of network availability, your applications can work both online and offline.
- Basic pattern
	The basic pattern that IndexedDB encourages is the following:
	- Open a database.
	- Create an object store in the database. 
	- Start a transaction and make a request to do some database operation, like adding or retrieving data.
	- Wait for the operation to complete by listening to the right kind of DOM event.
	- Do something with the results (which can be found on the request object).
	- With these big concepts under our belts, we can get to more concrete stuff.
> [More...](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)


# What is WebSQL?
Web SQL Database is a web page API for storing data in databases that can be queried using a variant of SQL.
> Note: Web SQL was deprecated because standards are really important and turning Web SQL into a proper standard would have been prohibitively difficult.


# What is Cache API?
The Cache interface provides a storage mechanism for Request / Response object pairs that are cached.
> [More...](https://developer.mozilla.org/en-US/docs/Web/API/Cache)


# What are semantic tags in HTML5?	
Semantic tags allowing you to describe more precisely what your content is.
- **Sections and outlines in HTML5**: A look at the new outlining and sectioning elements in HTML5: `<section>`, `<article>`, `<nav>`, `<header>`, `<footer>` and `<aside>`.
- **New semantic elements**: Beside sections, media and forms elements, there are numerous new elements, like `<mark>`, `<figure>`, `<figcaption>`, `<data>`, `<time>`, `<output>`, `<progress>`, or `<meter>` and `<main>` 
- ** Using HTML5 audio and video **: The `<audio>` and `<video>` elements embed and allow the manipulation of new multimedia content.
> [More...](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5)


# What's the difference between an "attribute" and a "property"?


# What are custom attributes in HTML5?
- The data-* attributes is used to store custom data private to the page or application.
- The data-* attributes gives us the ability to embed custom data attributes on all HTML elements.
- The stored (custom) data can then be used in the page's JavaScript to create a more engaging user experience (without any Ajax calls or server-side database queries).
- The data-* attributes consist of two parts:
	- The attribute name should not contain any uppercase letters, and must be at least one character long after the prefix "data-"
	- The attribute value can be any string
	
> Note: Custom attributes prefixed with "data-" will be completely ignored by the user agent.

All such custom data are available via the HTMLElement interface of the element the attribute is set on. The HTMLElement.dataset property gives access to them.


# What are web sockets?
The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.


# What are media elements in HTML5?
- [`<audio>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)
The  `<audio>`  element is used to play audio in a Web context. These can be used invisibly as a destination for more complex media, or with visible controls for user-controlled playback of audio files. Accessible from JavaScript as  HTMLAudioElement objects.

- [`<video>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video)
The  `<video>`  element is an endpoint for video content in a Web context. It can be used to simply present video files, or as a destination for streamed video content.  `<video>`  can also be used as a way to link media APIs with other HTML and DOM technologies, including  `<canvas>` (for frame grabbing and manipulation), for example. Accessible from JavaScript as HTMLVideoElement objects.

- [`<track>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/track")
The HTML  `<track>`  element can be placed within an  `<audio>`  or  `<video>` element to provide a reference to a  WebVTT format subtitle or caption track to be used when playing the media. Accessible from JavaScript as HTMLTrackElement objects.

- [`<source>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/source)
The HTML  `<source>`  element is used within an  `<audio>`  or  `<video>`  element to specify source media to present. Multiple sources can be used to provide the media in different formats, sizes, or resolutions. Accessible from JavaScript as  HTMLSourceElement objects.


# What is doctype (different types of Doctypes)?
When authoring document is HTML or XHTML, it is important to [Add a Doctype declaration](http://www.w3.org/QA/Tips/Doctype). This makes sure the document will be parsed the same way by different browsers.
	
The simplest and most reliable doctype declaration to use is the one defined in  [HTML5](https://www.w3.org/TR/html5):
```html
<!DOCTYPE html>
```
There are many other declaration types which can be used in HTML document depending on what version of HTML is being used.
HTML 4.01 has 3 possible doctypes − HTML 4 Strict, HTML 4 Transitional, and HTML 4 Frameset. Every HTML document you create should have one of these three DTDs.
- HTML 4 Strict
This document type includes all HTML elements except those that have been deprecated, and those that appear in frameset documents.
```html
<!DOCTYPE 	HTML 
			PUBLIC 
			"-//W3C//DTD HTML 4.01//EN" 
			"http://www.w3.org/TR/html4/strict.dtd">
```
- HTML 4 Transitional
This document type includes all HTML elements including those that have been deprecated.
```html
<!DOCTYPE 	HTML 
			PUBLIC 
			"-//W3C//DTD HTML 4.01 Transitional//EN"
			"http://www.w3.org/TR/html4/loose.dtd">;
```
- HTML 4 Frameset
This document type includes all HTML elements in the transitional DTD as well as those in framed document.
```html
<!DOCTYPE 	HTML 
			PUBLIC 
			"-//W3C//DTD HTML 4.01 Frameset//EN"
	   		"http://www.w3.org/TR/html4/frameset.dtd">
```
[More...](https://www.w3.org/QA/2002/04/valid-dtd-list.html)


#  What is metadata tag?


# What Would Happen If The HTML Document Does Not Contain `<!DOCTYPE>`?
- It instructs the Web Browser about the version of HTML used for creating the Web page.
- If the developer misses declaring the DOCTYPE information in the code, then new features and tags provided by HTML5, like `<article>`, `<footer>`, and `<header>` will not be supported. Additionally, the Browser may automatically go into Quirks or Strict Mode.


# What is iframe tag?
- The HTML Inline Frame element `<iframe>` represents a nested browsing context, embedding another HTML page into the current one.
- Each embedded browsing context has its own session history and document. The browsing context that embeds the others is called the parent browsing context. The topmost browsing context — the one with no parent — is usually the browser window, represented by the Window object.	
> [More...](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)


# What are List elements in HTML5
HTML offers web authors three ways for specifying lists of information. All lists must contain one or more list elements. Lists may contain:
- `<ul>`: An unordered list. This will list items using plain bullets.
- `<ol>`: An ordered list. This will use different schemes of numbers to list your items.
- `<dl>`: A definition list. This arranges your items in the same way as they are arranged in a dictionary.


# What are the features provided by HTML5?
HTML5 introduces a number of new elements and attributes that help in building an attractive webSite, that we see nowadays.
It supports following new features.
1. New Semantic Elements – These are like `<header>`, `<footer>`, and `<section>`.
2. Forms 2.0 – It contains improvements to HTML web forms. It has introduced new attributes for the `<input>` tag.
3. Persistent Local Storage – With HTML5, it is possible to achieve this, without resorting to third-party plugins.
4. WebSocket – It facilitates setting up a bidirectional communication for web applications.
5. Server-Sent Events(SSE) – These events got introduced in HTML5. The direction of the flow of the execution of these events is from the server to the Web Browser.
6. Canvas – It supports a two-dimensional drawing surface that is programmable using JavaScript.
7. Audio & Video – It allows embedding audio or video on the web pages without resorting to third-party plugins.
8. Geolocation – It facilitates the visitors to share their physical location with the web application.
9. Microdata – It allows building our personal vocabulary beyond HTML5 and extends our web pages with those custom semantics.
10. Drag and drop – It supports to Drag and drop the items from one location to another location on the same Web page.


# What are new form elements in HTML5?
- `<datalist>`: Specifies a list of pre-defined options for input controls
- `<output>`: Defines the result of a calculation


# Which elements of HTML 4.01 are no more a part of HTML5?


# HTML5 drag and drop feature?


# What are new HTML5 types?


# What are web workers?
Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.
> [More...](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)


# Geolocation API in HTML5?


# Difference between attribute and property?


# What UI, Security, Performance, SEO, Maintainability or Technology considerations do you make while building a web application or site?


# How many resources will a browser download from a given domain at a time?


# Name 3 ways to decrease page load (perceived or actual load time).


# Explain some of the pros and cons for CSS animations versus JavaScript animations.


# What does CORS stand for and what issue does it address?


# What's the difference between full standards mode, almost standards mode and quirks mode?


# Describe the difference between `<script>`, `<script async>` and `<script defer>`.


#  What is progressive rendering?
