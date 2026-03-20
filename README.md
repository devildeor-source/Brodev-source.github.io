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

    .header {
      padding: 15px;
      font-size: 20px;
      font-weight: bold;
      border-bottom: 1px solid #333;
    }

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

    /* Input section */
    .input-container {
      position: fixed;
      bottom: 0;
      width: 100%;
      background-color: #0d0d0d;
      border-top: 1px solid #333;
      padding: 10px;
      display: flex;
      justify-content: center;
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
      border: none;
      color: white;
      padding: 10px;
      border-radius: 50%;
      cursor: pointer;
      font-size: 16px;
      margin: 0 3px;
    }

    /* Send button */
    .send-btn {
      background: #4CAF50;
    }

    .send-btn:hover {
      background: #45a049;
    }

    /* Mic button */
    #micBtn {
      background: #333;
    }

    #micBtn.active {
      background: red;
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
      margin-left: auto;
    }

    .bot {
      background-color: #333;
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
      <button id="micBtn">🎤</button>
      <input type="text" id="message" placeholder="How can I help you?" />
      <button class="send-btn" onclick="sendMessage()">➤</button>
    </div>
  </div>

  <script>
    function sendMessage() {
      const input = document.getElementById("message");
      const chat = document.getElementById("chat");
      const welcome = document.getElementById("welcome");

      let text = input.value.trim();
      if (text === "") return;

      if (welcome) welcome.style.display = "none";

      let userMsg = document.createElement("div");
      userMsg.className = "message user";
      userMsg.innerText = text;
      chat.appendChild(userMsg);

      let botMsg = document.createElement("div");
      botMsg.className = "message bot";
      botMsg.innerText = "Thinking...";
      chat.appendChild(botMsg);

      chat.scrollTop = chat.scrollHeight;
      input.value = "";

      setTimeout(() => {
        botMsg.innerText = "This is a demo response.";
      }, 1000);
    }

    document.getElementById("message").addEventListener("keypress", function(e) {
      if (e.key === "Enter") {
        sendMessage();
      }
    });

    // 🎤 MIC FEATURE
    document.addEventListener("DOMContentLoaded", function () {

      const micBtn = document.getElementById("micBtn");
      const messageInput = document.getElementById("message");

      let recognition;
      let isListening = false;

      if ('webkitSpeechRecognition' in window) {
        recognition = new webkitSpeechRecognition();
        recognition.continuous = false;
        recognition.lang = "en-US";

        recognition.onresult = function(event) {
          const transcript = event.results[0][0].transcript;
          messageInput.value = transcript;
        };

        recognition.onend = function() {
          isListening = false;
          micBtn.classList.remove("active");
        };
      } else {
        micBtn.style.display = "none";
      }

      micBtn.onclick = () => {
        if (!recognition) return;

        if (!isListening) {
          recognition.start();
          isListening = true;
          micBtn.classList.add("active");
        } else {
          recognition.stop();
          isListening = false;
          micBtn.classList.remove("active");
        }
      };

    });
  </script>

</body>
</html>
