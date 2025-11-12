
## 🏠 Homework — Practice Tasks

Try completing the following small exercises before the next session 👇

### 🧩 Task 1: Create a Custom Module
- Create a file named `greet.js`
- Inside it, write a function `sayHello(name)` that prints:
```

Hello, <name>! Welcome to Node.js!

```
- Export it using `module.exports`
- Import it into `index.js` and call it

---

### 🌍 Task 2: Add a New Route
Modify your HTTP server so that:
- When a user visits `/about`, it should respond with:
```

This is a Node.js Workshop server created by <your name>

````
- For any other path, respond with “404 - Page Not Found”

---

### 📨 Task 3: Handle POST Data
- Create a route `/register` that accepts a POST request
- The request body should contain:
```json
{ "username": "student1" }
````

* Respond with a message:

  ```json
  { "message": "Welcome student1!" }
  ```

---

### ⚙️ Bonus Challenge (Optional)

Use the `fs` (File System) module to:

* Save each POST request body into a file called `data.json`

---

### 🕒 Submission

* Complete all tasks in a single folder
* Name it: `nodejs_homework_<yourname>`
* Include both `.js` files and a short README.md explaining what you did

---

### 🏁 Tip

Use:

```bash
node index.js
```

to test your server after each change,
and open `http://localhost:3000` in your browser or Postman.

---

🧠 **Goal:** Practice `require()`, modularization, routing, and handling POST data — the core building blocks of any Node.js backend app.


