# 🧩 JSON POST Sender (HTML + JS)

A simple tool to send POST requests with JSON data.  
You can manually enter the URL and JSON body, then view the formatted JSON response.

---

## 💻 HTML Code

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <title>JSON POST Sender</title>
  <style>
    body {
      font-family: system-ui, sans-serif;
      max-width: 650px;
      margin: 2rem auto;
      padding: 1rem;
    }
    input, textarea {
      width: 100%;
      padding: 8px;
      margin-top: 6px;
      margin-bottom: 12px;
      font-family: monospace;
      font-size: 14px;
      border: 1px solid #ccc;
      border-radius: 5px;
    }
    button {
      background: #007bff;
      color: white;
      border: none;
      padding: 10px 16px;
      border-radius: 6px;
      cursor: pointer;
    }
    button:hover {
      background: #0056b3;
    }
    pre {
      background: #f6f8fa;
      padding: 10px;
      border-radius: 6px;
      overflow-x: auto;
      white-space: pre-wrap;
    }
  </style>
</head>
<body>
  <h2>🔗 JSON POST Sender</h2>

  <label>Enter URL:</label>
  <input id="url" type="text" placeholder="https://example.com/api" required />

  <label>Enter JSON Data:</label>
  <textarea id="jsonData" rows="8" placeholder='{"name":"John","email":"john@example.com"}'></textarea>

  <button id="sendBtn">Send POST Request</button>

  <h3>Response:</h3>
  <pre id="responseBox">No response yet</pre>

  <script>
    document.getElementById("sendBtn").addEventListener("click", async () => {
      const url = document.getElementById("url").value.trim();
      const jsonInput = document.getElementById("jsonData").value.trim();
      const responseBox = document.getElementById("responseBox");

      if (!url) {
        alert("Please enter a URL");
        return;
      }

      let data;
      try {
        data = jsonInput ? JSON.parse(jsonInput) : {};
      } catch (e) {
        alert("Invalid JSON format!");
        return;
      }

      responseBox.textContent = "Sending request...";

      try {
        const res = await fetch(url, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify(data)
        });

        const text = await res.text();
        try {
          const json = JSON.parse(text);
          responseBox.textContent = JSON.stringify(json, null, 2);
        } catch {
          responseBox.textContent = text;
        }
      } catch (err) {
        responseBox.textContent = "Error: " + err.message;
      }
    });
  </script>
</body>
</html>
