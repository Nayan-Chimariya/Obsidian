Node.js has a built-in module called HTTP, which allows Node.js to transfer data over the Hyper Text Transfer Protocol (HTTP).

import the module using the `require` method:
```node
const http = require("hhtp");
```

The HTTP module can create an HTTP server that listens to server ports and gives a response back to the client.

Use the `createServer()` method to create an HTTP server:

```node
const myServer = http.createServer(function (req, res) {  
  res.write('Hello World!'); 
  res.end();
});

myServer.listen(8000, () => {
console.log("Started Server at port 8000");
});
```
