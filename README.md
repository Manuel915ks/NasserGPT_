<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NasserGPT</title>
<style>
body { font-family: Arial, sans-serif; margin:0; height:100vh; display:flex; flex-direction:column; background:#121212; color:#fff; }
header { background:#1f1f1f; color:#00bfff; padding:20px; text-align:center; font-size:28px; font-weight:bold; box-shadow:0 2px 5px rgba(0,0,0,0.5);}
#messages { flex:1; padding:20px; overflow-y:auto; display:flex; flex-direction:column;}
.message { padding:12px 18px; margin:8px 0; border-radius:12px; max-width:80%; word-wrap:break-word; font-size:16px;}
.user { background:#00bfff; color:#fff; align-self:flex-end; box-shadow:0 2px 5px rgba(0,191,255,0.4);}
.bot { background:#2c2c2c; color:#fff; align-self:flex-start; box-shadow:0 2px 5px rgba(0,0,0,0.5);}
#inputArea { display:flex; padding:12px; background:#1f1f1f; border-top:1px solid #333;}
#input { flex:1; padding:12px; border-radius:8px; border:1px solid #333; font-size:16px; background:#2c2c2c; color:#fff;}
#input::placeholder { color:#aaa; }
button { padding:12px 24px; margin-left:10px; border:none; border-radius:8px; background:#00bfff; color:#fff; font-size:16px; cursor:pointer; transition:0.3s;}
button:hover { background:#009fdf;}
body::before { content:'به ناسر چی پی تی خوش آمدید.'; position:fixed; top:10px; right:10px; font-size:20px; color:#555;}
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

async function sendMessage(){
  const text = input.value.trim();
  if(!text) return;

  // Benutzer-Nachricht
  const userMsg = document.createElement('div');
  userMsg.className='message user';
  userMsg.textContent=text;
  messages.appendChild(userMsg);
  input.value='';
  messages.scrollTop = messages.scrollHeight;

  // Bot tippt...
  const typing = document.createElement('div');
  typing.className='message bot';
  typing.textContent='NasserGPT schreibt...';
  messages.appendChild(typing);
  messages.scrollTop = messages.scrollHeight;

  try {
    const isPersian = /[\u0600-\u06FF]/.test(text);
    const systemMsg = isPersian ? "Du bist ein hilfreicher Assistent, antworte auf Persisch." : "Du bist ein hilfreicher Assistent, antworte auf Deutsch.";

    const response = await fetch('https://api.openai.com/v1/chat/completions',{
      method:'POST',
      headers:{
        'Content-Type':'application/json',
        'Authorization':'Bearer DEIN_API_KEY'
      },
      body: JSON.stringify({
        model:"gpt-3.5-turbo",
        messages:[
          {role:"system", content: systemMsg},
          {role:"user", content: text}
        ]
      })
    });

    const data = await response.json();
    typing.remove();
    const botMsg = document.createElement('div');
    botMsg.className='message bot';
    botMsg.textContent = data.choices[0].message.content;
    messages.appendChild(botMsg);
    messages.scrollTop = messages.scrollHeight;

  } catch(err){
    typing.remove();
    const botMsg = document.createElement('div');
    botMsg.className='message bot';
    botMsg.textContent='Fehler beim Abrufen der Antwort.';
    messages.appendChild(botMsg);
  }
}

// Enter-Taste senden
input.addEventListener('keydown', function(e){
  if(e.key==='Enter') sendMessage();
});
</script>

</body>
</html>
