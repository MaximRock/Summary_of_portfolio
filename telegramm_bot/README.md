Бот для конвертации валют.

При выборе "Меню без кнопок" бот работает как описано в модуле 18.6..
При выборе "Меню с кнопками" бот работает на кнопках.

При вводе или не верном выборе, появляются предупреждающие сообщения бота.
Отрицательное или нулевое значение валюты - бот выдает предупреждение.
После предложения ввести валюту бот принимает на ввод только значение валюты
из списка.

Файл /bot.py - собственно сам бот

Файл /config.py - конфигурационный

файлы /extenButtons.py /extensions.py - исключения для варианта с кнопками и без кнопок

файл /markup.py - меню кнопок