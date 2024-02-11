Initially a client send the request to a server running node

**![[node_client_req.png]]

Then there is an event queue that stores the requests and works on FIFO principle.

![[node_event_queue.png]]

Then there is the event loop, that handles the requests on the event queue. It checks periodically whether there is a request on the event queue or not. Upon seeing a request, it handles that request and removes it from the event Queue.

![[event loop.png]]

The request can be of two types:
 - Blocking Request
 - Non-Blocking Request

![[requests in node server.png]]

Blocking operations halt the execution of code until they complete, while, non-blocking operations allow the code to continue executing asynchronously, enabling better utilization of system resources and improved performance, especially in I/O-heavy applications like web servers. Node.js is designed around non-blocking, asynchronous I/O operations to maximize efficiency and scalability.

Examples:

Blocking Operation:

``` node
const fs = require('fs');

// Blocking operation - Synchronous read
const data = fs.readFileSync('file.txt');
console.log(data.toString());
```

Non Blocking Operation:

```node
const fs = require('fs');

// Non-blocking operation - Asynchronous read
fs.readFile('file.txt', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data.toString());
});
```

The Thread pool:

![[thread pool.png]]

The Blocking operations require threads to complete the operation. The operation are executed only when there is a worker (thread) available. If there are no threads available, then the operations stack up and create a traffic of operations. 

The default thread pool size is 4, and it can be maxed out up to the cpu cores of the system.

Node code to see the cpu core count:

``` node
const os = require("os");
console.log(os.cpus().length);
```



