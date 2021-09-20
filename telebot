import telebot

HELP = """Справка:
/help - напечатать справку
/add - добавить задачу
/print - вывести на экран
"""

print("Bot starting...")

todos = {}

TOKEN = '1977619074:AAFQ4sk123pCKkE_IX7S2GTdlD9_CLA42o0'
bot = telebot.TeleBot(TOKEN)

name1 = "ерге"
name2 = "Танюша"
name3 = "Ксю"
name4 = "💩"

def add_task (date,task):
 if date in todos:
      todos[date].append(task)
 else:
      todos[date]=[task]
 print(todos)


@bot.message_handler(commands=['help', 'HELP'])
def send_welcome(message):
	bot.reply_to(message, HELP)

@bot.message_handler(commands=['print'])
def print_tasks(message):
  date = message.text.split(' ')[1]
  if date in todos:
    text = f'Задачи на {date}:\n'
    for task in todos[date]:
      text = text + f'\n[] {task}'
    bot.send_message(message.chat.id, text)
  else:
    bot.send_message(message.chat.id, f'На дату {date} задач нет')


@bot.message_handler(commands=['add'])
def add(message):
    add_line = message.text.split(' ', maxsplit=2)
    date = add_line[1]
    task = add_line[2]
    add_task(date, task)
    bot.send_message(message.chat.id, f'Задача "{task}" добавлена на {date}')


@bot.message_handler(content_types=["text"])
def echo(message):
    if name1 in message.text:
        text = 'Привет, Сергей'
    elif name2 in message.text:
        text = 'Танюшка тоже молодец!'
    elif name3 in message.text:
        text = 'А ты, Ксюша, иди делай уроки, не мучай бота'
    elif name4 in message.text:
        text = 'Сама ты какашка!'
    else:
        text = message.text

    bot.send_message(message.chat.id, text)

bot.polling(none_stop=True)

