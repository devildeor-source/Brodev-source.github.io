<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>AI Solver</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">    
    <style>
        /* The Secret to Matte Black */
        body { 
            background-color: #0D0D0D; 
            color: #E0E0E0; 
            margin: 0; 
            height: 100vh; 
            display: flex; 
            flex-direction: column; 
            overflow: hidden;
        }     
        .matte-input-container {
            background: #1A1A1A;
            border: 1px solid rgba(255,255,255,0.07);
            border-radius: 28px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        #welcome-text {
            transition: opacity 0.4s ease;
        }
        .chat-area {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            overflow-y: auto;
        }
    </style>
</head>
<body>
    <div class="p-6 opacity-20">
        <span class="text-xs tracking-[0.5em] font-bold">SYSTEM_READY</span>
    </div>
    <div class="chat-area">
        <div id="welcome-text" class="text-center">
            <h1 class="text-6xl md:text-8xl font-black text-white/5 tracking-tighter select-none">
                HELLO WORLD
            </h1>
        </div>
    </div>
    <div class="p-6 pb-10 w-full max-w-3xl mx-auto">
        <div class="matte-input-container flex items-center p-2">
l            
            <button id="mic-btn" class="p-4 text-gray-500 hover:text-red-500 transition-colors">
                <i class="fa-solid fa-microphone text-xl"></i>
            </button>
            <input type="text" id="main-input" 
                class="flex-1 bg-transparent border-none outline-none px-2 text-white placeholder-gray-600 text-lg"
                placeholder="How can I help you?">
            <button id="send-btn" class="bg-white text-black w-12 h-12 rounded-2xl flex items-center justify-center hover:bg-blue-600 hover:text-white transition-all transform active:scale-90 shadow-lg">
                <i class="fa-solid fa-paper-plane text-lg"></i>
            </button>
        </div>
    </div>
    <script>
        const input = document.getElementById('main-input');
        const welcome = document.getElementById('welcome-text');
        const sendBtn = document.getElementById('send-btn');
        const micBtn = document.getElementById('mic-btn');
        // Function to hide HELLO WORLD when user interacts
        function hideWelcome() {
            welcome.style.opacity = '0';
        }
        // 1. Text Typing Logic
        input.addEventListener('input', () => {
            if (input.value.length > 0) hideWelcome();
            else welcome.style.opacity = '1';
        });
        // 2. Click Send Logic
        sendBtn.onclick = () => {
            if (input.value.trim() !== "") {
                alert("Message Sent: " + input.value); // Replace with your AI logic later
                input.value = "";
                welcome.style.opacity = '1';
            }
        };
        // 3. Voice Logic (JavaScript)
        const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();     
        micBtn.onclick = () => {
            recognition.start();
            micBtn.classList.add('text-red-500');
        };
        recognition.onresult = (event) => {
            const result = event.results[0][0].transcript;
            input.value = result;
            hideWelcome();
            micBtn.classList.remove('text-red-500');
        };
        recognition.onerror = () => micBtn.classList.remove('text-red-500');
    </script>

</body>
</html>
