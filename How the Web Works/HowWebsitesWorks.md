# How Websites Works

When you visit a website, your browser (like Safari or Google Chrome) makes a request to a web server asking for information about the page you're visiting. It will respond with data that your browser uses to show you the page; a web server is just a dedicated computer somewhere else in the world that handles your requests.

There is two major components that make up a website:

1. Front End (Client-Side) - the way your browser renders a website
2. Back end (Server-Side) - a server that processes your request and returns a response


## HTML (HyperText Markup Language)

Websites are primarly created using:

- HTML, to build websites and define their structure
- CSS, To make websites look pretty by adding styling options
- JavaScript, implement complex features on pages using interactivity

HTML is the language websites are written in. Elements (also known as tags) are the building blocks of HTML pages and tells the browser how to display content. 

The code snippet below shows a simple HTML document, the structure of which is the same for every website:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h1>Example Heading</h1>
    <p>Example paragraph.</p>
</body>
</html>
````

### HTML Structure Components

The `<!DOCTYPE html>` defines that the page is an HTML5 document. This helps with standardisation across different browsers and tells the browser to use HTML5 to interpret the page.

The `<html>` element is the root element of the HTML page, all other elements come after this element.

The `<head>` element contains information about the page (such as the page title).

The `<body>` element defines the HTML document's body. Only content inside the body is shown in the browser.

The `<h1>` element defines a large heading.

The `<p>` element defines a paragraph.

There are many other elements (tags) used for different purposes. For example, there are tags for buttons (`<button>`), images (`<img>`), lists, and much more.

### Attributes

Tags can contain attributes, which provide additional information about an element. For example, the class attribute can be used to style an element (e.g., make the text a different color):

``` 
<p class="bold-text">Text here</p>
```

The src attribute is used on images to specify the location of an image:

``` 
<img src="img/cat.jpg">
```

An element can have multiple attributes, each with its own purpose:
``` 
<p attribute1="value1" attribute2="value2">
```

### ID Attribute
Elements can also have an id attribute:

``` 
<p id="example">
```

The id is unique to that element. Unlike the class attribute, where multiple elements can use the same class, each element must have a different id to identify it uniquely.

Element ids are used for styling and for identifying elements with JavaScript.


## JavaScript

JavaScript (JS) is one of the most popular coding languages in the world and allows pages to become interactive. HTML is used to create the website structure and content, while JavaScript is used to control the functionality of web pages. 

Without JavaScript, a page would not have interactive elements and would always be static. JS can dynamically update the page in real-time, giving functionality to change the style of a button when a particular event on the page occurs (such as when a user clicks a button) or to display moving animations.

JavaScript is added within the page source code and can be either loaded within ``<script>`` tags or can be included remotely with the src attribute: `<script src="/location/of/javascript_file.js"></script>`

## Sensitive Data Exposure

Sensitive Data Exposure occurs when a website does not properly protect (or remove) sensitive clear-text information from the end user. This is usually found in a site's frontend source code.

We know that websites are built using many HTML elements (tags), all of which we can see simply by using **"View Page Source"**. A website developer may forget to remove login credentials, hidden links to private parts of the website, or other sensitive data exposed in HTML or JavaScript.

Sensitive information can potentially be leveraged to further an attacker's access within different parts of a web application. For example, there could be HTML comments containing temporary login credentials. If you view the page’s source code and find this information, you could use those credentials to log in elsewhere on the application — or worse, use them to access backend components of the site.

Whenever you're assessing a web application for security issues, one of the first things you should do is review the page source code to see if you can find any exposed login credentials, hidden links, API keys, or other sensitive information.
```html
<!DOCTYPE html>
<html>
<head>
    <title>Fake Website</title>
</head>
<body>
    <form>
        <input type="text" name="username">
        <input type="password" name="password">
        <button>Login</button>
        <!-- TODO: remove test credentials admin:password123 -->
    </form>
</body>
</html>
```

## HTML Injection

HTML Injection is a vulnerability that occurs when unfiltered user input is displayed on the page. If a website fails to sanitise user input (filter any "malicious" text that a user inputs into a website), and that input is used on the page, an attacker can inject HTML code into a vulnerable website.

Input sanitisation is very important in keeping a website secure, as information a user inputs into a website is often used in other frontend and backend functionality. A vulnerability you'll explore in another lab is database injection, where you can manipulate a database lookup query to log in as another user by controlling the input that's directly used in the query.

When a user has control of how their input is displayed, they can submit HTML (or JavaScript) code, and the browser will use it on the page, allowing the user to control the page's appearance and functionality.
