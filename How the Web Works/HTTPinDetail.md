# HTTP (HyperText Transfer Protocol)

HTTP is the protocol used whenever you view a website. It is a set of rules that allows web browsers and web servers to communicate and transfer webpage data such as HTML, images, videos, and other resources.

HTTP works on a request–response model:
- A client (your browser) sends a request to a server
- The server processes the request and sends back a response

However, HTTP sends data in plain text, meaning it can be read by anyone who intercepts the traffic.

## HTTPS (HyperText Transfer Protocol Secure)

HTTPS is the secure version of HTTP. It uses encryption to protect the data being transmitted between your browser and the web server.

This encryption provides:

- **Confidentiality** – Prevents others from seeing the data you send and receive  
- **Integrity** – Ensures the data is not modified during transmission  
- **Authentication** – Confirms that you are communicating with the legitimate web server and not an impersonator

HTTPS achieves this by using **TLS (Transport Layer Security)**, which relies on digital certificates issued by trusted Certificate Authorities (CAs).


## Request and Responses

When we access a website, your browser will need to make requests to a web server for assets such as HTML, Images, and download the responses. Before that, you need to tell the browser specifically how and where to access these resources, this is where URLs will help.

### What is a URL (Uniform Resource Locator)

A URL is predominantly an instruction on how to access a resource on the internet.

| URL Part | Description | Example |
|----------|-------------|---------|
| **Scheme** | Instructs on what protocol to use for accessing the resource, such as HTTP, HTTPS, or FTP. | `http` |
| **User** | Some services require authentication to log in. You can include a username and password in the URL. | `user:password@` |
| **Host** | The domain name or IP address of the server you wish to access. | `genericwebsite.com` |
| **Port** | The port you are going to connect to. Usually 80 for HTTP and 443 for HTTPS, but it can be any port between 1–65535. | `:80` |
| **Path** | The file name or location of the resource you are trying to access. | `/view-room` |
| **Query String** | Extra bits of information that can be sent to the requested path. | `?id=1` |
| **Fragment** | A reference to a location on the actual page requested. Commonly used for pages with long content so a specific section can be linked directly. | `#task3` |


## Making A Request

It's possible to make a request to a web server with just one line **GET / HTTP/1.1**

But for a much richer web experience, you’ll need to send other data as well. This other data is sent in what is called headers, where headers contain extra information to give to the web server you’re communicating with.

### Example Request

```
GET / HTTP/1.1

Host: genericwebsite.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://genericwebsite/
```


To break down each line of this request:

**Line 1:** This request is using the **GET** method (more on this in the HTTP Methods section), requesting the home page `/` and telling the web server we are using **HTTP protocol version 1.1**.

**Line 2:** We tell the web server we want the website **genericwebsite.com**.

**Line 3:** We tell the web server we are using the **Firefox version 87** browser.

**Line 4:** We are telling the web server that the web page that referred us to this one is **https://genericwebsite.com**.

**Line 5:** HTTP requests always end with a blank line to inform the web server that the request has finished.


### Example Response

``` 
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98


<html>
<head>
    <title>GenericWebsite</title>
</head>
<body>
    Welcome To GenericWebsite.com
</body>
</html>
```

To break down each line of the response:

**Line 1:** `HTTP/1.1` is the version of the HTTP protocol the server is using, followed by the HTTP Status Code, in this case **200 OK**, which tells us the request has completed successfully.

**Line 2:** This tells us the web server software and version number.

**Line 3:** The current date, time, and timezone of the web server.

**Line 4:** The `Content-Type` header tells the client what sort of information is going to be sent, such as HTML, images, videos, PDF, XML, etc.

**Line 5:** `Content-Length` tells the client how long the response is. This allows the client to confirm that no data is missing.

**Line 6:** The HTTP response contains a blank line to confirm the end of the HTTP headers.

**Line 7–14:** The information that has been requested, in this instance the homepage (the response body).

## HTTP Methods

HTTP methods are a way for the client to show its intended action when making an HTTP request. Some of the most common methods are:

### GET Request

Used for retrieving information from a web server.  
GET requests should not modify data on the server, they are meant to be read-only.

### POST Request

Used for submitting data to the web server, often to create new records.  
This is commonly used when sending form data, uploading files, or creating accounts.

