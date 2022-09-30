Echo - вивід у вихідний код
===========================

> id: d6a1a7bf-03bf-49ea-9947-d4d6753ca6e4
> slug:
> 	cs: echo
> 	uk: echo-vivid-u-vihidnij-kod
> 
> perex:
> 	- Echo - výpis řetězce do stránky a na standardní výstup. Možnosti escapování a HTTP hlaviček.
> 	- Echo - вивести рядок на сторінку і в стандартний вивід. Параметри екранування та HTTP-заголовків.
> 
> publicationDate: '2020-02-16 18:40:31'
> mainCategoryId: '6cbbbf59-9bbd-4ca3-a6c3-eb204a2f8070'
> sourceContentHash: '7d611691825ec537f58f387696d13e28'

Конструкція `echo` використовується для виводу змінної або рядка у вихідний код.

| Підтримка: | Всі версії
|----------------|------
| Короткий опис: | Вивести один або декілька рядків
| Тип: | <a href="/commands-and-functions">команда, конструкція</a> (не функція)

Опис
-----

```php
echo 'Привіт, світе!';
```

На ньому написано: "Привіт, світ".

```php
$var = 'Текст';
echo $var;
```

Виводить значення змінної `$var`, тобто "Текст".

**Echo** не є функцією (це <a href="/commands-and-functions">команда</a>), тому ви можете використовувати дужку, а можете і не використовувати. Таким чином, правильним є також написання `echo ("hello world");`.

> **Додаткове зауваження:** PHP розглядає **Echo** як команду (конструкцію) і, таким чином, трактує її як вираз. Дужки в цьому випадку не є обов'язковими. Якщо дати позначення: `echo ('щось');`, то оператор **Echo** не стає функцією і не розглядається як така. Дужки в даному випадку означають взяття в них точного значення виразу, подібно до того, як це працює в математиці.

Лапки
--------

Рядки можуть бути взяті в лапки та апострофи.

Отже, це:

```php
echo "Привіт";
```

Це те саме, що і зараз:

```php
echo 'Привіт';
```

Але пам'ятайте, що кожен рядок повинен починатися і закінчуватися одним і тим же типом символу лапок, і символ лапок не повинен використовуватися в рядку.

Наприклад, якщо ви хочете вивести HTML-посилання (або будь-який HTML-код), перед лапками необхідно поставити косу риску. Коса риска означає "саме цей символ", тому вона не розуміється як вираз у мові.

```php
echo "<a href="index.php\">текст посилання</a>";
```

Технічна примітка: Лапки мають <a href="/quotation-meaning">особливе значення</a> в PHP.

Параметри
---------

- `arg` Вихідний параметр.

Значення, що повертаються
-----------------

Значення не повертається.

Не може бути використана як змінна.

Примітка
--------

Примітка: Оскільки це **мовна конструкція** (конструкція = команда) (а не функція), вона не може бути завантажена у змінну.

Приклад
-------

```php
echo "Привіт, світе!";

echo "echo" може виводити декілька рядків тексту.
Але остерігайтеся HTML-тега <br>, він не друкується. Для цього і призначена функція nl2br()".;

$a = "php";				// визначення змінної

echo "Мені подобається" . $a;	// пише він: Мені подобається php
```

**Echo** також має скорочений синтаксис, де можна використовувати тільки знак рівності після відкриваючого php-тега.

```php
Ahoj <?=$jmeno;?>!
```

Це корисно, якщо нам потрібно написати якусь швидку інформацію на сторінку. Наприклад, поточного року:

```php
Píše Jan Barášek © <?=date('Y');?>
```

> Цей скорочений синтаксис буде працювати тільки в тому випадку, якщо включено скорочене відкриття php-тегів, тобто директива `short_open_tag` встановлена в значення `on`.

Операція
-------

Всі звичайні математичні операції можна виконувати за допомогою команди **echo**.

Детальніше про математику див. <a href="/mathematics">окрему статтю</a>.

```php
echo 5 + 3 * 2; // виводить 11
```