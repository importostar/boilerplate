---
title: bot_telegram
date: 2020-05-07
---
Example Python program bot_telegram.py
Python version 3.x or newer.
To check the Python version use:

    python --version

## Modules

* import telebot
* import const   # файл с токеном
* import os
* import random
* import urllib.request as urllib2
* from datetime import datetime
* >>>import telebot
* import config
* import telebot
* import config
* import telebot
* import telebot
* import sqlite3
* import shelve
* from SQLighter import SQLighter
* from config import shelve_name, database_name
* from random import shuffle
* import telebot
* import cherrypy
* import config
* import time
* import eventlet
* import requests
* import logging
* import telebot
* from time import sleep

## Classes

* class SQLighter:
* class WebhookServer(object):

## Methods

* def log(message,answer):
* def handle_start(message):
* def handle_start(message):
* def handle_text(message):
* def repeat_all_messages(message): # Название функции не играет никакой роли, в принципе
* def find_file_ids(message):
* def __init__(self, database):
* def select_all(self):
* def select_single(self, rownum):
* def count_rows(self):
* def close(self):
* def count_rows():
* def get_rows_count():
* def set_user_game(chat_id, estimated_answer):
* def finish_user_game(chat_id):
* def get_answer_for_user(chat_id):
* def generate_markup(right_answer, wrong_answers):
* def game(message):
* def check_answer(message):
* def index(self):
* def echo_message(message):
* def get_data():

## Code

