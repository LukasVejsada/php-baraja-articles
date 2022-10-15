Об'єднання великих масивів в PHP
================================

> id: ccfb3f47-c8a0-4d0f-aa29-18d4c1775725
> slug:
> 	cs: mergovani-velkeho-pole
> 	uk: ob-ednannya-velikih-masiviv-v-php
> 
> publicationDate: '2020-02-06 09:32:08'
> mainCategoryId: '95374429-e651-46bd-9149-15aa716f8207'
> sourceContentHash: '3bfc3b53d26a4c9b675e851a643fc71a'

Часто нам потрібно об'єднати декілька масивів разом, це можна зробити дуже елегантно за допомогою функції `array_merge`:

```php
$userIdsA = [1, 2, 3];
$userIdsB = [5, 6, 7];

// повертає [1, 2, 3, 5, 6, 7]
$finalIds = array_merge($userIdsA, $userIdsB);
```

Функція `array_merge` об'єднує два масиви в один великий масив. Якщо відбувається колізія ключів, то перемагає значення крайнього правого масиву.

Повторне злиття в циклі
---------------------------

Однак, часто ми отримуємо масив масивів, який створюється тільки в циклі (наприклад, з бази даних, а потім пропускається через foreach), і тому ми не знаємо наперед кількість злиттів.

Наївне рішення могло б виглядати так:

```php
$finalIds = [];

foreach ($users as $user) {
    $finalIds = array_merge($finalIds, $user->someIds);
}
```

Однак це рішення є дуже неефективним, оскільки ми повинні об'єднувати масиви разом з кожною ітерацією та ітерації по всьому великому масиву.

Однак є просте рішення, коли ми модифікуємо алгоритм злиття, щоб він проходив через дані лише один раз:

```php
$finalIds = [];

foreach ($users as $user) {
    $finalIds[] = $user->someIds;
}
```

У цьому випадку поле `$finalIds` буде генерувати трохи більше даних, але це все одно є меншою проблемою, ніж перевага в економії часу.

Саме об'єднання залежить від версії PHP, яку ви використовуєте, і вирішується за допомогою елегантного трюку:

```php
/* PHP 5.6 і старше */ </ span> </ span> */ </ span> PHP 5.6 і старше
$finalIds = call_user_func_array('array_merge', $finalIds + [[]]);

/* PHP 5.6+ та новіші версії */
$finalIds = array_merge([], ...$finalIds);

/* PHP 7.4+ і новіше для непорожніх полів */
$finalIds = array_merge(...$finalIds);
```

Зокрема, дуже цікаво виглядає рішення `array_merge(...$finalIds)`, оскільки воно використовує нову концепцію PHP 7, де у функцію можна передавати динамічну кількість аргументів, використовуючи символ трикрапки на початку. Тоді процес злиття є максимально ефективним, і вся логіка автоматично обробляється внутрішньо PHP.

Скорочений запис `array_merge(...$finalIds)` можна використовувати тільки для непорожніх масивів. Якщо це пустий масив, то у функцію не передається жодного аргументу і функція видає помилку `Функція array_merge викликана з 0 параметрами, необхідний хоча б 1.`.