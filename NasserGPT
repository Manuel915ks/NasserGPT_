<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NasserGPT</title>
<style>
body {
  font-family: 'Arial', sans-serif;
  margin: 0;
  height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #121212;
  color: #ffffff;
}
header {
  background-color: #1f1f1f;
  color: #00bfff;
  padding: 20px;
  text-align: center;
  font-size: 28px;
  font-weight: bold;
  letter-spacing: 1px;
  box-shadow: 0 2px 5px rgba(0,0,0,0.5);
}
#messages {
  flex: 1;
  padding: 20px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}
.message {
  padding: 12px 18px;
  margin: 8px 0;
  border-radius: 12px;
  max-width: 80%;
  word-wrap: break-word;
  font-size: 16px;
}
.user {
  background-color: #00bfff;
  color: #fff;
  align-self: flex-end;
  box-shadow: 0 2px 5px rgba(0,191,255,0.4);
}
.bot {
  background-color: #2c2c2c;
  color: #ffffff;
  align-self: flex-start;
  box-shadow: 0 2px 5px rgba(0,0,0,0.5);
}
#inputArea {
  display: flex;
  padding: 12px;
  background-color: #1f1f1f;
  border-top: 1px solid #333;
}
#input {
  flex: 1;
  padding: 12px;
  border-radius: 8px;
  border: 1px solid #333;
  font-size: 16px;
  background-color: #2c2c2c;
  color: #fff;
}
#input::placeholder {
  color: #aaa;
}
button {
  padding: 12px 24px;
  margin-left: 10px;
  border: none;
  border-radius: 8px;
  background-color: #00bfff;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  transition: 0.3s;
}
button:hover {
  background-color: #009fdf;
}
body::before {
  content: 'به ناسر چی پی تی خوش آمدید.';
  position: fixed;
  top: 10px;
  right: 10px;
  font-size: 20px;
  color: #555;
}
</style>
</head>
<body>

<header>NasserGPT</header>

<div id="messages">
  <div class="message bot">Hallo! Ich bin NasserGPT. Du kannst mir jede Frage stellen.</div>
</div>

<div id="inputArea">
  <input type="text" id="input" placeholder="Schreibe hier...">
  <button onclick="sendMessage()">Senden</button>
</div>

<script>
const messages = document.getElementById('messages');
const input = document.getElementById('input');

// --- KI-Antworten ---
function generateReply(text){
  const t = text.trim();
  const isPersian = /[\u0600-\u06FF]/.test(t);

  if(isPersian){
    // Wenn Text auf Persisch ist
    if(t.includes('سلام') || t.includes('hi')) return 'سلام! خوش آمدی 👋';
    if(t.includes('چطوری')) return 'من خوبم، مرسی! تو چطوری؟';
    return 'من پاسخ شما را به فارسی می‌دهم: ' + t;
  } else {
    // Deutsch-Antworten
    const low = t.toLowerCase();
    if(low.includes('hallo') || low.includes('hi')) return 'Hallo! Schön, dich zu sehen 👋';
    if(low.includes('wie geht')) return 'Mir geht es gut, danke! Und dir?';
    if(low.includes('wer bist')) return 'Ich bin NasserGPT, dein Chatbot-Assistent!';
    if(low.includes('hilfe') || low.includes('problem')) return 'Ich kann dir helfen. Stell mir einfach deine Frage.';
    return 'Interessant! Kannst du das noch etwas genauer erklären?';
  }
}

// --- Nachricht senden ---
function sendMessage(){
  const text = input.value.trim();
  if(!text) return;

  // Benutzer-Nachricht
  const userMsg = document.createElement('div');
  userMsg.className = 'message user';
  userMsg.textContent = text;
  messages.appendChild(userMsg);
  input.value='';
  messages.scrollTop = messages.scrollHeight;

  // Bot tippt...
  const typing = document.createElement('div');
  typing.className='message bot';
  typing.textContent='NasserGPT schreibt...';
  messages.appendChild(typing);
  messages.scrollTop = messages.scrollHeight;

  setTimeout(()=>{
    typing.remove();
    const botMsg = document.createElement('div');
    botMsg.className='message bot';
    botMsg.textContent = generateReply(text);
    messages.appendChild(botMsg);
    messages.scrollTop = messages.scrollHeight;
  }, 800);
}

// Enter-Taste senden
input.addEventListener('keydown', function(e){
  if(e.key === 'Enter') sendMessage();
});
</script>

</body>
</html>