### PUT Request

Used for sending data to a web server to update or replace existing information.  
PUT typically replaces the entire resource with the new data provided.

### DELETE Request

Used for deleting information or records from a web server.

## HTTP Status Codes

when a HTTP server responds, the first line always contains a status code informing the client of the outcome of their request and also potentially how to handle it. These status codes can be broken down into 5 different ranges:

| Status Code Range | Description |
|-------------------|-------------|
| **100–199 – Information Response** | These are sent to tell the client the first part of their request has been accepted and they should continue sending the rest of their request. These codes are not very common. |
| **200–299 – Success** | This range of status codes is used to tell the client their request was successful. |
| **300–399 – Redirection** | These are used to redirect the client's request to another resource. This can be either a different webpage or a different website altogether. |
| **400–499 – Client Errors** | Used to inform the client that there was an error with their request. |
| **500–599 – Server Errors** | This range is reserved for errors happening on the server-side and usually indicates a major problem with the server handling the request. |

### Common HTTP Status Codes

| Status Code | Meaning |
|-------------|---------|
| **200 – OK** | The request was completed successfully. |
| **201 – Created** | A resource has been created (for example, a new user or new blog post). |
| **301 – Moved Permanently** | This redirects the client's browser to a new webpage or tells search engines that the page has moved somewhere else and to look there instead. |
| **302 – Found** | Similar to the above permanent redirect, but as the name suggests, this is only a temporary change and it may change again in the near future. |
| **400 – Bad Request** | This tells the browser that something was either wrong or missing in their request. This could happen if the web server expected a certain parameter that the client didn't send. |
| **401 – Not Authorised** | You are not currently allowed to view this resource until you have authorized with the web application, most commonly with a username and password. |
| **403 – Forbidden** | You do not have permission to view this resource whether you are logged in or not. |
| **405 – Method Not Allowed** | The resource does not allow this method request. For example, you send a GET request to `/create-account` when it was expecting a POST request instead. |
| **404 – Page Not Found** | The page/resource you requested does not exist. |
| **500 – Internal Server Error** | The server has encountered some kind of error with your request that it doesn't know how to handle properly. |
| **503 – Service Unavailable** | The server cannot handle your request as it's either overloaded or down for maintenance. |


## Headers

Headers are additional bits of data you can send to the web server when making requests. Although no headers are strictly required when making an HTTP request, you’ll find it difficult to view a website properly without them.

### Common Request Headers

**Host** – Some web servers host multiple websites, so by providing the `Host` header you can tell it which one you require. Otherwise, you'll just receive the default website for that server.

**User-Agent** – This identifies your browser software and version number. Telling the web server your browser details helps it format the website properly for your browser. Some elements of HTML, JavaScript, and CSS are only supported in certain browsers.

**Content-Length** – When sending data to a web server (such as in a form submission), the `Content-Length` header tells the web server how much data to expect in the request body. This way, the server can ensure it isn't missing any data.

**Accept-Encoding** – Tells the web server what types of compression methods the browser supports so the data can be compressed and made smaller for transmission over the internet.

**Cookie** – Data sent to the server to help it remember information about you, such as session IDs or preferences.

### Common Response Headers

These are the headers that are returned to the client from the server after a request.

**Set-Cookie** – Information the browser should store and send back to the web server with future requests.

**Cache-Control** – Specifies how long the content of the response should be stored in the browser's cache before requesting it again.

**Content-Type** – Tells the client what type of data is being returned: HTML, CSS, JavaScript, images, PDF, video, etc. Using this header, the browser knows how to process the data.

**Content-Encoding** – Indicates what method has been used to compress the data to make it smaller when sending it over the internet.

## Cookies

Cookies are small pieces of data that are stored on your computer. Cookies are saved when you receive a `Set-Cookie` header from a web server. With every further request you make to that server, your browser sends the cookie data back using the `Cookie` header.

Because HTTP is stateless (it doesn't keep track of your previous requests), cookies can be used to help the web server remember who you are, store personal settings for the website, or remember whether you've visited the website before.

Cookies can be used for many purposes but are most commonly used for website authentication. The cookie value is not usually a clear-text string where you can see the password, but rather a token — a unique secret value that is difficult for humans (and attackers) to guess.


