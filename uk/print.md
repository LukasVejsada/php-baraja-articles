Друк
====

> id: '23d672c5-b347-43b8-bd08-8ccb7ecca33f'
> slug:
> 	cs: print
> 	uk: druk
> 
> publicationDate: '2019-08-22 20:48:46'
> mainCategoryId: '6cbbbf59-9bbd-4ca3-a6c3-eb204a2f8070'
> sourceContentHash: b7f7c3c32d9f3c1efd794ca38b7db384

`print` - виведення рядка

Опис
--------------------------

```php
print 'Здрастуй, світ!';
```

`print()` насправді не є реальною функцією (це мовна конструкція), тому дужки використовувати не потрібно.

Параметри
--------------------------

- Я знаю, що це не так.

Вихідний параметр

Значення, що повертаються
--------------------------

Завжди повертає число 1.

Примітка
--------------------------

Примітка: Оскільки це **мовна конструкція** (а не функція), вона не може бути завантажена у змінну.

Приклад
--------------------------

```php
print "Привіт, світе!";

print "print" може виводити кілька рядків тексту, але слідкуйте за тегом HTML
тому що він не друкується. Саме про це йдеться у доповіді <a href="/nl2br">Nl2br</a>.";

// Приклад з'єднання зі змінною
$a = 'php';

print 'Мені подобається' . $a; // Мені подобається php
```

**print** виконує ту саму функцію, що й **echo**. Якщо ви шукаєте більше інформації, перегляньте статтю <a href="/echo">echo</a>.