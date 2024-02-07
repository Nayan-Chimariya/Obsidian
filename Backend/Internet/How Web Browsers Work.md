## Navigation

_Navigation_ is the first step in loading a web page. It occurs whenever a user requests a page by entering a URL into the address bar, clicking a link, submitting a form, as well as other actions.

In ideal conditions, this usually doesn't take too long, but latency and bandwidth are foes that can cause delays.

##### DNS lookup

The first step of navigating to a web page is finding where the assets for that page are located. If you navigate to `https://example.com`, the HTML page is located on the server with IP address of `93.184.216.34`. If you've never visited this site, a DNS lookup must happen.

More on [[DNS]]

##### TCP handshake

Once the IP address is known, the browser sets up a connection to the server via a **TCP three-way handshake.** This mechanism is designed so that two entities attempting to communicate — in this case the browser and web server — can negotiate the parameters of the network TCP socket connection before transmitting data, often over [[HTTP]]

![[TCP 3 way handshake.png]]



##### TLS negotiation

For secure connections established over HTTPS, another "handshake" is required. This handshake, or rather the [TLS](https://developer.mozilla.org/en-US/docs/Glossary/TLS) negotiation, determines which cipher will be used to encrypt the communication, verifies the server, and establishes that a secure connection is in place before beginning the actual transfer of data. This requires five more round trips to the server before the request for content is actually sent.

## Response

Once we have an established connection to a web server, the browser sends an initial `Get Request` on behalf of the user, which for websites is most often an HTML file. Once the server receives the request, it will reply with relevant response headers and the contents of the HTML.

```html
<!doctype html>
<html lang="en-US">
  <head>
    <meta charset="UTF-8" />
    <title>My simple page</title>
    <link rel="stylesheet" href="styles.css" />
    <script src="myscript.js"></script>
  </head>
  <body>
    <h1 class="heading">My Page</h1>
    <p>A paragraph with a <a href="https://example.com/about">link</a></p>
    <div>
      <img src="myimage.jpg" alt="image description" />
    </div>
    <script src="anotherscript.js"></script>
  </body>
</html>
```

This response for this initial request contains the first byte of data received. Time to First Byte (TTFB) is the time between when the user made the request (say by clicking on a link) and the receipt of this first packet of HTML. The first chunk of content is usually 14KB of data.

In our example above, the request is definitely less than 14KB, but the linked resources aren't requested until the browser encounters the links during parsing, described below.
##### Congestion control / TCP slow start


In order to balance the number of transmitted segments, the TCP slow start algorithm is used to gradually increase the amount of transmitted data until the maximum network bandwidth can be determined, and to reduce the amount of transmitted data in case of high network load.

The number of segments to be transmitted is controlled by the value of the congestion window (CWND), which can be initialized to 1, 2, 4, or 10 MSS (MSS is 1500 bytes over the Ethernet protocol). That value is the number of bytes to send, upon receipt of which the client must send an ACK.

If an ACK is received, then the CWND value will be doubled, and so the server will be able to send more segments the next time. If instead no ACK is received, then the CWND value will be halved. That mechanism thus achieves a balance between sending too many segments, and sending too few.



## Parsing

Once the browser receives the first chunk of data, it can begin parsing the information received. **Parsing** is the step the browser takes to turn the data it receives over the network into the DOM and CSSOM, which is used by the renderer to paint a page to the screen.

The DOM is the internal representation of the markup for the browser. The DOM is also exposed and can be manipulated through various APIs in JavaScript.

Even if the requested page's HTML is larger than the initial 14KB packet, the browser will begin parsing and attempting to render an experience based on the data it has. This is why it's important for web performance optimization to include everything the browser needs to start rendering a page, or at least a template of the page (the CSS and HTML needed for the first render) in the first 14KB. But before anything is rendered to the screen, the HTML, CSS, and JavaScript have to be parsed.

##### Building the DOM tree

The DOM tree describes the content of the document. The `<html>` element is the first element and root node of the document tree. The tree reflects the relationships and hierarchies between different elements. Elements nested within other elements are child nodes. The greater the number of DOM nodes, the longer it takes to construct the DOM tree.

![[DOM tree.png]]






## Render
Rendering steps include style, layout, paint, and in some cases compositing. The CSSOM and DOM trees created in the parsing step are combined into a render tree which is then used to compute the layout of every visible element, which is then painted to the screen. In some cases, content can be promoted to its own layer and composited, improving performance by painting portions of the screen on the GPU instead of the CPU, freeing up the main thread.


