Небезпечне використання констант в PHP
======================================

> id: b4d0f45f-c059-4a47-9b63-8980d0d465ed
> slug:
> 	cs: nebezpecne-konstanty
> 	uk: nebezpecne-vikoristannya-konstant-v-php
> 
> publicationDate: '2021-06-22 10:49:46'
> mainCategoryId: '561b0614-e152-4a62-a634-1f2d605d39d9'
> sourceContentHash: '58d4ea2e4bf106402386506b023ba4d2'

При використанні констант в PHP слід пам'ятати про дві хитрі речі.

Динамічні та статичні константи
------------------------------

Константа може бути визначена в PHP або статично безпосередньо в класі (найкраще рішення), або, наприклад, наступним чином:

```php
class Region
{
	public const PREFIX = 420;
}
```

І користь від цього цілком зрозуміла. Під час компіляції класу значення константи визначається і ми можемо отримати доступ до неї, викликавши ім'я класу та саму константу. Найчастіше за допомогою написання `Region::PREFIX`.

Інший (набагато гірший спосіб) - визначати константу динамічно під час виконання програми (найчастіше десь у конфігураційному скрипті), де вона потім є чимось на зразок:

```php
define('BASE_DIR', __DIR__ . '/../');
```

Основним недоліком визначення константи через функцію `define` є те, що скрипт, який визначає константу, міг бути не викликаний, тому константа не буде існувати при спробі її зчитування.

У поєднанні з використанням динамічної константи у визначенні статичної у класі це може призвести навіть до фатальної помилки відображення:

```php
class InvoiceGenerator
{
	// Це абсолютно неправильно!
	public const DATA_DIR = BASE_DIR . '/data/invoice';
}
```

> Пояснення:** **Пояснення:**
>
> Використання динамічної константи в статичній константі має основний недолік, який полягає в тому, що значення динамічної константи не може бути прочитане під час виконання програми. Тому цей скрипт повинен оброблятися заново при кожному запиті (тобто його не можна зберігати в OPCache для оптимізації швидкості), а якщо константа взагалі не існувала, то виникає фатальна помилка під час компіляції і додаток взагалі не може бути запущений.

Якщо ви використовуєте PhpStan, він може автоматично попередити вас про цю проблему:

```txt
Reflection error: Could not locate constant "BASE_DIR" while
evaluating expression in InvoiceGenerator at line 6
```

> Навчання: **Навчання:**
>
> Значення всіх констант завжди повинні бути постійними.


Успадкування констант при використанні static
-------------------------------------

У деяких випадках має сенс використовувати успадкування для перевизначення значення константи. Але в такому випадку предок не може зчитати значення з нащадка (або не повинен).

Прикладом є визначення країн та регіонів:

```php
abstract class Region
{
	public function getPrefix(): int
	{
		// Фатальна помилка!
		return static::REGION;
	}
}

final class CzechRepublic extends Region
{
	public const REGION = 420;
}
```

Парадокс полягає в тому, що вищенаведений код не обов'язково викидає помилку, але її може викинути некоректне використання спадковості.

Якщо викликати метод `getPrefix()` на нащадку `CzechRepublic`, то все буде коректно, оскільки значення константи буде прочитано правильно. Однак, якщо нащадок не задав значення константи, то буде викинута фатальна помилка неіснуючої константи. Найгірше те, що це **прихована залежність**, яка створюється при реалізації методу, і розробник, який успадковує клас, може навіть не знати про цю залежність.

Найкращим рішенням у цьому випадку є або визначення константи безпосередньо в предку зі значенням за замовчуванням (щоб логіка завжди проходила), або, як мінімум, виключення в гетері.

```php
abstract class Region
{
	public const REGION = null;

	public function getPrefix(): int
	{
		if (static::REGION === null) {
			throw new \LogicException('Регіон не визначено.');
		}
		return static::REGION;
	}
}

final class CzechRepublic extends Region
{
	public const REGION = 420;
}
```

PhpStan реагує на цю помилку наступним чином:

```txt
Access to undefined constant static(Region):REGION.
```