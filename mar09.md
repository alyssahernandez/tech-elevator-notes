# Networks, URLs & Basic HTML/CSS

*HTTP:* hypertext transfer protocol

*HTML:* text that follows a specific structure; no different than doing a console in/out, except the browsers know how to render/print the text in a specific way into graphics

*Server:* a server is just a computer on which data is stored. Once a user quits their session on a website/web application, the server flushes the memory, which allows the server to handle thousands and thousands of requests.
- The server doesn't chat back and forth with the user; there's no back and forth chitter chatter. The server takes information from your request and gives you what you need, and then flushes the memory.
- If a server had to remember all of the people it's communicating with--imagine if you leave a website up and you're gone for an hour--the server would fill up very quickly and the website would be extremely slow.

*Webserver:* a software program that handles web requests. It's different than a web application. It can handle returning plain HTML files. When a request goes from the laptop to the server, we don't want every application to deal with ports, networking, etc, so there are webservers out there that handle that low-level stuff for us. Exists in part to load plain files, but also hosts your web applications.
- Tomcat : Java
- Kestrel : .NET Core
- IIS : Microsoft Intermit Information System
- Apache : open-source
- Nginx : Open-source C-based server

*Cloud:* "cloud-computing" is really just storing your data on someone elses computer
- Google Drive's cloud storage is really just stored on Google's computers

*Front-end developer:* a programmer who writes code to be displayed on someone elses computer; it lives on the user's device
- no longer have control over the device the user is using
- programmers typically have high quality computers, so it's a good idea to keep junk laptops around to test your software on a lower quality model

*Back-end developer:* works on the code the user doesn't see; the database, server on which the website is hosted, etc.

*Browser:* effectively reads a text document that has a particular shape--HTML--and knows how to translate it into something visual.

## Web Application vs Website

HTML and CSS files can be served on a server somewhere and open in a web browser; they can be local.

Websites are dynamic applications through which a user is sending a request to your server to --. The server runs code on its side--java, python, etc. There is also a database server; the database server and regular server work together to process requests sent by the user.

In our class, our database server and our web server are both stored on our local computer. The webserver we're using is Tomcat--a Java webserver.

A website is pretty static; it's just returning a page of text that is pre-rendered. Sure, there has to be *some* code that runs in the backend, but it's pre-rendered. In a web application, there's code that runs between your request to the server and the content you get back.

## Backend vs Frontend

Backend:
- Server
- Webserver
- Database
- Java
- Spring MVC
- JSP/JSTL

Frontend (Client):
- HTML
- CSS
- Javascript

## Breaking Down a URL

http://www.techelevator.com/foo?name=Andrew&last=McGuier

