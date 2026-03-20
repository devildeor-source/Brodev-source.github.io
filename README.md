<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Brodev AI</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background-color: #0d0d0d;
      color: white;
      display: flex;
      flex-direction: column;
      height: 100vh;
    }

    /* Header */
    .header {
      padding: 15px;
      font-size: 20px;
      font-weight: bold;
      border-bottom: 1px solid #333;
    }

    /* Chat area */
    .chat-container {
      flex: 1;
      padding: 20px;
      overflow-y: auto;
    }

    .welcome {
      text-align: center;
      margin-top: 30%;
      opacity: 0.7;
    }

    .welcome h1 {
      font-size: 32px;
      margin-bottom: 10px;
    }

    .welcome p {
      font-size: 14px;
      letter-spacing: 2px;
    }

    /* Input area */
    .input-container {
      position: fixed;
      bottom: 0;
      width: 100%;
      background-color: #0d0d0d;
      border-top: 1px solid #333;
      padding: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .input-box {
      display: flex;
      width: 90%;
      max-width: 600px;
      background: #1a1a1a;
      border-radius: 25px;
      padding: 5px;
      align-items: center;
    }

    input {
      flex: 1;
      padding: 12px;
      border: none;
      outline: none;
      background: transparent;
      color: white;
      font-size: 16px;
    }

    button {
      background: #4CAF50;
      border: none;
      color: white;
      padding: 10px 14px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 16px;
    }

    button:hover {
      background: #45a049;
    }

    /* Chat messages */
    .message {
      margin: 10px 0;
      padding: 10px 15px;
      border-radius: 15px;
      max-width: 70%;
    }

    .user {
      background-color: #4CAF50;
      align-self: flex-end;
      margin-left: auto;
    }

    .bot {
      background-color: #333;
      align-self: flex-start;
    }

  </style>
</head>

<body>

  <!-- Header -->
  <div class="header">
    Brodev AI
  </div>

  <!-- Chat Area -->
  <div class="chat-container" id="chat">
    <div class="welcome" id="welcome">
      <h1>HELLO WORLD</h1>
      <p>READY FOR REQUEST</p>
    </div>

  </div>
  <!-- Input Area -->
  <div class="input-container">
    <div class="input-box">
      <input type="text" id="message" placeholder="How can I help you?" />
      <button onclick="sendMessage()">➤</button>
    </div>
  </div>

  <script>
    function sendMessage() {
      const input = document.getElementById("message");
      const chat = document.getElementById("chat");
      const welcome = document.getElementById("welcome");

      let text = input.value.trim();
      if (text === "") return;

      // Remove welcome text after first message
      if (welcome) welcome.style.display = "none";

      // User message
      let userMsg = document.createElement("div");
      userMsg.className = "message user";
      userMsg.innerText = text;
      chat.appendChild(userMsg);

      // Bot reply (temporary)
      let botMsg = document.createElement("div");
      botMsg.className = "message bot";
      botMsg.innerText = "Thinking...";
      chat.appendChild(botMsg);

      // Scroll down
      chat.scrollTop = chat.scrollHeight;

      // Clear input
      input.value = "";

      // Fake response (replace with API later)
      setTimeout(() => {
        botMsg.innerText = "This is a demo response.";
      }, 1000);
    }
    // Enter key support
      document.getElementById("message").addEventListener("keypress", function(e) {
      if (e.key === "Enter") {
        sendMessage();
      }
    });
  </script>

</body>
</html>
