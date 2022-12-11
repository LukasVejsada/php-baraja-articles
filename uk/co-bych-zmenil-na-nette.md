Що б я змінив у Нетті на місці Девіда Ґрадла
============================================

> id: bad8fe4f-92a4-4396-8698-7ec42bb2aef8
> slug:
> 	- null
> 	uk: so-b-ya-zminiv-u-netti-na-misci-devida-gradla
> 
> cs: co-bych-zmenil-na-nette
> publicationDate: '2022-11-18 17:45:00'
> mainCategoryId: '483db7b7-5699-41fb-ba0b-d2b653bacd1f'
> sourceContentHash: '953e6c78b9dff185bbf8e3e9582d24c3'

Майже 6 років активно використовую Nette Framework для розробки комерційного програмного забезпечення. Протягом перших років я був дуже захоплений, і ця система чудово задовольняла всі потреби, які ми мали як команда, і в принципі не було причин шукати інший інструмент.

Приблизно з 2019 року я починаю спостерігати деякий спад початкового ентузіазму в Nette, де я починаю сумувати за деякими розширеними функціями. Часто це речі, які виходять за рамки самого фреймворку, тому я навіть не очікую, що вони коли-небудь будуть реалізовані, але, з іншого боку, розробник повинен прийняти рішення, як продовжувати розвиток далі, і, можливо, звернутися до іншої технології.

Рівень бази даних
-----------------

Я вважаю базу даних Nette однією з найбільших помилок фреймворку, на жаль.

Щотижня у нас в компанії проходять співбесіди, на яких молодь, яка щойно закінчила школу, або навіть люди середнього рівня, які переходять з іншої структури, застосовують і відкривають для себе базу даних Nette в рамках свого знайомства з Nette. Як рівень бази даних, це не так вже й погано, але проблема полягає в практичному використанні в реальних проектах.

Це тому, що Nette Database не намагається підштовхнути розробників до використання строгих типів даних з самого початку, до іменування стовпців та відношень, до відокремлення методів запитів (репозиторіїв) від моделей та інших дрібних нюансів, які в цілому роблять дуже багато.

Багато років я користувався бібліотекою "Дібі", яка свого часу відіграла величезну роль. Це дозволило досить гарно запитувати базу даних та уніфікувало інтерфейс. З іншого боку, часи не стоять на місці, і коли бази даних повертатимуть нетипізовані об'єкти, PHPStan просто принципово не буде задоволений.

Особисто я б або вбудував власну підтримку сутностей та репозиторіїв в базу даних Nette, або забезпечив офіційну підтримку Доктрини в рамках Nette. Якщо ви програмуєте програми на рівні великої корпорації, ви повинні серйозно ставитися до розвитку, і Доктрина, зокрема, має великий сенс. В той же час, ви хочете одразу навчити новачків кращим технологіям і не хочете привчати їх до старих звичок.

Трасування та протоколювання помилок
---------------------

Я досі вважаю Tracy найкращим відладчиком для PHP.

Коли я прийшов у 2017 році в неназване діджитал-агентство і побачив технічний стан їхніх Nette-проектів, я жахнувся. Скільки разів у них були сайти, написані на чистому PHP без жодної спроби логування помилок. Досить простим рішенням було встановити Tracy на проект, викликати `Debugger::enable()` і більше нічого не робити. Помилки автоматично заносилися до каталогу, який потрібно було лише вручну переглядати кожні кілька днів.

Що стосується Трейсі, то мені здається, що це вже готовий продукт, який Девіду немає сенсу покращувати. З іншого боку, я все ще бачу простір для вдосконалення в новому напрямку.

Наприклад, чому Трейсі не включає платні функції для компаній або приватних осіб, які серйозно ставляться до безпеки?

Трейсі може реалізувати спеціальний веб-інтерфейс типу Sentry, де ви створюєте обліковий запис, а виробничі помилки автоматично надсилаються через API, де ви можете відстежувати їх у всіх проектах. Додаток також може запитувати окремі сайти, автоматично визначати, що вони недоступні, і повідомляти власника в інший спосіб (оскільки Трейсі не може логічно виявити збій сервера). Я також іноді стикаюся з проблемою, що на виробничому майданчику випадково вмикається Tracy, і ви можете дізнатися через DIC, як отримати доступ до бази даних або деінде. Трейсі повинен попередити вас і про це.

