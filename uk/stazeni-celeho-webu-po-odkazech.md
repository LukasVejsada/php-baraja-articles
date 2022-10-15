Завантаження всього сайту за посиланнями на PHP
===============================================

> id: dd4abb8e-8f9b-4867-b98f-ff1c859d387a
> slug:
> 	cs: stazeni-celeho-webu-po-odkazech
> 	uk: zavantazennya-vs-ogo-sajtu-za-posilannyami-na-php
> 
> publicationDate: '2019-11-06 17:41:30'
> mainCategoryId: f46a0d80-fbe4-4be8-a5e4-04a8d29b0afc
> sourceContentHash: e70451decff5c7bdf19bca8181c0dd5e

Відносно часто я вирішую завдання завантаження всіх сторінок в межах одного сайту або домену, оскільки потім виконую з результатами різні вимірювання, або використовую сторінки для повнотекстового пошуку.

Одним з можливих рішень є використання готового інструменту [Xenu] (http://home.snafu.de/tilman/xenulink.html), який дуже складно встановити на веб-сервер (це Windows-програма), або [Wget] (https://www.gnu.org/software/wget/), який не скрізь підтримується і створює ще одну непотрібну залежність.

Якщо стоїть завдання просто зробити копію сторінки для подальшого перегляду, то дуже корисною є програма [HTTrack](https://www.httrack.com/), яка мені найбільше подобається, тільки при індексуванні параметризованих URL можна втратити точність в деяких випадках.

Тому я почав шукати інструмент, який може автоматично індексувати всі сторінки безпосередньо в PHP з розширеною конфігурацією. Згодом він став проектом з відкритим вихідним кодом.

Baraja WebCrawler
-----------------

Саме для цих потреб я реалізував власний пакет Composer [WebCrawler] (https://github.com/baraja-core/webcrawler), який елегантно справляється з процесом індексації сторінок самостійно, а якщо мені трапляється новий випадок, то я його ще більше вдосконалюю.

Встановлюється за допомогою команди Composer:

```shell
composer require baraja-core/webcrawler
```

І він простий у використанні. Достатньо створити екземпляр і викликати метод `crawl()`:

```php
$crawler = new \Baraja\WebCrawler\Crawler;

$result = $crawler->crawl('https://example.com');
```

У змінній `$result` буде доступний повний результат у вигляді екземпляру сутності `CrawledResult`, яку рекомендую вивчити, оскільки вона містить багато цікавої інформації про весь сайт.

Налаштування гусеничного ходу
------------------

Часто нам доводиться якось обмежувати завантаження сторінок, тому що інакше ми, напевно, завантажили б весь Інтернет.

Для цього використовується сутність `Config`, якій передається конфігурація у вигляді масиву (ключ-значення) і далі передається конструктором в Crawler.

Наприклад:

```php
$crawler = new \Baraja\WebCrawler\Crawler(
    new \Baraja\WebCrawler\Config([
        // ключ => значення
    ])
);
```

Налаштування параметрів:

| Ключ | Значення за замовчуванням | Можливі значення
|-------------------------|---------------|-----------------|
| `followExternalLinks` | `false` | `Bool`: Залишатися тільки в межах одного домену? Чи може він також індексувати зовнішні посилання?
| `` sleepBetweenRequests`` | ``1000`` | ``Int``: Час очікування між завантаженням кожної сторінки в мілісекундах.
| `maxHttpRequests` | `1000000` | `Int`: Скільки максимально завантажених URL-адрес?
| `maxCrawlTimeInSeconds` | `30` | `Int`: Скільки триває максимальне завантаження в секундах?
| `allowedUrls` | `['.+']` | `String[]`: Масив дозволених форматів URL у вигляді регулярних виразів.
| `forbiddenUrls` | `['']` | `String[]`: Масив заборонених форматів URL у вигляді регулярних виразів.

Регулярний вираз повинен точно відповідати всій URL-адресі у вигляді рядка.