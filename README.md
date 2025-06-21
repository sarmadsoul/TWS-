import os
import telebot
import random
import time
import threading

BOT_TOKEN = os.getenv("BOT_TOKEN")
CHANNEL_USERNAME = "@trade_with_sarmad"

bot = telebot.TeleBot(BOT_TOKEN)

quotes = [
    "Discipline is doing what needs to be done, even if you don’t want to.",
    "Your soul needs peace more than your ego needs attention.",
    "Consistency is what transforms average into excellence.",
    "Strive not to be a man of success, but a man of value.",
    "Every step toward Allah is a step toward real success.",
    "Patience is bitter, but its fruit is sweet. – Prophet Muhammad ﷺ"
]

def send_post():
    while True:
        try:
            message = random.choice(quotes)
            bot.send_message(CHANNEL_USERNAME, f"🕊️ {message}")
        except Exception as e:
            print("Error sending message:", e)
        time.sleep(6 * 60 * 60)  # 6 hours

@bot.message_handler(commands=["start"])
def start_handler(message):
    bot.send_message(message.chat.id, "🕊️ Assalamu Alaikum, I'm your soul assistant.\nI will send peace, strength and motivation every day.")

@bot.message_handler(func=lambda m: True)
def reply_handler(message):
    if "🕊️" in message.text or "More Inspiration" in message.text:
        bot.send_message(message.chat.id, f"🕊️ {random.choice(quotes)}")

threading.Thread(target=send_post, daemon=True).start()

print("Bot is running...")
bot.polling()
