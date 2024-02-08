The Node.js file system (fs) module allows you to work with the file system on your machine.
To include the File System module, use the `require()` method:

```node
const fs = require("fs");
```

Common use for the File System module:

- Read files
- Write files
- Append files
- Copy files
- Delete files (Unlink)

The process of handling files can be either asynchronous (async) or Synchronous (sync).

1. **Synchronous File Handling**:
    - Synchronous file handling blocks the execution of subsequent code until the file operation (e.g., reading or writing) is complete.
    - Synchronous methods have names ending with 'Sync' (e.g., `fs.readFileSync()`, `fs.writeFileSync()`).
    - They can potentially lead to performance issues, especially in applications that require high concurrency, as they block the event loop during execution.

2. **Asynchronous File Handling**:
	- Asynchronous file handling does not block the execution of subsequent code. Instead, it utilizes callbacks, promises, or async/await syntax to handle the result of file operations.
	- Asynchronous methods do not have 'Sync' in their names (e.g., `fs.readFile()`, `fs.writeFile()`).
	- These methods are more suitable for I/O-bound operations, especially in applications requiring high concurrency
	- Asynchronous code can be more complex due to callback handling or promise chaining, but it generally provides better performance and scalability.

In summary, synchronous file handling in Node.js can be simpler but may cause performance bottlenecks, while asynchronous file handling is more efficient for I/O-bound operations and allows for better scalability, especially in applications with high concurrency requirements.

Code snippets for the common file actions:
``` node

const file = require("fs");

//sync file writing
file.writeFileSync("test.txt","Creting files using fs module");

//async file writing
file.writeFile("test.txt","test for async data writing", (err)=> {});

//sync file read
result = file.readFileSync("./test.txt","utf-8")
console.log(result)

//async file read
file.readFile("./test.txt","utf-8",(err,result)=>{
if(err){
console.log("Error ",err);
} else{
console.log(result);
}
});

//appending file
file.appendFileSync("./test.txt","appended txt\n")

//copying file
file.copyFileSync("./test.txt","./copied.txt");

//deleting a file (unlinking a file)
file.unlinkSync("./copied.txt");
```
