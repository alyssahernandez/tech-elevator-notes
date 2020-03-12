# Java MVC

## Review from HTML/CSS

Avoid using `grid-template-rows` (use `grid-template-columns` instead) and `order`. Screen readers read the page from top to bottom, so changing the order via CSS will affect the order in which it reads.

An element can be placed in a grid area called `content` using which rule? `grid-area: content;`. The value will always be something that matches the `grid-template-area` value assigned as well. The names are arbitrary. A template area is just a way to define the layout for a set of rows.

## Request and Response Flow for a Java Servlet

**Note: Most of the employers though Tech Elevator use the Java MVC framework.**

First, a user sends a request to the web server. Basically, you're requesting access to what's at the root of the server. The request always starts with sending a series of text to the server defining the length of the request, the "language" it's speaking (HTTP protocol 1), the compression, the headings, etc. Our server, in this course, is Tomcat. Tomcat will read all of the text and generate a request object in Java and hand it off to our web app depending on the structure of the URL (defined above), which then looks internally and sees "okay what route do I have that can handle this. That is the `get request` sent to the server and then Java. Our web app container is a Java program we create that is stored in Tomcat. If Tomcat doesn't find it, you will get a 404 error. Note: Tomcat is actually written in Java itself, but you don't *have* to use Tomcat as your web server; there are other Java webservers that aren't written in Java.

1) Your laptop sends a request to a web server app/software (such as Tomcat), but it is on a physical web sever. Everything from there on is backend.
2) The web server sends a `get request` to a web app container
3) The web app container sends a `get request` to your servlet, which is where your java code is stored
4) The response content is sent from the servlet back to the web app container
5) The response content is sent from the web app container to the web server app
6) The response content is sent from the web server app back to your laptop

The web app container determines which servlet to use depending on the URL structure path. Typically, one servlet takes in one request. We may have a bunch of servlets, but the web app container determines which servlet is used.

The virtual machine--the Java virtual machine is a good example of that--is a digital representation of a physical machine. If I have a Mac but I want to run Windows, I could run the entire Windows OS on a virtual machine; which acts like a computer. The virtual machine cannot see the content of the physical machine and vice versa. Because virtual machines exist now, the model of today has become to just pay a company to use one of their virtual machines. There about four or five major ones and they're typically open-source. Even in the early 2000s, you basically had to run multiple apps on one server, whereas now, you just run your apps on individual VMs.

A servlet can handle one HTTP request.

There is a directory where Tomcat stores all of the web apps, which contains a bunch of compiled code. It looks for our code in a particular place in there and then determines which servlet to use.

## Navigating a Web App Folder

First, go to the `WEB-INFO` FOLDER AND FINE THE `web.xml` file to see what the app is composed of. Make sure you're on the `Source` view instead of `Design` to view a list of the servlets. Basically, the `web.xml` file takes a URL and matches it to a servlet. 

A server is just a Java class, just like every other java class we've written, but it inherits from the HTTP servlet. In the configuration file (`web.xml`), which just saying point me to a java class that runs this servlet. HTTP servlet is built into java to handle web requests:

`public class HelloServlet extends HttpServlet {`

## MVC

*MVC:* model view controller:

1) Our laptop sends a request.
2) Tomcat handles the route (URL)
3) The request is dispatched to the controller; its job is to take the parts of the request (rips it apart) it needs to communicate with the model using the parameters to call a model method (`DAOUsers.getUserProfileFromUsername`)
   1) For now, let's think of servlet as the controller
4) The model reaches out to the database and turns the requested value into a java object
   1) You should not use the controller to communicate with the database
5) The model sends the object back to the controller
6) The controller then takes the object and sends it to the view/framework
   1) JSPs are a view for doing server-side pages in Java
7) The view sends what the user will see back to the user's laptop
   1) Note: Languages and frameworks differ in this step. Sometimes the controller will send it back to the user's screen
   2) You should not be doing application logic here
   3) The view should be concerned with taking java objects and turning them into something visible

Simplified:

1) Request to Tomcat to handle the URL/route
2) Tomcat sends the request via a specific route to the controller
3) The controller rips apart the request and calls a method from the model based on the URL
4) The model executes the method and pulls values from the database to render them as java objects
5) The model sends the object back to the controller
6) The controller sends the objects to the view
7) The view configures what the user will see & sends it to them

NOTE: The view *also* takes input from the user. The user interacts with the view; not the controller.