*Protocol (**http://**):* how we tell the server we want it to respond to us
- "I want you to respond to me via an HTML request"
- *https:* does the same thing but it's encrypted
- the double slash (**://**) separtes the protocol from the domain name (it's part of the protocol)

*Subdomain (**www.**):* there can be multiple ones; anything before the main domain

*Main domain name (**techelevator**):* 

*Top-level domain (**.com**):* an organization that is managing **all** of the domain names
- the dot (**.**) separates the domain name from the TLD (it's part of the TLD)
- there is one big organization that owns all of the `.com` domains
- technically, main domains are just delegations of top-level domains
  - Apple owns `.app`
  - Google owns `.dev`
  - the US owns `.com`
  - Lybia owns `.ly`
- every country has its own `ican`/TLD that is specific to their country
  - because these domains are owned by specific countries, they have full control over those and could technically say they own all of the websites/organizations/startups that use their TTDs
  - there are a lot of politics surrounding TTDs; let's say there's a new TTD that comes out... corporations may have to purchase the new domain to maintain their brand
  - *Squatting:* you purchase a domain name with a newer TLD that is the same as a large organization's domain name; you purchase it and force the organization to purchase it from you from millions/billions of dollars
 
 *Path/resource (**foo**):* always starts with the slash

 *Query string(**?name=Andrew&last=McGquier**):* a way we can pass parameters to a page
 - with Java, we declared parameters by stating the data type and then the value of it
 - with URLs, we always start with a single question mark and then pass in *variable name equals* and then pass in the value

*#:* used for anchor tags on the page
- if we want to put a tag halfway down the page, we can do that with a hash mark

## HTML / CSS

*HTML:* hypertext markup language; the content of the page -- the **what**

*CSS:* cascading stylesheet -- how the content is displayed on the page

Three ways to style an HTML page ordered from best practice to worst:
- link to an external stylesheet
  - `<link href="style.css" rel="stylesheet">`
- style block at the top of a the HTML document
  - `<style> . . . </style>`
- within an element
  - `<div some style stuff... > ... </div>`

Because there are three different ways to style an HTML document, all three work together to style your document. This is where the term *cascading* comes into play. First, the external stylesheet is applied to the document. Then, the style block at the top of the HTML document is applied. Finally, the styling within an element is applied. Typically the rule is: **last one within wins.** The in-element styling is also directly applied to one specific element, so it overrides the other ones that are more general. If there are four classes in a row for example, that all apply to the same elements, the most recent one will override the other ones if the other ones have the same styling (such as `background-color`).

## Selectors

*Selectors:* they specify which element the following style block will apply to.

`*`: universal selector; applies to everything

`div` / `p` / `section`: element selector; you list the name of the element you want the styling to apply to. it matches any element/tag on the page with that name and applies to it, and overrides the universal selector
- if i want to apply a purple background to all of the `div` elements:
  
```CSS
div {
    display: block;
    background-color: purple;
}
```

`.class`: class selector; overwhelmingly the most important selector. it won't actually say `class` because you name the class within your elements. within an element, if you put `class="foo"` in a few elements (without the period), every one of those elements would have the following code applied to it. make sure you don't include spaces in the names either, as that would just give it additional classes rather than linking them altogether.

```CSS
.foo {
    background-color: blue;
}
```

`#id`: ID selector; very specific and almost the same as using in-element styling. if you put an `#id` on an element, you *cannot* repeat it because it must be unique. it basically just keeps your HTML document clean by avoiding in-line attributes. another benefit to using an ID selector is that it makes it easier to find a specific element with an HTML document rather than having to manually read through the document. **IDs rank higher than classes.** just**** like classes, you do not include `#` when you are declaring it within an element: `(<div id="idExample"> . . . /div>)`:

```CSS
#id {
    background-color: green;
}
```

## Combining Selectors

*Multi-rule selectors:* if you use periods within your stylesheet to connect multiple selectors, the styling would only apply to elements that have both of those selectors: `section.foo`

*Descendant selectors:* if you use spaces in ur elements, the styling will search for the first selector listed and then apply the actual styling to whatever is **nested** within that selector as the second selector listed: `body .foo` will only apply the styling to `.foo` elements with the `body`

## The Box-Model

Elements in CSS are laid out according to the box-model. An element in CSS renders as an invisible box, and there are various sections within that box:
- margin // space outside of the content
- border // border around the content
- padding // space between the border and the content
- content // content...

## Display Property

*Block:* sections, divs, paragraphs--things that should follow each other on the page--these all display as blocks by default. Block-type elements create a new line in the display and take up as much width in the browser as they can based on their settings. They always bump down to another line; you will never have two block elements on the same line. You can, however, with certain display types, manually set the height and width of an element.

*Inline:* anchor tags, links, span tags, images--these are elements that are inline by default. Inline elements do not start a new line; they conform to the size of their content. You **cannot** specify a specific height/width; they're kind of meant to behave as text.

*Inline-block:* these elements do not force elements on a new line and they still take up the minimum width, but they can have height/width set on them. 
- these are useful because with inline elements, you can't set a height or width, but let's say you want block elements on the same line--you can still set their height and width.

*None:* Basically says "don't display this element at all"; makes the element invisible.

## Position

Every element has a display and a position. If we don't specify a position, the browsers display the elements as static by default.

*Static positioning:* the default positioning
- usually you want everything static (most of the time)

*Relative positioning:* tells the browser to render the page as you want, but the element should still take up the same amount as its original space; but you can specify how many pixels to move it by--10px towards the top, 50px to the right, etc
- you can move it to move an image into a corner, for example
- it's still taking up its original space; other elements act as if the element is still in its original place
- you want to avoid this because changing the element it's relative to will cause a lot of problems; you may have to make those elements relative then and change all of the styling, etc

*Absolute positioning:* makes the element relative to its container
- doing this yanks the element out of its original position so the other elements act as if it isn't there
- it's similar to relative positioning in that you can specify the number of pixels to move it to certain directions

*Fixed positioning:* the element is taken entirely out of the flow and is positioned relative to the entire browser window
- the element doesn't move as you scroll through the page
- it basically gives it a permanent position on the screen
- an example of this would be a menu bar at the top of a website