# Farhangpt
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>FarhanGPT عبر OpenRouter</title>
  <style>
    body {
      font-family: Tahoma;
      background-color: #f4f4f4;
      padding: 20px;
      direction: rtl;
    }
    #chat {
      background: white;
      padding: 15px;
      height: 300px;
      overflow-y: scroll;
      border: 1px solid #ccc;
    }
    #userInput, button {
      padding: 10px;
      font-size: 16px;
    }
    #userInput {
      width: 75%;
    }
    button {
      width: 20%;
    }
  </style>
</head>
<body>

  <h2>FarhanGPT - واجهة تفاعلية</h2>
  <div id="chat"></div><br>
  <input type="text" id="userInput" placeholder="اكتب سؤالك...">
  <button onclick="sendMessage()">إرسال</button>

  <script>
    async function sendMessage() {
      const input = document.getElementById("userInput");
      const chat = document.getElementById("chat");
      const message = input.value;

      if (!message.trim()) return;

      chat.innerHTML += `<p><strong>أنت:</strong> ${message}</p>`;
      input.value = '';

      // استبدل بـ مفتاح API الخاص بك
      const API_KEY = "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";

      const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
        method: "POST",
        headers: {
          "Authorization": `Bearer ${API_KEY}`,
          "Content-Type": "application/json",
          "HTTP-Referer": "https://farhangpt.com",
          "X-Title": "FarhanGPT",
        },
        body: JSON.stringify({
          "model": "google/gemini-2.5-pro-preview-03-25",
          "messages": [{ "role": "user", "content": message }]
        })
      });

      const data = await response.json();

      if (response.ok) {
        const reply = data.choices[0].message.content;
        chat.innerHTML += `<p><strong>FarhanGPT:</strong> ${reply}</p>`;
      } else {
        chat.innerHTML += `<p><strong>خطأ:</strong> فشل في الاتصال.</p>`;
      }

      chat.scrollTop = chat.scrollHeight;
    }
  </script>

</body>
</html>
