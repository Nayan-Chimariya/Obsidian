Hypertext Transfer Protocol (HTTP) is a method for encoding and transporting information between a client (such as a web browser) and a web server.

![[http_handshake.png]]

This diagram shows a simplified version of how your computer communicates with a server. Here’s the breakdown of each step:

1. You tell your browser to go to `http://someserver.com/link`.
2. Your device and the server set up a TCP connection.
3. Your browser sends an **HTTP request** to the server.
4. The server receives the HTTP request and parses it.
5. The server responds with an **HTTP response**.
6. Your computer receives, parses, and displays the response.

![[http_methods.png]]

## HTTP Request

HTTP was designed to send content over the Internet, like HTML, videos, images, and so on. This is done with an HTTP request and response. HTTP requests contain the following elements:

- **The method** describes what action the client wants to perform. The method for static content is typically `GET`, though there are others available, like `POST`, `HEAD`, and `DELETE`.

- **The path** indicates to the server what web page you would like to request. For example, the path of this page is `/python-https`.

- **The version** is one of several HTTP versions, like 1.0, 1.1, or 2.0. 

- **The headers** help describe additional information for the server.

- **The body** provides the server with information from the client. Though this field is not required, it’s typical for some methods to have a body, like a `POST`.

## HTTP Response

These are the tools your browser uses to communicate with a server. The server responds with an HTTP response. The HTTP response contains the following elements:

- **The version** identifies the HTTP version, which will typically be the same as the request’s version.

- **The status code** indicates whether a request was completed successfully. There are quite a few [status codes](https://www.restapitutorial.com/httpstatuscodes.html).

- **The status message** provides a human-readable message that helps describe the status code.

- **The headers** allow the server to respond with additional metadata about the request. These are the same concept as request headers.

- **The body** carries the content. Technically, this is optional, but typically it contains a useful resource.



## [More on HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview)



