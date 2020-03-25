#

## Review

Avoid using code in the JSP such as: `${x}` to take a user's input because their input could contain HTML and that would be a cross-site inscription attack.

For the JSP equivalent of `if else` statements in java:

```JSP
<c: choose>
    <c:when test="${x % 15 == 0}"> // if
        fizz // then
    </c:when>
    <c:when test="${x % 3 == 0}"> // else if
        <span class="red">buzz</span> // then
        // see span definition below
    <c:otherwise> // else
        buzz
    </c:otherwise>
</c:choose>
```

*Span:* spans are inline tags that wrap text to apply to the text within them. If you only want one word in a sentence to be red, for example,

If you only want to check one condition:

```JSP
<c:if test = "${salary > 2000}">
    <p>My salary is: <c:out value = "${salary}"/><p>
</c:if>
```

A `for` loop in java:

```java
for (int x = 0; x < 50; x++>) {
    // some code that will loop through 0-49
}
```

The equivalent in jsp:

```jsp
<c:forEach begin="0" end="49" var="x" step="1">
    // some code
</c:forEach>
```

## Scriplets

*Scriplets:* scriplets are a way to insert java code into a jsp document. Don't use scriplets!!

You can use your java code in the java file itself... and then just call it in the jsp doc rather than using scriplets to write it there.

NOTE: If a scriplet starts with <%a>, that's totally fine.

## Scopes

*Scopes:* scopes are maps of variables(?). They are cookies.

Order of scopes:
1) page
2) request
3) session
4) server

WHat is stored in session scopes:
- id of a user's particular row for a game in the session so you don't have to go look it up every time
- a user's current position on a game board for a current session so you don't have to look it up every time
- login info to make sure the user is logged in the entire time they're using the application

With session scope, the server has to make space for every single user logged in for the entire duration they're on the page. This can take up a *lot* of space, especially if a ton of users are logged in, 
- an example of small storage would be their username and email address so you don't have to reach out to a database to grab the values every time

Page scope is only used for the current page. It's for the duration of a single JSP file while you're using it. If you load another JSP file, you don't have any access to the variables from other JSP variables.

Request scope maps can be used in any JSP file or java file until the server responds to the user; then it's gone. It is used if you are referencing multiple JSPs in the same page.

NOTE: Most of the time, we'll be working with page scopes and session scopes. Very rarely will we need to store something in a request scope.

 Server scope maps last for as long as the application is running.

A variable with a page scope only exists as long as the page is running.

What happens if I put the same variable in different scopes?
- If I declare the variable in the page scope and in the session scope, it does *not* If I map a variable in the page scope, it will just build on each other. The jsp will check if a variable is in the page scope. If it finds it, that's the value it will use and it will stop. If it doesn't find it, it would check the request scope. If it's there, it would use it and stop. If not, it goes onto the session scope.

If you want to specifically choose which scope it should use:

```jsp
<c:set var="myPageVar" value="Larry" scope="page" />
    <c:set var="myRequestVar" value="Curly" scope="request" />
	<c:set var="mySessionVar" value="Moe" scope="session" />
		
	<ul>
    <li>Value of <em>pageScope.myPageVar</em> is: <b>${pageScope.myPageVar}</b></li>
    <li>Value of <em>requestScope.myRequestVar</em> is: <b>${requestScope.myRequestVar}</b></li>
    <li>Value of <em>sessionScope.mySessionVar</em> is: <b>${sessionScope.mySessionVar}</b></li>
</ul>
```

In simpler terms:

```jsp
${x} // checks every scope and stops after it finds it
${<scope>.x} // list the scope you want and it will
// only check that scope for x
{sessionScope.x} // specifically checks the sessionScope
```

If you have the same variable in different scopes, it wil always use the value of the first one it finds:

```jsp
<li>Valuie of ambiguous var from <em>page</em> is: <b>${
    pageScope.anAmbiguousVar}</b></li>
}
```

## EL

In ELs, we can access both lists and arrays by using bracket notations:

```jsp
<c:set var="stringList" value="${['Three', 'Blind', 'Mice']}" />
// we are declaring a string list

    <p>Array elements are referenced in JSP EL in the same way as Java. 
    However, one difference is that Lists can also be referenced 
    using the same syntax as arrays</p>
    <ul>
        <li><em>stringList[2]</em> is <b>${stringList[2]}</b></li>
        // this is pretty "mice"
    </ul> 
```

## String Maps in JSP EL

You can use maps in JSP EL too, but only string maps. It's important to note that you *must* match the 

You cannot call any methods in EL. The ONLY thing you can access from EL is getters and booleans. There's no `get` word:

```jsp
<p>The Mustang is made by <b>${model2Manufacturer.Mustang}</b>.</p>
// this is printing the value of the key "Mustang"
// note that you *must* use dot notation
```

## Java Beans

Java beans are just java classes with very particular restrictions. It's just a class in which the conditions are true:
- they are serialized

*Serialization:* the process of turning an object (or data) from one format into another while preserving the structural information (i.e. can be reserved).
- If I'm serializing a java object or data, I'm likely turning it into a String/JSON. That's a really common serialization. If I print a java object as a String, it'll print the hash code, which can't be reversed. That's the point of serialization; you *can* reserve it.
- Turning java objects into database rows; we call it mapping, but it's really serialization.

In order for a java object to be serialized (java beans):
- it must have a constructor that doesn't take any arguments
  - however, you *can* have an additional constructor that takes parameters; you just can't use it
  - the object is still a bean because it still has another constructor with no parameters
- you must be able to access *all* of the data in the object via getters
- you must be able to store *all* of the data in the object via setters
- you cannot have private variables that are not accessible via getters/setters

NOTE: serialization does not mean you cannot have derived property. As a reminder, a derived property is a property that is generated using other members of the object. BUT, you sti
- Ex: If you have a database connection within an object, you cannot serialize it. You cannot turn a database into a String.
- if you serialize an object, you should be able to de-serialize it and have it have the exact same values

You can have methods attached to a java bean object as long as the method doesn't depend on data that can't be serialized.

## Accessing JSPs from Java Files

```java
public class NameServlet extends HttpServlet {

	@Override
	protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        // here, just like normal, we are adding
        // items to a list in the java file
		List<String> names = new ArrayList<String>();
		names.add("AndrÃ©");
		names.add("Matt");
		names.add("Vineeta");
		names.add("Diane");
		names.add("Apple");
		names.add("Leon");
		names.add("C.J.");

        /* This line adds a request attribute with the name "nameList" that contains our list of student names
        in the JSP file linked below.
        This will later be used by the View (i.e. JSP) to 
        display student names in HTML */
		req.setAttribute("nameList", names);

		/* This line forwards the request to the JSP */
		this.getServletContext().getRequestDispatcher("/WEB-INF/nameList.jsp").forward(req, resp);
	}
}
```

Here, we're accessing the `WEB-INF/nameList.jsp` file that is stored in the same directory as our java file.

In the below code, it's important to note that there won't be a compiler error if you list incompatible data types. When we use `items`, we must use an `array` or `list`. If we use a String, we're going to get some weird behaviors. This code is 

```jsp
<c:forEach var="name" items="${requestScope.nameList}">
    <li>${name}</li>
</c:forEach>
```

## Retrieving Values from Java Beans Objects Within JSP

Trim off the *getter* part, or the *is* part of the object
you're from which you're retrieving values:

```jsp
<c:forEach var="person" items="${personList}">
    <tr>
        <td><c:out value="${person.firstName}"</td>
        // this is a better way to get values so 
        // you aren't at risk for an injection attack
        <td>${person.lastName}</td>
        // although the methos is "getLastName",
        // you drop the "get" and just list the
        // variable name since you can *only*
        // call getters, so there's no need
        // to state "get"
        <td>${person.age}</td>
        <td>${person.adult}</td>
    </tr>
</c:forEach>
```