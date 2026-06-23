# What Happens When You Type https://www.google.com in Your Browser and Press Enter?

When you type `https://www.google.com` in your browser and press Enter, many steps happen in a very short time. The browser does not magically know where Google is or how to display the page. It must resolve the domain name, establish a network connection, pass through security layers, communicate over encrypted HTTPS, reach Google’s infrastructure, and receive a response from web and application servers that may use databases or other internal services.

This article explains the main steps at a high level.

## 1. The Browser Checks the URL

First, the browser reads the URL:

`https://www.google.com`

The URL tells the browser several important things:

- `https` means the browser must use HTTPS, which is HTTP over TLS/SSL encryption.
- `www.google.com` is the domain name.
- Because no port is written in the URL, the browser uses the default HTTPS port, which is port `443`.

Before connecting to the server, the browser needs to know the IP address of `www.google.com`.

## 2. DNS Request

Computers communicate using IP addresses, not domain names. A domain name such as `www.google.com` is easy for humans to remember, but the browser needs an IP address to connect to the server.

The browser starts a DNS lookup. DNS stands for Domain Name System. It works like the phonebook of the internet.

The browser checks several places before sending a DNS request to the internet:

1. Browser DNS cache
2. Operating system DNS cache
3. Local hosts file
4. DNS resolver, usually provided by the ISP or a public DNS provider

If the IP address is not cached, the DNS resolver looks for the answer. It may contact root DNS servers, top-level domain servers for `.com`, and authoritative DNS servers for `google.com`.

Finally, the DNS resolver returns an IP address for `www.google.com`.

Now the browser knows which server IP address it should contact.

## 3. TCP/IP Connection

After DNS resolution, the browser opens a network connection to the IP address returned by DNS.

The internet mainly uses the TCP/IP model for communication. IP is responsible for addressing and routing packets between machines. TCP is responsible for creating a reliable connection between the client and the server.

For HTTPS, the browser connects to port `443`.

Before data can be exchanged, TCP performs a three-way handshake:

1. The client sends a SYN packet to the server.
2. The server replies with SYN-ACK.
3. The client replies with ACK.

After this handshake, a TCP connection is established between the browser and the server.

## 4. Firewall

Before the request reaches the final server, it may pass through one or more firewalls.

A firewall is a security system that controls network traffic based on rules. It can allow or block traffic depending on the source IP, destination IP, port, protocol, or other security policies.

For example, a firewall may allow HTTPS traffic on port `443` but block unwanted or suspicious traffic.

Firewalls protect infrastructure from unauthorized access and reduce exposure to attacks.

## 5. HTTPS and SSL/TLS

Because the URL starts with `https`, the browser and the server must create an encrypted connection.

HTTPS means HTTP over TLS. Older explanations may say SSL, but modern HTTPS uses TLS. The purpose is to encrypt the communication between the browser and the server.

During the TLS handshake:

1. The browser and server agree on encryption settings.
2. The server sends its TLS certificate.
3. The browser verifies that the certificate is valid and trusted.
4. The browser and server create shared encryption keys.
5. After that, all HTTP data is encrypted.

This is important because it protects sensitive information from being read or modified while traveling over the network.

## 6. Load Balancer

Large websites like Google do not depend on one server only. They use many servers distributed across different locations.

After the encrypted connection is established, the request may reach a load balancer.

A load balancer distributes incoming traffic across multiple backend servers. This helps with performance, availability, and scalability.

Instead of sending all users to one server, the load balancer chooses a healthy backend server that can handle the request.

Load balancers can use different algorithms, such as:

- Round Robin
- Least Connections
- IP Hash
- Weighted Round Robin

The goal is to prevent one server from being overloaded and to keep the service available even if one backend server fails.

## 7. Web Server

The request then reaches a web server.

A web server, such as Nginx or Apache, handles HTTP or HTTPS requests. Its job is to receive the request, understand what resource is being requested, and decide how to respond.

The web server can serve static files directly, such as:

- HTML
- CSS
- JavaScript
- Images
- Icons

If the request requires dynamic processing, the web server forwards it to an application server.

## 8. Application Server

The application server runs the application code and business logic.

For example, if the request needs personalized results, user-specific content, search processing, authentication, or interaction with internal services, the application server handles that logic.

The application server may:

- Process the request
- Call internal APIs
- Apply business rules
- Communicate with databases
- Generate a dynamic response

In the case of Google, the application layer is extremely complex because it may involve search systems, ranking systems, caching systems, user account services, ads systems, and many other internal services.

## 9. Database

Many dynamic websites need databases to store and retrieve data.

A database stores structured information such as users, settings, content, logs, sessions, or application data.

When the application server needs data, it sends a query to a database or another storage system. The database processes the query and returns the result.

For a service like Google, the backend does not depend on a single traditional database only. It uses large distributed storage systems, caches, indexes, and databases. However, the general idea is the same: the application needs to retrieve or store data before building a response.

## 10. The Server Sends a Response Back

After the web server and application server finish processing the request, a response is sent back to the browser.

The response usually contains:

- HTTP status code, such as `200 OK`
- Headers
- HTML document
- References to CSS, JavaScript, images, and other resources

Because the connection is HTTPS, the response is encrypted before traveling back to the browser.

The browser receives the response, decrypts it, reads the HTML, and starts rendering the page. If the HTML references additional files such as CSS, JavaScript, fonts, or images, the browser sends more requests to download them.

Finally, the page appears on the screen.

## Summary

When you type `https://www.google.com` and press Enter, the browser performs many steps:

1. It reads the URL.
2. It sends a DNS request to find the IP address.
3. It establishes a TCP connection using TCP/IP.
4. The request may pass through firewalls.
5. It creates a secure HTTPS connection using TLS.
6. The request reaches a load balancer.
7. The load balancer forwards the request to a web server.
8. The web server may forward dynamic work to an application server.
9. The application server may communicate with databases or internal services.
10. The response is sent back to the browser and rendered as a web page.

This process happens very quickly, but it includes many important layers of the web infrastructure: DNS, TCP/IP, firewalls, HTTPS/SSL, load balancing, web servers, application servers, and databases.