Трейсі також міг реалізувати інші дрібниці, які я знаю з Node.js. Наприклад, для відображення вихідного коду можна було б вибрати інтервал символів, на якому рядок підсвічується особливим чином, навіщо передбачити можливість підсвічування конкретної лексеми в межах рядка. У той же час, було б непогано додати підтримку другої (можливо, синьої) лінії підсвічування для відображення контексту в наступній частині програми.

При відображенні фрагмента вихідного коду я б не побоявся додати кнопку, яка може відобразити решту коду в ajax, щоб я міг досліджувати його безпосередньо в браузері зі стеку викликів. Це те, що робить Symfony, і це чудова функція. Якби це було доповнено базовим статичним аналізом з можливістю повзати по методам, класам та успадкуванню, то це зекономило б багато налагоджувальної роботи для всієї команди.

Якщо стек викликів проходить через пакет, було б непогано показувати версію пакета, з яким я працюю, для конкретного файлу. Часто я отримую помилку в пакеті, який розробляю, і я можу візуально знати, що це стара версія.

Статична маршрутизація
----------------

В рамках Nette Router я б дозволив визначити новий тип, який називається статичний маршрутизатор. Це був би нащадок базового маршрутизатора, але він міг би приймати тільки рядковий літерал, який був би не регулярним виразом, а прямим шляхом. Багато сторінок працюють статично (контакти, різні статті, на диво часто навіть домашня сторінка), і через це роутеру доводиться кожного разу оцінювати реджекс-правила на відповідність і склад URL.

Якби в шаблоні Latte, наприклад, використовувався статичний маршрут, його можна було б безпечно перевести в статичний рядок `{$basePath}/path` під час компіляції шаблону, тому не було б необхідності компілювати 100 URL-адрес, які є в макеті, наприклад, на кожен запит.

Я розумію, що можу досягти тієї ж функціональності шляхом кешування на стороні шаблону, але я б набагато більше цінував системне рішення.

У фреймворку Next.js я повністю захопився концепцією статичної маршрутизації. Немає такого поняття, як `n:href`, коротше кажучи, ви повинні знати URL-адресу заздалегідь, що змушує вас не робити так багато перенаправлень, заздалегідь продумувати формати URL-адрес і зберігати їх постійними.

Інтерфейс PSR
------------

Мені шкода, що Nette не має власного інтерфейсу PSR. Як розробника пакунків, це може збити вас з пантелику, якщо ви взагалі хочете визначити залежність Composer від Nette. З одного боку, Nette вирішує для вас багато проблем, з іншого боку, ви знаєте, що потім просто не зможете її замінити. Неодноразово я вважав за краще використовувати Symfony, Laravel або зовсім інший універсальний інтерфейс через відсутність універсального інтерфейсу.

Відсутність підтримки загальних стандартів для майбутньої переносимості - головна причина, чому я повністю пішов з Nette в 2022 році і ми розробляємо нові додатки в командах виключно на generic.

Рівень API
----------

Що робити, якщо ви хочете використовувати Nette як бекенд для обробки запитів REST API? Ви будуєте презентера і відправляєте відповідь як `$this->sendJson()`? Чи будете ви встановлювати сторонню бібліотеку? Чи ви Девід Градл, який вирішує потребу у відсутній бібліотеці, одразу ж пишучи нову?

Чому Nette не може реалізувати щось настільки поширене, як REST API, відразу з коробки? Сьогодні майже кожному додатку потрібно спілкуватися через API - наприклад, надавати дані фронтенду.

Для новачків це знову ж таки призводить до того, що вони починають користуватися вбудованим Latte і сніппетами, замість того, щоб дізнатися, що є кращий варіант - побудувати весь фронтенд окремо, і просто надавати йому дані.

Довіра до того, що буде через 10 років
-------------------------

Останній пункт є дуже прагматичним, і походить з дебатів, які ми час від часу чуємо від бізнес-відділів в команді.

Що було б, якби Девід Грудл взагалі припинив розробку Nette? А якщо хтось припинить її розробку? На що б ми перейшли? І наскільки це буде складно?

Багато розробників (часто без корпоративного досвіду) люблять кепкувати з цього приводу, мовляв, нічого страшного. Ніби так, але це не так.

Коли ви стоїте перед вибором, що краще - Nette чи React та Node.js для навчання молодших розробників у вашій компанії, то, на жаль, останній варіант перемагає.

Нетте ще не встигла на поїзд, але в десятках інтерв'ю, які я давав за останні півроку, я відчуваю це досить сильно.