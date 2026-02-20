# index.jsconst express = require("express");
const axios = require("axios");

const app = express();
app.use(express.json());

// פרטי AliExpress שלך
const APP_KEY = "PASTE_YOUR_APP_KEY_HERE";
const APP_SECRET = "PASTE_YOUR_APP_SECRET_HERE";

// כתובת השרת שלך שמקבלת פוסטים
const CHAT_ENDPOINT = "https://YOUR-SERVER.com/api/import/post";
const CHAT_TOKEN = "987654321"; // אם יש לך טוקן אחר תשנה

app.get("/", (req, res) => {
  res.send("HotDeals bot is running 🚀");
});

// דוגמה שליחה ידנית לבדיקה
app.get("/test", async (req, res) => {
  try {
    await axios.post(
      CHAT_ENDPOINT,
      {
        text: "🔥 דיל בדיקה מ-AliExpress",
        author: "HotDeals Bot",
        timestamp: new Date().toISOString(),
      },
      {
        headers: {
          Authorization: `Bearer ${CHAT_TOKEN}`,
        },
      }
    );

    res.send("Message sent successfully");
  } catch (err) {
    res.status(500).send(err.message);
  }
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => console.log("Server running on port " + PORT));
