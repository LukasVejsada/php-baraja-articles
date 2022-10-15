Огляд знань з веб-розробки
==========================

> id: e5e9613c-66fe-4d5e-a686-a182aab8061a
> slug:
> 	cs: znalosti
> 	uk: oglyad-znan-z-veb-rozrobki
> 
> publicationDate: '2019-09-11 10:07:07'
> mainCategoryId: '6cbbbf59-9bbd-4ca3-a6c3-eb204a2f8070'
> sourceContentHash: b7284b1fc11b40ddb7628995070198a1

Знати, як створити сайт і потім всебічно піклуватися про нього, - це не просто вміти його зробити. На цьому шляху є багато перешкод, і добре мати хоча б базове уявлення про кожну з них. Коли я починав, я не знав, що саме потрібно вивчати. Ця сторінка слугує своєрідним дороговказом через теми, які мені довелося поступово вивчати, щоб мати змогу розбиратися у веб-розробці та розбиратися у найбільш поширених ситуаціях.

Адміністрування серверів
--------------

> Веб-сервер - це комп'ютер, на якому працює Інтернет. Коли користувач переглядає сторінку, веб-сервер надсилає її користувачеві.
>
> На даний момент (2021 рік) вже немає сенсу отримувати безкоштовний хостинг, якщо ви серйозно займаєтеся інтернетом. Сервер можна **орендувати від 50 крон на місяць**.

- Встановлення сервера (відрізняється для Windows та Linux)
- Конфігурація сервера
	- Налаштування Apache
	- Налаштування PHP
	- <a href="/info">отримання поточної конфігурації PHP</a> (функція `phpinfo()`)
	- Маршрутизація Ngnix (підвищує продуктивність сервера)

Інтернет та веб-браузер
--------------------------------

- Веб-браузери
- Принцип запиту та відповіді
	- URL-адреса
	- Ajax та Ajaj
	- Генерація HTML-коду (системи шаблонів)

Струни
-----------------

- Читання, запис та об'єднання рядків, особливо базові операції з рядками
- Обробка рядків
	- Посимвольний перегляд
	- <a href="/if">порівняння рядків</a>
	- Схожість рядків (функції `levenshtein()`, `imilar_text()` та `soundex()`)
	- <a href="/explode">Вибухнути</a>, розділення роздільником
	- **Регулярні вирази** розбивають рядки по універсально настроюється масці
	- **Токенізатор** розбиває рядки на дрібні частини (токени)
- Серіалізація даних в рядок
	- <a href="/json">Json</a>, об'єкт javascript, що зберігається в рядку