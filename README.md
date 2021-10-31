# Telegram_bot-PogodaBot
from pyowm.owm import OWM
from pyowm.utils.config import get_default_config
import pyowm
import telebot
import telebot

config_dict = get_default_config()
config_dict['language'] = 'ru'  
owm = pyowm.OWM('58a41fc57491f76397dbe5111e457541') 
mgr  =  owm . weather_manager ()
bot = telebot.TeleBot("2095532057:AAG7UMwtEduCGqgrBMoHLiZeMuUhmaIInZU")


@bot.message_handler(content_types=['text'])
def send_echo(message):
    observation = mgr.weather_at_place( message.text )
    w = observation.weather
    temp = w.temperature('celsius')["temp"]

    answer = "В городе " + message.text +" сейчас " + w.detailed_status + "\n"
    answer += "Температура сейчас в районе " + str(temp) + "\n\n" 

    if temp < 0:
        answer += "Сейчас ппц как холодно, одевайся как танк!"

    elif temp < 10:
       answer += "Сейчас не достаточно тепло для шорт и футболки, одевайся не много теплей!"

    elif temp > 20:
       answer += "Пора выпускать футболочку на прогулочку"

    bot.send_message(message.chat.id,answer) 
	

bot.polling( none_stop = True )

apihelper.SESSION_TIME_TO_LIVE = 5 * 60



input()

