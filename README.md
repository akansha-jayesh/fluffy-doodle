# fluffy-doodleimport os
import telebot
import requests
from dotenv import load_dotenv

load_dotenv()
BOT_TOKEN = os.getenv("BOT_TOKEN")
OMDB_API_KEY = os.getenv("OMDB_API_KEY")
ADMIN_ID = os.getenv("ADMIN_ID")  # Your Telegram user ID

bot = telebot.TeleBot(BOT_TOKEN)

# GPT Fake Response (Can integrate OpenAI later)
def gpt_reply(msg):
    return f"Jayesh bhai, yeh GPT reply hai: '{msg}' ka jawab love se!"

# Movie Search
def get_movie(name):
    url = f"http://www.omdbapi.com/?t={name}&apikey={OMDB_API_KEY}"
    res = requests.get(url).json()
    if res.get("Response") == "True":
        return f"🎬 *{res['Title']}*\n⭐ {res['imdbRating']}/10\n📝 {res['Plot']}\n📅 {res['Year']}", res['Poster']
    else:
        return "Movie nahi mila bhai!", None

# Shayari Collection
shayari_romantic = [
    "Tumse juda ho kar jee nahi paayenge hum 💔",
    "Tere bina har pal adhoora lagta hai 💕"
]
shayari_adult = [
    "Jab tu paas hoti hai, har ang mere jazbaat bolte hain 🔥",
    "Tere hothon pe likhi hai meri har raaz ki dastaan 💋"
]

# YouTube song search (simple)
def song_search(query):
    return f"🔗 YouTube pe search karo: https://www.youtube.com/results?search_query={query.replace(' ', '+')}"

# Start Command
@bot.message_handler(commands=['start'])
def start_msg(msg):
    bot.reply_to(msg, "JayAkanshaBot activated! 🔥 Use /gpt, /movie, /shayari, /sexy, /song, /manage")

# GPT
@bot.message_handler(commands=['gpt'])
def handle_gpt(msg):
    text = msg.text.replace('/gpt', '').strip()
    if text:
        reply = gpt_reply(text)
        bot.reply_to(msg, reply)
    else:
        bot.reply_to(msg, "Bhai, /gpt ke baad kuch likh toh sahi!")

# Movie
@bot.message_handler(commands=['movie'])
def handle_movie(msg):
    name = msg.text.replace('/movie', '').strip()
    if not name:
        bot.reply_to(msg, "Movie ka naam toh de bhai!")
        return
    result, poster = get_movie(name)
    if poster:
        bot.send_photo(msg.chat.id, poster, caption=result, parse_mode='Markdown')
    else:
        bot.reply_to(msg, result)

# Shayari
@bot.message_handler(commands=['shayari'])
def romantic(msg):
    import random
    bot.reply_to(msg, random.choice(shayari_romantic))

@bot.message_handler(commands=['sexy'])
def adult(msg):
    import random
    bot.reply_to(msg, f"Akansha ke liye special 🔥\n\n{random.choice(shayari_adult)}")

# Song
@bot.message_handler(commands=['song'])
def handle_song(msg):
    song = msg.text.replace('/song', '').strip()
    if not song:
        bot.reply_to(msg, "Gaana ka naam de bhai!")
        return
    link = song_search(song)
    bot.reply_to(msg, link)

# Admin management
@bot.message_handler(commands=['manage'])
def manage_bot(msg):
    if str(msg.from_user.id) != ADMIN_ID:
        bot.reply_to(msg, "Tu admin nahi hai bhai! ❌")
        return
    bot.reply_to(msg, "Admin commands: /shutdown (manual stop)")

@bot.message_handler(commands=['shutdown'])
def shutdown(msg):
    if str(msg.from_user.id) == ADMIN_ID:
        bot.reply_to(msg, "Bot bandh ho raha hai 💀")
        exit()
    else:
        bot.reply_to(msg, "Admin command hai bhai!")

# Fallback
@bot.message_handler(func=lambda m: True)
def echo(msg):
    bot.reply_to(msg, f"Jayesh bhai, command samajh nahi aayi: {msg.text}")

