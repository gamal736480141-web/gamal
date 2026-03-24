<!DOCTYPE html>
<html lang="ar">
<head>
<meta charset="UTF-8">
<title>AI App</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: "Cairo", Arial;
    background: #000; /* خلفية سوداء */
    color: #00ff88; /* لون أخضر */
    text-align: center;
}

/* العنوان */
.header {
    padding: 15px;
    font-size: 20px;
    border-bottom: 1px solid #00ff88;
    background: #000;
}

/* الحاوية */
.container {
    max-width: 700px;
    margin: 30px auto;
    padding: 20px;
    border: 1px solid #00ff88;
    border-radius: 15px;
    box-shadow: 0 0 15px #00ff88;
}

/* المدخلات */
input {
    width: 90%;
    padding: 12px;
    margin: 10px;
    border-radius: 10px;
    border: 1px solid #00ff88;
    background: #000;
    color: #00ff88;
}

/* الأزرار */
button {
    padding: 12px 20px;
    margin: 10px;
    border-radius: 10px;
    border: 1px solid #00ff88;
    background: #000;
    color: #00ff88;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #00ff88;
    color: #000;
}

/* الشات */
#chatBox {
    background: #000;
    height: 300px;
    overflow-y: auto;
    padding: 10px;
    border-radius: 10px;
    border: 1px solid #00ff88;
    text-align: right;
}

/* الرسائل */
.msg-user {
    color: #00ff88;
    margin: 5px 0;
}

.msg-ai {
    color: #00cc66;
    margin: 5px 0;
}

/* الصور */
img {
    width: 100%;
    border-radius: 10px;
    margin-top: 10px;
    border: 1px solid #00ff88;
}
</style>

</head>
<body>

<div class="header">
💚 تم إنشاء هذا التطبيق من قبل المهندس جمال الحبشي 💚
</div>

<div class="container">

    <h2>🤖 تطبيق الذكاء الاصطناعي</h2>

    <input type="password" id="apiKey" placeholder="أدخل API KEY">

    <h3>💬 الدردشة</h3>
    <div id="chatBox"></div>

    <input type="text" id="userInput" placeholder="اكتب رسالتك...">
    <button onclick="sendMessage()">إرسال</button>

    <h3>🎨 توليد الصور</h3>
    <input type="text" id="imagePrompt" placeholder="اكتب وصف الصورة">
    <button onclick="generateImage()">توليد صورة</button>

    <div id="imageResult"></div>

</div>

<script>

// إضافة رسالة
function addMessage(text, type) {
    const chatBox = document.getElementById("chatBox");
    const msg = document.createElement("div");

    msg.className = type === "user" ? "msg-user" : "msg-ai";
    msg.innerText = text;

    chatBox.appendChild(msg);
    chatBox.scrollTop = chatBox.scrollHeight;
}

// إرسال رسالة
async function sendMessage() {
    const input = document.getElementById("userInput").value;
    const apiKey = document.getElementById("apiKey").value;

    if (!input || !apiKey) {
        alert("أدخل النص و API KEY");
        return;
    }

    addMessage("أنت: " + input, "user");

    const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": "Bearer " + apiKey
        },
        body: JSON.stringify({
            model: "gpt-4o-mini",
            messages: [{ role: "user", content: input }]
        })
    });

    const data = await response.json();
    const reply = data.choices?.[0]?.message?.content || "حدث خطأ";

    addMessage("AI: " + reply, "ai");
}

// توليد صورة
async function generateImage() {
    const prompt = document.getElementById("imagePrompt").value;
    const apiKey = document.getElementById("apiKey").value;

    if (!prompt || !apiKey) {
        alert("أدخل الوصف و API KEY");
        return;
    }

    const resultDiv = document.getElementById("imageResult");
    resultDiv.innerHTML = "⏳ جاري التوليد...";

    const response = await fetch("https://api.openai.com/v1/images/generations", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": "Bearer " + apiKey
        },
        body: JSON.stringify({
            model: "gpt-image-1",
            prompt: prompt,
            size: "1024x1024"
        })
    });

    const data = await response.json();
    const imageUrl = data.data?.[0]?.url;

    if (imageUrl) {
        resultDiv.innerHTML = `<img src="${imageUrl}">`;
    } else {
        resultDiv.innerHTML = "❌ فشل توليد الصورة";
    }
}

</script>

</body>
</html>
