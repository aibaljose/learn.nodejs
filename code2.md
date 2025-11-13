# 🍳 Node.js Express Server Example

This simple Express.js server demonstrates:
- CORS configuration for specific frontend origins  
- JSON body parsing  
- Example routes for GET and POST requests  
- Simulated order responses

---

```js
// server.js

const express = require("express");
const cors = require("cors");
const app = express();

// ✅ CORS configuration – Allow requests from specific frontend origins
app.use(
  cors({
    origin: [
      "http://127.0.0.1:5500",
      "http://localhost:5500",
      "https://aibaljose.github.io",
      "https://aibaljose.github.io/code",
    ],
    credentials: true,
    optionsSuccessStatus: 200,
  })
);

// Parse JSON request bodies
app.use(express.json());

// 🧾 POST route – receive an order
app.post("/order", (req, res) => {
  console.log(req.body);
  res.json({
    message: "Order received successfully",
    order: req.body,
  });
});

// 🍔 GET route – simulate delayed order retrieval
app.get("/getorder", (req, res) => {
  setTimeout(() => {
    res.send("dsfsdfdsf");
  }, 2500);
});

// 🏠 Root route
app.get("/", (req, res) => {
  res.send("hai");
});

// Example of simulated cooking process
// Uncomment if you want to test delay responses
/*
app.get("/", (req, res) => {
  res.send("👨‍🍳 Chef is ready to take your orders!");
});

// Simulate order from Table 1
app.get("/table1", (req, res) => {
  console.log("🍳 Received order from Table 1");
  setTimeout(() => {
    console.log("✅ Table 1's Pasta is ready!");
    res.send("🍝 Table 1: Your Pasta is ready!");
  }, 2000);
});

// Simulate order from Table 2
app.get("/table2", (req, res) => {
  console.log("🍳 Received order from Table 2");
  setTimeout(() => {
    console.log("✅ Table 2's Pizza is ready!");
    res.send("🍕 Table 2: Your Pizza is ready!");
  }, 3000);
});

// Generic POST route for any order
app.post("/order", (req, res) => {
  const { table, dish } = req.body;
  console.log(`🪑 ${table} ordered ${dish}`);

  setTimeout(() => {
    console.log(`✅ ${table}'s ${dish} is ready!`);
    res.json({ message: `${table}: Your ${dish} is ready!` });
  }, 2500);
});
*/

// 👂 Start server
app.listen(3000, () => {
  console.log("👨‍🍳 Chef is listening on port 3000...");
});