bot.infinity_polling()import os
import telebot
import requests
from dotenv import load_dotenv

load_dotenv()
BOT_TOKEN = os.getenv("BOT_TOKEN")
OMDB_API_KEY = os.getenv("OMDB_API_KEY")
ADMIN_ID = os.getenv("ADMIN_ID")  # Your Telegram user ID

bot = telebot.TeleBot(BOT_TOKEN)

# GPT Fake Response (Can integrate OpenAI later)
def gpt_reply(msg):
    return f"Jayesh bhai, yeh GPT reply hai: '{msg}' ka jawab love se!"

# Movie Search
def get_movie(name):
    url = f"http://www.omdbapi.com/?t={name}&apikey={OMDB_API_KEY}"
    res = requests.get(url).json()
    if res.get("Response") == "True":
        return f"🎬 *{res['Title']}*\n⭐ {res['imdbRating']}/10\n📝 {res['Plot']}\n📅 {res['Year']}", res['Poster']
    else:
        return "Movie nahi mila bhai!", None

# Shayari Collection
shayari_romantic = [
    "Tumse juda ho kar jee nahi paayenge hum 💔",
    "Tere bina har pal adhoora lagta hai 💕"
]
shayari_adult = [
    "Jab tu paas hoti hai, har ang mere jazbaat bolte hain 🔥",
    "Tere hothon pe likhi hai meri har raaz ki dastaan 💋"
]

# YouTube song search (simple)
def song_search(query):
    return f"🔗 YouTube pe search karo: https://www.youtube.com/results?search_query={query.replace(' ', '+')}"

# Start Command
@bot.message_handler(commands=['start'])
def start_msg(msg):
    bot.reply_to(msg, "JayAkanshaBot activated! 🔥 Use /gpt, /movie, /shayari, /sexy, /song, /manage")

# GPT
@bot.message_handler(commands=['gpt'])
def handle_gpt(msg):
    text = msg.text.replace('/gpt', '').strip()
    if text:
        reply = gpt_reply(text)
        bot.reply_to(msg, reply)
    else:
        bot.reply_to(msg, "Bhai, /gpt ke baad kuch likh toh sahi!")

# Movie
@bot.message_handler(commands=['movie'])
def handle_movie(msg):
    name = msg.text.replace('/movie', '').strip()
    if not name:
        bot.reply_to(msg, "Movie ka naam toh de bhai!")
        return
    result, poster = get_movie(name)
    if poster:
        bot.send_photo(msg.chat.id, poster, caption=result, parse_mode='Markdown')
    else:
        bot.reply_to(msg, result)

# Shayari
@bot.message_handler(commands=['shayari'])
def romantic(msg):
    import random
    bot.reply_to(msg, random.choice(shayari_romantic))

@bot.message_handler(commands=['sexy'])
def adult(msg):
    import random
    bot.reply_to(msg, f"Akansha ke liye special 🔥\n\n{random.choice(shayari_adult)}")

# Song
@bot.message_handler(commands=['song'])
def handle_song(msg):
    song = msg.text.replace('/song', '').strip()
    if not song:
        bot.reply_to(msg, "Gaana ka naam de bhai!")
        return
    link = song_search(song)
    bot.reply_to(msg, link)

# Admin management
@bot.message_handler(commands=['manage'])
def manage_bot(msg):
    if str(msg.from_user.id) != ADMIN_ID:
        bot.reply_to(msg, "Tu admin nahi hai bhai! ❌")
        return
    bot.reply_to(msg, "Admin commands: /shutdown (manual stop)")

@bot.message_handler(commands=['shutdown'])
def shutdown(msg):
    if str(msg.from_user.id) == ADMIN_ID:
        bot.reply_to(msg, "Bot bandh ho raha hai 💀")
        exit()
    else:
        bot.reply_to(msg, "Admin command hai bhai!")

# Fallback
@bot.message_handler(func=lambda m: True)
def echo(msg):
    bot.reply_to(msg, f"Jayesh bhai, command samajh nahi aayi: {msg.text}")

