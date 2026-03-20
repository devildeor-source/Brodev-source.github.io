<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Core AI</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #0A0A0A; color: #E0E0E0; margin: 0; padding: 0; overflow: hidden; height: 100vh; display: flex; flex-direction: column; }
        .matte-card { background: #161616; border: 1px solid rgba(255,255,255,0.05); border-radius: 24px; }
        .hide { display: none !important; }
        #chat-window { flex: 1; overflow-y: auto; padding: 20px; display: flex; flex-direction: column; gap: 15px; }
        /* Professional Matte Button */
        .send-btn { background: white; color: black; border-radius: 18px; transition: all 0.2s; }
        .send-btn:active { transform: scale(0.9); background: #3b82f6; color: white; }
    </style>
</head>
<body>
    <nav class="p-5 flex justify-between items-center border-b border-white/5 bg-[#0A0A0A]">
        <div class="flex items-center gap-2">
            <div class="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center font-bold text-white">A</div>
            <span class="font-bold tracking-tight">CORE_AI</span>
        </div>
        <div class="opacity-50 text-white">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"></circle><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"></path></svg>
        </div>
    </nav>
    <div id="chat-window">
        <div id="welcome-msg" class="flex-1 flex flex-col items-center justify-center opacity-30">
            <h1 class="text-6xl font-black tracking-tighter text-white">HELLO WORLD</h1>
            <p class="text-[10px] tracking-[0.4em] uppercase mt-2">Ready for Request</p>
        </div>
    </div>
    <div class="p-6 bg-[#0A0A0A] border-t border-white/5">
        <div class="matte-card p-1 flex items-center max-w-3xl mx-auto shadow-2xl">
            <button id="mic-btn" class="p-4 text-gray-500 hover:text-white">
                <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M12 2a3 3 0 0 0-3 3v7a3 3 0 0 0 6 0V5a3 3 0 0 0-3-3Z"></path><path d="M19 10v2a7 7 0 0 1-14 0v-2"></path><line x1="12" x2="12" y1="19" y2="22"></line></svg>
            </button>            
            <input type="text" id="user-input" placeholder="How can I help you?" 
                class="flex-1 bg-transparent border-none outline-none px-2 text-white text-md">
            <button id="send-btn" class="send-btn p-4 ml-2">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="22" y1="2" x2="11" y2="13"></line><polygon points="22 2 15 22 11 13 2 9 22 2"></polygon></svg>
            </button>
        </div>
    </div>
    <script>
        const input = document.getElementById('user-input');
        const welcome = document.getElementById('welcome-msg');
        const chatWindow = document.getElementById('chat-window');
        const sendBtn = document.getElementById('send-btn');
        const micBtn = document.getElementById('mic-btn');
        function startInteraction() {
            welcome.classList.add('hide');
        }
        // Send Logic
        sendBtn.onclick = () => {
            if(!input.value) return;
            startInteraction();
            const msg = document.createElement('div');
            msg.className = "self-end bg-blue-600 p-4 rounded-2xl rounded-tr-none max-w-[80%] text-white text-sm shadow-lg";
            msg.innerText = input.value;
            chatWindow.appendChild(msg);
            input.value = "";
            chatWindow.scrollTop = chatWindow.scrollHeight;
        };
        // Input listener for hiding "Hello World"
        input.addEventListener('keypress', (e) => { if(e.key === 'Enter') sendBtn.click(); });
        input.addEventListener('input', () => { if(input.value.length > 0) startInteraction(); });
        // Voice Recognition
        const recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
        micBtn.onclick = () => {
            recognition.start();
            micBtn.style.color = "#ef4444";
        };
        recognition.onresult = (e) => {
            input.value = e.results[0][0].transcript;
            micBtn.style.color = "";
            startInteraction();
        };
        recognition.onerror = () => { micBtn.style.color = ""; };
    </script>
</body>
</html>
