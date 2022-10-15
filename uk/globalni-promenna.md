Глобальні змінні в PHP
======================

> id: '1cdfc51a-31f4-4a5d-81f6-cfd92f86a9d4'
> slug:
> 	cs: globalni-promenna
> 	uk: global-ni-zminni-v-php
> 
> publicationDate: '2019-08-22 20:48:46'
> mainCategoryId: '0e39aee9-2818-480c-8081-e0c2d039bb24'
> sourceContentHash: '31e78a9abf19252ef62315230a3731b5'

Глобальні змінні доступні в будь-який час в будь-якій частині програми і не потребують передачі.

> Попередження:** Добре спроектований додаток не повинен використовувати глобальні змінні, оскільки вони порушують принцип інкапсуляції і при необережному поводженні з ними можуть призвести до важко виявлених помилок.

Приклад використання:

```php
$a = 1;
$b = 2;

function suma(): void
{
	global $a, $b;
	$b = $a + $b;
}

suma();

echo $b; // виводить число 3, тому що змінна $b є глобальною
```

Зауважимо, що ми отримали змінні `$a` та `$b` поза їх природним контекстом. Така поведінка називається "магічною", тому що якщо інша функція перевизначить змінні, що використовуються в даний момент, то програма зіткнеться з неочікуваним станом.

Правильно, програма повинна **інкапсулювати** і передавати змінні кожного разу:

```php
$a = 1;
$b = 2;

function suma(int $a, int $b): int
{
	return $a + $b;
}

echo suma($a, $b); // виводить 3
```

Завдяки цьому ми можемо викликати функцію динамічно з різними вхідними параметрами і її вихід буде залежати тільки від вхідних даних, а не від оточення.

Отримання вхідних параметрів з URL-адреси
---------------------------------

Мабуть, єдиним розумним застосуванням глобальних змінних є розбір користувацького вводу, в цьому випадку мова йде про <a href="/superglobal-variable">суперглобальні змінні</a>.

В даному випадку це чиста конструкція, оскільки змінна повинна бути доступна тільки для читання, а не тільки для запису, і до того ж вона однакова в усьому додатку:

```php
function getNameFromUrl(): string
{
    return isset($_GET['ім'я'])
    	? htmlspecialchars($_GET['ім'я'])
    	: '';
}

echo getNameFromUrl();
```