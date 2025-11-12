


# 🧠 Node.js Workshop Tutorial
**Workshop:** Introduction to Node.js  
**Facilitator:** Aibal Jose  
**Organized by:** µLearn AJCE  



## 🎯 Objective
In this workshop, we’ll learn how to:
- Understand what Node.js is and how it works
- Use Node.js built-in modules (`os`, `http`)
- Create a simple web server
- Handle HTTP requests (GET & POST)
- Modularize Node.js code using external files



## 🧩 Step 1 — Modularization

### 👉 What is Modularization?
In Node.js, **modularization** means splitting code into smaller reusable files (modules).  
Each module can export variables, functions, or objects which can be imported using `require()`.



### 🗂 File 1: `basejs.js`
This file defines a reusable function.

```js
// basejs.js
function mainmethod() {
  console.log("Main method executed from basejs module!");
}

module.exports = { mainmethod };
````

### 🗂 File 2: `index.js`

Now we **import** and use it inside our main file:

```js
// Modularization
const mainmethod = require("./basejs");
mainmethod.mainmethod();
```

✅ When you run `node index.js`, it will print:

```
Main method executed from basejs module!
```

---

## ⚙️ Step 2 — Node.js Basics: OS Module

The **`os`** module provides information about your operating system — memory, platform, CPU, etc.

Add this code:

```js
const os = require("os");

console.log("Free Memory:", os.freemem());
console.log("Total Memory:", os.totalmem());
console.log("Platform:", os.platform());
```

✅ Output Example:

```
Free Memory: 2415167488
Total Memory: 8252344320
Platform: win32
```

---

## 🌐 Step 3 — Creating a Basic HTTP Server

We’ll now create a simple web server using Node’s built-in **`http`** module.

```js
const http = require("http");

const server = http.createServer((req, res) => {
  console.log(req.url);                  // Shows requested URL
  console.log(req.method);               // Shows HTTP method (GET, POST, etc.)
  console.log(req.headers);              // Shows headers
  console.log(req.socket.remoteAddress); // Shows client IP

  // Example response for GET
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello from Node.js Server!");
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000/");
});
```

✅ Now visit:
**[http://localhost:3000/](http://localhost:3000/)** in your browser
and see your Node.js server respond.

---

## 📦 Step 4 — Handling POST Requests with JSON

We’ll now enhance the server to **receive JSON data** via POST requests.

```js
const http = require("http");

const server = http.createServer((req, res) => {
  console.log(req.url);
  console.log(req.method);
  console.log(req.headers);
  console.log(req.socket.remoteAddress);

  let body = "";

  if (req.method === "POST") {
    // Listen for data chunks
    req.on("data", chunk => {
      body += chunk;
    });

    // When all data received
    req.on("end", () => {
      const data = JSON.parse(body);
      console.log("Received:", data);

      // Send response
      res.writeHead(200, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ message: "User received!", user: data }));
    });
  } else {
    // For GET or other requests
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Welcome to Node.js Workshop Server!");
  }
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000/");
});
```

✅ Test using **curl** or **Postman:**

```bash
curl -X POST http://localhost:3000 \
-H "Content-Type: application/json" \
-d "{\"name\":\"Aibal Jose\", \"role\":\"Campus Lead\"}"
```

### Example Output in Terminal:

```
Received: { name: 'Aibal Jose', role: 'Campus Lead' }
```

### Example Response:

```json
{
  "message": "User received!",
  "user": { "name": "Aibal Jose", "role": "Campus Lead" }
}
```

---

## 🧠 Step 5 — Understanding `req` and `res` Objects

| Property / Method          | Description                                 |
| -------------------------- | ------------------------------------------- |
| `req.url`                  | URL of the request                          |
| `req.method`               | HTTP method (GET, POST, PUT, DELETE)        |
| `req.headers`              | Request header details                      |
| `req.socket.remoteAddress` | IP address of the client                    |
| `req.on("data")`           | Event listener for receiving chunks of data |
| `req.on("end")`            | Triggered after all data has been received  |
| `res.writeHead()`          | Sets status code and response headers       |
| `res.end()`                | Ends the response and sends data back       |

---

## 🧩 Step 6 — Combine All Together (Final Code)

### 🗂 index.js (Final Version)

```js
// Modularization
const mainmethod = require("./basejs");
mainmethod.mainmethod();

// Node basic
const os = require("os");

console.log(os.freemem());
console.log(os.totalmem());
console.log(os.platform());

// HTTP Server
const http = require("http");

const server = http.createServer((req, res) => {
  console.log(req.url);
  console.log(req.method);
  console.log(req.headers);
  console.log(req.socket.remoteAddress);

  let body = '';

  if (req.method == "POST") {
    req.on("data", chunk => {
      body += chunk;
    });

    req.on("end", () => {
      const data = JSON.parse(body);
      console.log("Received:", data);

      res.writeHead(200, { "Content-Type": "application/json" });
      res.end(JSON.stringify({ message: "User received!", user: data }));
    });
  } else {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Welcome to Node.js Workshop Server!");
  }
});

server.listen(3000, () => {
  console.log("Server running at http://localhost:3000/");
});
```

---

## 💻 Step 7 — Running the Application

1. Save both files (`index.js` and `basejs.js`) in the same folder.
2. Run:

   ```bash
   node index.js
   ```
3. Open [http://localhost:3000/](http://localhost:3000/) in your browser.

---

## 🧩 Step 8 — Experiment

Try modifying:

* Response type (e.g., `"Content-Type": "application/json"`)
* Add a new route like `/about`
* Log the request body and headers
* Create another module file for utilities

---

## 🧭 Summary

| Concept          | Description                                         |
| ---------------- | --------------------------------------------------- |
| `require()`      | Imports a module                                    |
| `module.exports` | Exports functions or variables from a module        |
| `os` module      | Provides system information                         |
| `http` module    | Allows creation of a web server                     |
| `req` & `res`    | Request and Response objects used for communication |
| `req.on("data")` | Handles streaming request data                      |
| Modularization   | Makes code reusable and organized                   |

---

## 🚀 Next Steps

After this workshop, explore:

* Express.js for faster API building
* `fs` module (File system operations)
* Creating REST APIs
* Using environment variables

---

## ❤️ Credits

**Facilitator:** Aibal Jose
**Organized by:** µLearn AJCE
**Topic:** Node.js Fundamentals
**Date:** *12/11/2025*


