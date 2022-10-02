Тестирование основного функционала интернет магазина "Лабиринт"
'https://www.labirint.ru/'.

Структура проекта:

   - base:
      - seleniumbase.py - функции ожидания локаторов, используемые в разных тестах.
      - utils.py - утилиты для тестов.
   - pom:
       - home_page.py - локаторы и функции главной страницы.
   - папка tests:
      - test_page.py - тесты главной страницы.
      - screenshot: скриншоты тестов
          - 1_authorization
              - скриншоты авторизации
          - 2_home_page_header_personal
              - скриншоты меню персональный кабинет
          - 3_home_page_header_personal_button_my_maze
              - скриншоты кнопки мой лабиринт в меню персонального кабинета
   - conftest.py - фикстуры для тестов.
   - settings.py - тестовые данные для тестов.
   - requiremets.txt - используемые библиотеки.

---
Запуск тестов:

 - selenium - установить по пути path в операционной системе, в windows - C:\Windows\System32, так же тесты можно 
запускать через run test в PyCharm.
 - скачать selenium - https://chromedriver.storage.googleapis.com/(версия selenium для браузера)/
 - установка - pip3 install -r requirements
 - команда для терминала - pytest -s -v tests/test_page.py::/testClass/::/test/

___
Класс TestAuthorization - тестирование авторизации на сайте.
Тесты:
- test_auth_my_maze - тест полной авторизации на сайте с использованием кода скидки
полученной в рузультате ручной авторизации.

 - test_nav_link_email_positive - позитивный тест с использованием параметризации 
вводим код скидки используемый при авторизации, корректный номер телефона, корректный почтовый адрес,
проверка активнаная кнопка "Войти".

 - test_nav_link_email_negative - негативный тест с использованием параметризации 
проверки поля для ввода кода скидки, телефона, почты, вводимые данные в файле settings.py, 
в списке list_discount_phone_mail_negative, проверка неактивная кнопка "Войти".

 - test_nav_link_my_code_negative - негативный тест с использованием параметризации
проверки поля для ввода кода скидки, вводимые данные в файле settings.py, 
в списке list_my_discount_code_negative, проверка неактивная кнопка "проверить код и войти".

 - test_icons_auth_social_elements - тест проверки работоспособности иканок авторизации через социальные сети,
проверка скриншот страницы авторизации соц. сети в папке tests/screenshot/1_authorization/".

---
Класс TestHeaderMenuPersonal - Тест добавления товара в корзину.
Тесты:
 - test_header_personal_click - проверки меню сообщения мой лабиринт отложенно корзина проверка скриншоты в папке:
 tests/screenshot/2_home_page_header_personal

 - test_dropdown_menu_my_maze_click - тест проверки выпадающего меню мой лабиринт: заказы, вы смотрели, отложенные, баланс, настройки, выход
проверка скринщоты в папке: tests/screenshot/3_home_page_header_personal_button_my_maze

---
Класс TestAddingProduct - Тест проверки добавления товара в корзину, очистки крозины
Тесты:
 - test_adding_product_to_cart_first_book - Тест проверки добавления товара в корзину, проверка условия наличие товара на складе.
проверяем список товара в корзине не пустой, находимся на странице Корзина,
:return:сравневаем список товаров в корзине с тестовыми данными в переменой - LST_OF_POSTPONED_BOOKS.

 - test_adding_product_to_cart_second_book - Тест проверки добавления второго товара в корзину, проверка условия наличие товара на складе.
проверяем список товара в корзине не пустой, находимся на странице Корзина,
:return:сравневаем список товаров в корзине с тестовыми данными в переменой - LST_OF_POSTPONED_BOOKS.

 - test_removing_an_item_from_the_cart - Тест проверки удаления товара из корзины.
:return: сравниваем заголовок с текстом 'ВАША КОРЗИНА ПУСТА. ПОЧЕМУ?'.

---
Класс TestDeferredProduct - Тест проверки добавления книги в отложеные
Тесты:
 - test_addition_of_the_first_book - Тест добавление книги в отложеные, проверка книги на складе,
проверка в отложеных есть книга и находимся на странице отложеные.
:return: проверка название отложенной книги == название искомой книги

 - test_adding_a_second_book - Тест провенки добавление книги в отложеные если там уже есть книга,
проверка книги на складе, проверка в отложеных есть книга и находимся на странице отложеные.
:return: проверка название отложенной книги == название искомой книги

 - test_remove_books_from_deferred - Тест проверки удоления товаров из отложеного.
:return: сравниваем элемент с текстом.

---
Класс TestSearch - Тест поля "Поиска" на главной странице
Тесты:
 - test_search_relevance_check - Тест релевантности поиска по названию книги,
создаем список результатов поиска на главной странице, проверка - название и автор книги совпадают с ожидаемым рзультатом

 - test_book_russian_search - Тест проверки поле ввода Поиск используя параметризацию на русском языке,
даные ввода файл settings.py в списке list_of_values_in_the_search_field_rassian

 - test_book_english_search - Тест проверки поле ввода Поиск используя параметризацию на английском языке,
данные ввода файл settings.py в списке list_of_values_in_the_search_field_english

 - test_edgar_allan_poe_raven - Тест проверки нижнего предела поиска - осуществляем поиск по имени автора 'По Эдгар Аллан' и
названия книги 'Ворон', первый тест passed, остальные failed, даные ввода файл settings.py в списке 
list_of_values_in_the_search_field_edgar_allan_poe_raven, 

 - test_field_empty_spaces - Тест проверки поиска при пустом значении, при вводе одного пробела, двух пробелов

---
Класс TestHeaderMenu - Тест Header Menu
Тесты:
 - test_header_menu_click - Тест - проверки header menu выпадающий список кнопки еще, cd, сувениры, журналы, товары для дома.
:return: текст заголовка на странице соответствует странице из меню

 - test_header_menu_link_more - Тест - проверки header menu выпадающий список кнопки еще, cd, сувениры, журналы, товары для дома.
:return: текст заголовка на странице соответствует странице из меню

 - test_header_menu_link_delivery_region - Тест - проверки ссылки опрделения локации.
:return: проверяем видимость текста в элементе 'Укажите регион, чтобы мы точнее рассчитали условия доставки'

---
Класс TestSearchResultFilter - Тест фильтрации результатов поиска
Тесты:
 - test_search_filter - Тест проверки фильтрации поиска
:return: совпадение текста 'В КОРЗИНУ', 'ПРЕДЗАКАЗ', 'КУПИТЬ'