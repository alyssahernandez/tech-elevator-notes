# Shared Layout Pages, Partial Views & Dynamic Links

**NOTE: "mocking" is the technique we need to use to generate fake data into our trivial pursuit page**

## Principles to Follow for Programming Principles & Building Webpages

*DRY:* don't repeat yourself
- don't write code twice/multiple times
- write methods with parameters

*YAGNI:* you ain't gonna repeat yourself
- yes, it's good to not repeat yourself, but sometimes if it's such a small thing to repeat, you'll spend way too much time trying to redo the logic
- avoid pre-optimization

## Pulling Data from a Database into JSP

```jsp
<c:forEach var="class" items="classes">
    <li class="${class}"> . . . </li>
</c:forEach>
```

****************************** I think `classes` is the name of the column in the database and `class` is ... ?******************************

## Layouts

*Layout:* a common layout that users view across a web app
- there's likely a consistent header, left nav/menu, content and footer

If multiple JSP files use HTML/CSS documents (which, obviously, they do), it's better to import the HTML/CSS files into *one* JSP file, and then import that partial JSP fragment into the other JSP files that need to use them.
- Headers and footers, for example, are usually consistent throughout the app. Rather than redefining them on every JSP/webpage, it's better to just import the header/footer JSP files in each JSP doc. The other JSP files that need them would define the content that goes in between them.

## Using the Core (c:) Library in Your JSP Files

In all of the JSP files we've worked with so far, most of the code we've been writing starts with `c:`. That is a JSTL library for *core*, which contains a list of available methods. We import it like this:

```jsp
<%@ taglib prefix="c"   uri="http://java.sun.com/jsp/jstl/core" %>
```

## Inserting Header/Footer Files into Another JSP File

The order in which you insert the JSP files matters. It will be wherever you placed them, so be aware of where that is in the JSP file you are inserting them.

The format for inserting the header/footer files (and any other JSP files you want to include):

```jsp
<%@ include file="common/header.jspf" %>
```

Notice that we don't have to type the entire path; these files share a folder so we only need to list the relative path.

## Controller File

The controller java file should just contain the `@RequestMapping` methods to return JSP files to the view
- this is how you get from a URL to a controller method, and then from a controller method to a view
- to request data for the view to view, we use the `setAttribute` method to "put" java data into a map that the view can access

```java
@RequestMapping("/forum")
public String showForumList(HttpServletRequest request) {
    request.setAttribute("topicList", forumDao.readAllTopics());
    return "forum/forumList";
}
```

In the above, we are creating a variable/key of `topic` and the key is an object. The "type-to-type" of the map is "string-to-object." It is calling a method from the `forumDao` java file that returns a *list* of all of the topics displayed on the page (this is the space geek or whatever page that has a list of 4 blog post links). The point is to render them into markup when the values are displayed on the webpage.

We can put lists, objects, strings, longs--anything we want--into the value section as long as **the keys are alphanumeric strings and the values are beans, strings, primitives or collections (maps, lists, etc).**

The corresponding JSP file to call that list:

```jsp
<ul>
	<c:forEach var="topic" items="${topicList}">
		<c:url var="forumPostHref" value="/forum/forumDetail">
            <c:param name="forumId">${topic.id}</c:param>
        </c:url>
		<li><a href="${forumPostHref}">${topic.title}</li>
	</c:forEach>
</ul>
```

## Declaring a URL for the Items in the List Above

In the above code, the `c:forEach` loop will loop through each item in the `topicList` defined in the controller java file. 

Remember: `topicList` is key we declared to access the list value. Just like in a regular `for each` loop, we define a variable name as one particular item in a list; here we call it `topic` (rightfully so, as we're looping through a list of topics). `items="${topicList}"` is calling the list, just like we need to do, again, in a java `for each` loop.

The `c:url` line, followed by the `c:param` line, is declaring what the URL for each topic would be. The shared portion of the URL across all topics (after the default prefix) is: */forum/forumDetail* The unique portion, for each topic, would be each list item's id.

Remember: each list item is an object, and the list item object in this case has an `id` attribute. So, here, we have the shared URL, followed by the item's ID. We get the topic/item's id by calling a getter method: `"${topic.id}"` and setting it equal to a parameter named `forumId`.

The line after that: `<li><a href="${forumPostHref}">${topic.title}</li>` puts it all together. So, when you're on the topics page and click on any individual topics, you'll navigate to that individual's topic page with the URL we defined above.


## Formatting a URL

`<c:url var="imageURL: value="/img/post-${topic.id}.jpg"/>`