Python example

    import telebot
    import const   # файл с токеном
    import os
    import random
    import urllib.request as urllib2
    
    bot=telebot.TeleBot(const.token)
    
    # bot.send_message("chat_id","test")
    
    #upd=bot.get_updates()
    # print(upd)
    
    #last_upd=upd[-1]
    #message_from_user=last_upd.message
    #print(message_from_user)
    print(bot.get_me())
    def log(message,answer):
        print("\n --------")
        from datetime import datetime
        print(datetime.now())
        print("Сообщение от {0} {1}. (id={2}) \n Текст={3}" .format(message.from_user.first_name,
                                                                  message.from_user.last_name,
                                                                  str(message.from_user.id),
                                                                  message.text))
        print(answer)
    
    @bot.message_handler(commands=['start'])
    def handle_start(message):
        user_markup=telebot.types.ReplyKeyboardMarkup(True,True)
        user_markup.row('/start','/stop')
        user_markup.row('фото', 'аудио','документы')
        user_markup.row('стикер', 'видео','голос','локация')
        bot.send_message(message.from_user.id,'Добро пожаловать..', reply_markup=user_markup)
    
    @bot.message_handler(commands=['stop'])
    def handle_start(message):
           hide_markup = telebot.types.ReplyKeyboardMarkup()
           bot.send_message(message.from_user.id,'..',reply_markup=hide_markup)
    
    @bot.message_handler(content_types=['text'])
    def handle_text(message):
        answer = "Я вас не понимаю"
        if message.text=="прт":
            answer = "И вам привет)"
            log(message,answer)
            bot.send_message(message.chat.id,"""\r
            <b>И вам привет)</b>""",parse_mode="HTML")
        elif message.text=="фото":
            #all_files = os.listdir(directory)
            #random_file = random.choice(all_files)
            url = "фото1"
            urllib2.urlretrieve(url,'url_image.jpg')
            #img = open(directory + '/' + random_file, 'rb')
            img = open('url_image.jpg', 'rb')
            bot.send_chat_action(message.from_user.id,'upload_photo')
            bot.send_photo(message.from_user.id,img)
            img.close()
        elif message.text == "локация":
            bot.send_chat_action(message.from_user.id, 'find_location')
            bot.send_location(message.from_user.id, широта, долгота)
        else:
            bot.send_message(message.chat.id, answer)
            log(message,answer)
    bot.polling(none_stop=True, interval=0)
    
    ================Бот повторюша с помощью long polling######
    подключаем библиотеку
    pip install pytelegrambotapi
    подключаем pip3 для установки правильной версии. 
    python3
    >>>import telebot
    #config.py
    # Этот токен невалидный, можете даже не пробовать :)
    token = '110831855:AAE_GbIeVAUwk11O12vq4UeMnl20iADUtM'
    
    #bot.py
    # -*- coding: utf-8 -*-
    import config
    import telebot
    
    bot = telebot.TeleBot(config.token)
    #про хэндлеры
    # При написании ботов создают "слушателя", в котором обрабатывали входящее сообщение. 
    # Это, несомненно, круто, но как только наш бот начинает расти, это становится проблемой. 
    # В огромном количестве конструкций if-elif-else можно легко запутаться.
    # Для решения этой проблемы автор библиотеки написал хэндлеры (или декораторы, кому как проще).
    # Таким образом, мы можем разнести код по различным функциям и не кучковать его в одном месте, что повышает читабельность.
    # Обратите внимание: декораторы будут проверяться в порядке их следования в коде, по принципу "какой первый подошел, тот и используем".
    # Под "подошел" будем понимать равенство нашей лямбда-функции значению True.
    
    
    # -*- coding: utf-8 -*-
    import config
    import telebot
    
    bot = telebot.TeleBot(config.token)
    
     # Обработчик для текста
    @bot.message_handler(content_types=["text"])
    def repeat_all_messages(message): # Название функции не играет никакой роли, в принципе
        bot.send_message(message.chat.id, message.text)
    
    #Теперь запустим бесконечный цикл получения новых записей со стороны Telegram:
    
    if __name__ == '__main__':
         bot.polling(none_stop=True)
    #Функция polling запускает т.н. Long Polling, а параметр none_stop=True говорит, что бот должен стараться не прекращать работу при возникновении каких-либо ошибок 
    
    запуск python3 bot.py
    
    ###################Угадай мелодию####################
    #Попросим нашего бота прислать нам наши аудиофайлы и их file_id
    #5 никому не известных песен, сделал из них 15-20-секундные нарезки, сконвертировал в *.ogg и положил в папку "music". 
    #bot.py
    #Идентификаторы file_id уникальны для каждого бота по отдельности
    # -*- coding: utf-8 -*-
    import telebot
    
    bot = telebot.TeleBot(config.token)
    
    @bot.message_handler(commands=['test'])
    def find_file_ids(message):
        for file in os.listdir('music/'):
            if file.split('.')[-1] == 'ogg':
                f = open('music/'+file, 'rb')
                msg = bot.send_voice(message.chat.id, f, None)
                # А теперь отправим вслед за файлом его file_id
                bot.send_message(message.chat.id, msg.voice.file_id, reply_to_message_id=msg.message_id)
            time.sleep(3)
    
    
    if __name__ == '__main__':
        bot.polling(none_stop=True)
        
    #БД SQLite3
    #sqlite3 music.db <ttt.sql
    таблица music
    id file_id right_answer wrong_answer
    #SQLighter.py
    #При каждом создании объекта SQLighter будет открываться отдельное соединение с БД и впоследствии закрываться
    import sqlite3
    
    class SQLighter:
    
        def __init__(self, database):
            self.connection = sqlite3.connect(database)
            self.cursor = self.connection.cursor()
    
        def select_all(self):
            """ Получаем все строки """
            with self.connection:
                return self.cursor.execute('SELECT * FROM music').fetchall()
    
        def select_single(self, rownum):
            """ Получаем одну строку с номером rownum """
            with self.connection:
                return self.cursor.execute('SELECT * FROM music WHERE id = ?', (rownum,)).fetchall()[0]
    
        def count_rows(self):
            """ Считаем количество строк """
            with self.connection:
                result = self.cursor.execute('SELECT * FROM music').fetchall()
                return len(result)
    
        def close(self):
            """ Закрываем текущее соединение с БД """
            self.connection.close()
            
    #shelve
    # Создадим файл utils.py, в котором опишем методы для сохранения правильного ответа,
    # удаления правильного ответа, получения правильного ответа (или None, если юзер решил просто так что-то написать боту) 
    # и сохранении количества строк в основной БД. Количество строк будет пересчитываться при каждом запуске бота, тем самым, 
    # нам не надо думать, по какому правилу выбирать вопросы.
    #utils.py
    #использование ключевого слова with: оно позволяет не заморачиваться о закрытии хранилища, Python сам возьмет на себя управление
    
    # -*- coding: utf-8 -*-
    import shelve
    from SQLighter import SQLighter
    from config import shelve_name, database_name
    
    def count_rows():
        """
        Данный метод считает общее количество строк в базе данных и сохраняет в хранилище.
        Потом из этого количества будем выбирать музыку.
        """
        db = SQLighter(database_name)
        rowsnum = db.count_rows()
        with shelve.open(shelve_name) as storage:
            storage['rows_count'] = rowsnum
    
    
    def get_rows_count():
        """
        Получает из хранилища количество строк в БД
        :return: (int) Число строк
        """
        with shelve.open(shelve_name) as storage:
            rowsnum = storage['rows_count']
        return rowsnum
    
    
    def set_user_game(chat_id, estimated_answer):
        """
        Записываем юзера в игроки и запоминаем, что он должен ответить.
        :param chat_id: id юзера
        :param estimated_answer: правильный ответ (из БД)
        """
        with shelve.open(shelve_name) as storage:
            storage[str(chat_id)] = estimated_answer
    
    
    def finish_user_game(chat_id):
        """
        Заканчиваем игру текущего пользователя и удаляем правильный ответ из хранилища
        :param chat_id: id юзера
        """
        with shelve.open(shelve_name) as storage:
            del storage[str(chat_id)]
    
    
    def get_answer_for_user(chat_id):
        """
        Получаем правильный ответ для текущего юзера.
        В случае, если человек просто ввёл какие-то символы, не начав игру, возвращаем None
        :param chat_id: id юзера
        :return: (str) Правильный ответ / None
        """
        with shelve.open(shelve_name) as storage:
            try:
                answer = storage[str(chat_id)]
                return answer
            # Если человек не играет, ничего не возвращаем
            except KeyError:
                return None
            
    #config.py
    # -*- coding: utf-8 -*-
    token = 'YOUR_TOKEN'  # Токен бота
    database_name = 'music.db'  # Файл с базой данных
    shelve_name = 'shelve.db'  # Файл с хранилищем
    
    #добавим кастомную клаву с вариантами ответа в utils.py
    
    from random import shuffle
    
    def generate_markup(right_answer, wrong_answers):
        """
        Создаем кастомную клавиатуру для выбора ответа
        :param right_answer: Правильный ответ
        :param wrong_answers: Набор неправильных ответов
        :return: Объект кастомной клавиатуры
        """
        markup = types.ReplyKeyboardMarkup(one_time_keyboard=True, resize_keyboard=True)
        # Склеиваем правильный ответ с неправильными
        all_answers = '{},{}'.format(right_answer, wrong_answers)
        # Создаем лист (массив) и записываем в него все элементы
        list_items = []
        for item in all_answers.split(','):
            list_items.append(item)
        # Хорошенько перемешаем все элементы
        shuffle(list_items)
        # Заполняем разметку перемешанными элементами
        for item in list_items:
            markup.add(item)
        return markup
    
        #bot.py
        bot = telebot.TeleBot(config.token)
        
    @bot.message_handler(commands=['game'])
    def game(message):
        # Подключаемся к БД
        db_worker = SQLighter(config.database_name)
        # Получаем случайную строку из БД
        row = db_worker.select_single(random.randint(1, utils.get_rows_count()))
        # Формируем разметку
        markup = utils.generate_markup(row[2], row[3])
        # Отправляем аудиофайл с вариантами ответа
        bot.send_voice(message.chat.id, row[1], reply_markup=markup)
        # Включаем "игровой режим"
        utils.set_user_game(message.chat.id, row[2])
        # Отсоединяемся от БД
        db_worker.close()
        
        
    @bot.message_handler(func=lambda message: True, content_types=['text'])
    def check_answer(message):
        # Если функция возвращает None -> Человек не в игре
        answer = utils.get_answer_for_user(message.chat.id)
        # Как Вы помните, answer может быть либо текст, либо None
        # Если None:
        if not answer:
            bot.send_message(message.chat.id, 'Чтобы начать игру, выберите команду /game')
        else:
            # Уберем клавиатуру с вариантами ответа.
            keyboard_hider = types.ReplyKeyboardRemove()
            # Если ответ правильный/неправильный
            if message.text == answer:
                bot.send_message(message.chat.id, 'Верно!', reply_markup=keyboard_hider)
            else:
                bot.send_message(message.chat.id, 'Увы, Вы не угадали. Попробуйте ещё раз!', reply_markup=keyboard_hider)
            # Удаляем юзера из хранилища (игра закончена)
            utils.finish_user_game(message.chat.id)   
            
       if __name__ == '__main__':
        utils.count_rows()
        random.seed()
        bot.polling(none_stop=True)
        
        #################Веб хук######################
        sudo apt-get install openssl
        #сгенерируем приватный ключ: 
        openssl genrsa -out webhook_pkey.pem 2048
        # генерируем самоподписанный сертификат
        openssl req -new -x509 -days 3650 -key webhook_pkey.pem -out webhook_cert.pem
        #Common Name, следует написать IP адрес сервера, на котором будет запущен бот.
        #создаст файлы webhook_cert.pem и webhook_pkey.pem
        #необходимость наличия веб-сервера, для работы с вебхуками
        #используем веб-фреймворк CherryPy
        python3.4 -m pip install cherryp
        #bot.py
        #!/usr/bin/python3.4
    # -*- coding: utf-8 -*-
    import telebot
    import cherrypy
    import config
    
    WEBHOOK_HOST = 'IP-адрес сервера, на котором запущен бот'
    WEBHOOK_PORT = 443  # 443, 80, 88 или 8443 (порт должен быть открыт!)
    WEBHOOK_LISTEN = '0.0.0.0'  # На некоторых серверах придется указывать такой же IP, что и выше
    
    WEBHOOK_SSL_CERT = './webhook_cert.pem'  # Путь к сертификату
    WEBHOOK_SSL_PRIV = './webhook_pkey.pem'  # Путь к приватному ключу
    
    WEBHOOK_URL_BASE = "https://%s:%s" % (WEBHOOK_HOST, WEBHOOK_PORT)
    WEBHOOK_URL_PATH = "/%s/" % (config.token)
    
    bot = telebot.TeleBot(config.token)
    
    # Наш вебхук-сервер
    #  Принимаем входящие запросы по URL наш.ip.адрес/, 
    #  получаем содержимое и прогоняем через набор хэндлеров
    class WebhookServer(object):
        @cherrypy.expose
        def index(self):
            if 'content-length' in cherrypy.request.headers and \
                            'content-type' in cherrypy.request.headers and \
                            cherrypy.request.headers['content-type'] == 'application/json':
                length = int(cherrypy.request.headers['content-length'])
                json_string = cherrypy.request.body.read(length).decode("utf-8")
                update = telebot.types.Update.de_json(json_string)
                # Эта функция обеспечивает проверку входящего сообщения
                bot.process_new_updates([update])
                return ''
            else:
                raise cherrypy.HTTPError(403)
                
    # Хэндлер на все текстовые сообщения
    @bot.message_handler(func=lambda message: True, content_types=['text'])
    def echo_message(message):
        bot.reply_to(message, message.text)
      
    #отправим серверу наш самоподписанный сертификат и "обратный адрес", по которому просим сообщать обо всех новых сообщениях:
    # Снимаем вебхук перед повторной установкой (избавляет от некоторых проблем)
    bot.remove_webhook()
    
     # Ставим заново вебхук
    bot.set_webhook(url=WEBHOOK_URL_BASE + WEBHOOK_URL_PATH,
                    certificate=open(WEBHOOK_SSL_CERT, 'r'))
    # укажем настройки нашего сервера и запустим его!
    cherrypy.config.update({
        'server.socket_host': WEBHOOK_LISTEN,
        'server.socket_port': WEBHOOK_PORT,
        'server.ssl_module': 'builtin',
        'server.ssl_certificate': WEBHOOK_SSL_CERT,
        'server.ssl_private_key': WEBHOOK_SSL_PRIV
    })
    
     # Собственно, запуск!
    cherrypy.quickstart(WebhookServer(), WEBHOOK_URL_PATH, {'/': {}})
    ###################Постинг ВК групп в каналы #######################################
    #последние 10 записей от имени сообщества из группы C:\Music
    https://api.vk.com/method/wall.get?domain=c.music&count=10&filter=owner&access_token=token
    #bot.py
    # -*- coding: utf-8 -*-
    
    import time
    import eventlet
    import requests
    import logging
    import telebot
    from time import sleep
    
     # Каждый раз получаем по 10 последних записей со стены
    #     Во-первых, не забудьте сделать нужного бота администратором канала, иначе фокус не удастся.
    #     Во-вторых, обратите внимание, что в импортах появилась библиотека eventlet,
    #     она поможет нам избежать проблем при получении записей из ВК. 
    #     В-третьих, в указанный txt-файл будем записывать номер верхнего поста на момент проверки, 
    #     я решил не заморачиваться с созданием key-value хранилищ, ради одного числа-то.
    #     В-четвёртых, в качестве параметра BASE_POST_URL указываем ссылку на любой пост из нашей группы без последнего числа.
        
    URL_VK = 'https://api.vk.com/method/wall.get?domain=c.music&count=10&filter=owner&access_token=Ваш_токен_VK'
    FILENAME_VK = 'last_known_id.txt'
    BASE_POST_URL = 'https://vk.com/wall-39270586_'
    
    BOT_TOKEN = 'токен бота, постящего в канал'
    CHANNEL_NAME = '@канал'
    
    bot = telebot.TeleBot(BOT_TOKEN)
    
    # Иногда ВК начинает дурить и не возвращает список постов за приемлемое время.
    # В этом случае, нам нужно отвалиться по таймауту и пропустить проверку.
    # Можно, конечно, попробовать ещё раз, но мы люди не настойчивые :)
    
    def get_data():
        timeout = eventlet.Timeout(10)
        try:
            feed = requests.get(URL_VK)
            return feed.json()
        except eventlet.timeout.Timeout:
            logging.warning('Got Timeout while retrieving VK JSON data. Cancelling...')
            return None
        finally:
            timeout.cancel()
    
    

## Useful Links

- Articles: https://python-commandments.org/
- Python shell: https://bsdnerds.org/learn-python/
- Tutorial: https://pythonprogramminglanguage.com/