bot.infinity_polling()import os
import telebot
import requests
from dotenv import load_dotenv

load_dotenv()
BOT_TOKEN = os.getenv("BOT_TOKEN")
OMDB_API_KEY = os.getenv("OMDB_API_KEY")
ADMIN_ID = os.getenv("ADMIN_ID")  # Your Telegram user ID

bot = telebot.TeleBot(BOT_TOKEN)

# GPT Fake Response (Can integrate OpenAI later)
def gpt_reply(msg):
    return f"Jayesh bhai, yeh GPT reply hai: '{msg}' ka jawab love se!"

# Movie Search
def get_movie(name):
    url = f"http://www.omdbapi.com/?t={name}&apikey={OMDB_API_KEY}"
    res = requests.get(url).json()
    if res.get("Response") == "True":
        return f"🎬 *{res['Title']}*\n⭐ {res['imdbRating']}/10\n📝 {res['Plot']}\n📅 {res['Year']}", res['Poster']
    else:
        return "Movie nahi mila bhai!", None

# Shayari Collection
shayari_romantic = [
    "Tumse juda ho kar jee nahi paayenge hum 💔",
    "Tere bina har pal adhoora lagta hai 💕"
]
shayari_adult = [
    "Jab tu paas hoti hai, har ang mere jazbaat bolte hain 🔥",
    "Tere hothon pe likhi hai meri har raaz ki dastaan 💋"
]

# YouTube song search (simple)
def song_search(query):
    return f"🔗 YouTube pe search karo: https://www.youtube.com/results?search_query={query.replace(' ', '+')}"

# Start Command
@bot.message_handler(commands=['start'])
def start_msg(msg):
    bot.reply_to(msg, "JayAkanshaBot activated! 🔥 Use /gpt, /movie, /shayari, /sexy, /song, /manage")

# GPT
@bot.message_handler(commands=['gpt'])
def handle_gpt(msg):
    text = msg.text.replace('/gpt', '').strip()
    if text:
        reply = gpt_reply(text)
        bot.reply_to(msg, reply)
    else:
        bot.reply_to(msg, "Bhai, /gpt ke baad kuch likh toh sahi!")

# Movie
@bot.message_handler(commands=['movie'])
def handle_movie(msg):
    name = msg.text.replace('/movie', '').strip()
    if not name:
        bot.reply_to(msg, "Movie ka naam toh de bhai!")
        return
    result, poster = get_movie(name)
    if poster:
        bot.send_photo(msg.chat.id, poster, caption=result, parse_mode='Markdown')
    else:
        bot.reply_to(msg, result)

# Shayari
@bot.message_handler(commands=['shayari'])
def romantic(msg):
    import random
    bot.reply_to(msg, random.choice(shayari_romantic))

@bot.message_handler(commands=['sexy'])
def adult(msg):
    import random
    bot.reply_to(msg, f"Akansha ke liye special 🔥\n\n{random.choice(shayari_adult)}")

# Song
@bot.message_handler(commands=['song'])
def handle_song(msg):
    song = msg.text.replace('/song', '').strip()
    if not song:
        bot.reply_to(msg, "Gaana ka naam de bhai!")
        return
    link = song_search(song)
    bot.reply_to(msg, link)

# Admin management
@bot.message_handler(commands=['manage'])
def manage_bot(msg):
    if str(msg.from_user.id) != ADMIN_ID:
        bot.reply_to(msg, "Tu admin nahi hai bhai! ❌")
        return
    bot.reply_to(msg, "Admin commands: /shutdown (manual stop)")

@bot.message_handler(commands=['shutdown'])
def shutdown(msg):
    if str(msg.from_user.id) == ADMIN_ID:
        bot.reply_to(msg, "Bot bandh ho raha hai 💀")
        exit()
    else:
        bot.reply_to(msg, "Admin command hai bhai!")

# Fallback
@bot.message_handler(func=lambda m: True)
def echo(msg):
    bot.reply_to(msg, f"Jayesh bhai, command samajh nahi aayi: {msg.text}")

bot.infinity_polling()
