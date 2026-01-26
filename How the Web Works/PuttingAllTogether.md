# Putting All Together

When you request a website, your computer needs to know the server's IP address it needs to talk to; for this, it uses DNS. Your computer then talks to the web server using a special set of commands called the HTTP protocol; the webserver then returns HTML, JavaScript, CSS, Images, etc., which your browser then uses to correctly format and display the website to you.

There are also a few other components that help the web run more efficiently and provide extra features.

## Other Components

### Load Balancers

When a website's traffic starts getting quite large or is running an application that requires high availability, a single web server may no longer be enough. Load balancers provide two main features: ensuring high-traffic websites can handle the load and providing failover if a server becomes unresponsive.

When you request a website that uses a load balancer, the load balancer receives your request first and then forwards it to one of the multiple servers behind it. The load balancer uses different algorithms to decide which server is best to handle the request. Examples of these algorithms include **round-robin**, which sends requests to each server in turn, and **weighted**, which checks how many requests a server is currently handling and sends traffic to the least busy server.

Load balancers also perform periodic checks on each server to ensure they are running correctly; this is called a **health check**. If a server doesn’t respond properly, the load balancer will stop sending traffic to it until it becomes healthy again.

### CDN (Content Delivery Networks)

A CDN can be an excellent resource for reducing traffic to a busy website. It allows you to host static files from your website, such as JavaScript, CSS, images, and videos, across thousands of servers around the world.

When a user requests one of these hosted files, the CDN determines which server is geographically closest to the user and serves the content from there instead of from the origin server, which may be located far away. This improves speed and reduces load on the main web server.

### Databases

Websites often need a way to store information for their users. Web servers communicate with databases to store and retrieve data.

Databases can range from simple text-based storage to complex clusters of multiple servers that provide high speed and resilience. Some common database systems you may encounter include **MySQL, MSSQL, MongoDB, and PostgreSQL**, each with its own features and use cases.


### WAF (Web Application Firewall)

A WAF sits between the client’s web request and the web server. Its primary purpose is to protect the web server from attacks such as hacking attempts or denial-of-service attacks.

It analyzes web requests for common attack patterns, checks whether the request is coming from a real browser rather than a bot, and monitors for excessive traffic. A WAF often uses **rate limiting**, which restricts how many requests an IP address can make within a certain time period.

If a request is identified as potentially malicious, it is blocked and never forwarded to the web server.


## How Web Servers Work

### What is a Web Server

A web server is software that listens for incoming connections and uses the HTTP protocol to deliver web content to its clients. Some of the most common web server software you’ll come across are **Apache, Nginx, IIS, and Node.js**.

A web server delivers files from what is called its **root directory**, which is defined in the server’s configuration. For example, Nginx and Apache share the same default location of `/var/www/html` on Linux operating systems, while IIS uses `C:\inetpub\wwwroot` on Windows.

So, if you request the file ``http://www.example.com/picture.jpg``, 
The server would return the file located at ``/var/www/html/picture.jpg`` from its local hard drive.

### Virtual Hosts

Web servers can host multiple websites with different domain names. To achieve this, they use **virtual hosts**.

The web server checks the hostname provided in the HTTP request headers and matches it against its virtual host configuration (which is usually stored in text-based configuration files). If a match is found, the correct website is served. If no match is found, the default website is served instead.

Virtual hosts can have their root directories mapped to different locations on the hard drive. For example:

- `one.com` → `/var/www/website_one`  
- `two.com` → `/var/www/website_two`

There is no strict limit to the number of different websites you can host on a single web server, as long as system resources allow it.


### Static vs Dynamic Content

**Static content** is content that does not change. Common examples include images, JavaScript files, CSS files, and even HTML pages that always remain the same. These files are served directly from the web server without modification.

**Dynamic content**, on the other hand, can change depending on the request. For example:

- A blog homepage showing the most recent posts  
- A search page displaying results based on a user’s search query  

The content changes depending on data and user input.

These changes are handled in what is called the **Backend**, using programming and scripting languages. It’s called the backend because all processing happens behind the scenes. You cannot view the backend logic by looking at the page source, the HTML you see is only the result of that processing.

Everything you see in your browser is part of the **Frontend**, while the logic, database queries, and processing happen in the **Backend**.

## Fluxo de conexão

1. **DNS Resolve** → Descobre o IP do site  
2. **Connection** → Navegador abre conexão com o servidor  
3. **Security Layers** → Passa por CDN, WAF e Load Balancer  
4. **Web Server** → Recebe requisição HTTP  
5. **Backend** → Processa lógica do site  
6. **Database** → Busca ou salva dados  
7. **Response** → HTML volta para o navegador  
8. **Frontend** → Página aparece para o usuário

