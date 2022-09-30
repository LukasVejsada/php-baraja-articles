Як живеться програмісту у внутрішній команді розробників
========================================================

> id: '9309b0f2-0265-43aa-a9c3-10b2d486cdfc'
> slug:
> 	cs: jak-zije-programator-v-internim-tymu
> 	uk: yak-zivet-sya-programistu-u-vnutrisnij-komandi-rozrobnikiv
> 
> publicationDate: '2022-01-10 12:00:00'
> mainCategoryId: '483db7b7-5699-41fb-ba0b-d2b653bacd1f'
> sourceContentHash: e65dd78fa9813b552f30b98f04aacb30

За чесність доводиться платити високу ціну.

Цей сайт завжди був описом тієї реальності, з якою стикаються люди в ІТ, тому я хотів би розповісти про свій досвід роботи в командах розробників. Нижче наведено загальний досвід, який я отримав у різних компаніях. Жоден досвід не пов'язаний з однією конкретною компанією і не обов'язково слугує для критики.

Компанії, як правило, не хочуть працьовитих та ініціативних людей
----------------------------------------------

Маєте багато ідей? Хочете впроваджувати інновації? Вам подобається знаходити елегантні рішення для складних проблем, над якими працює ваша команда і які мучать половину компанії? Чи усвідомлюєте ви важливість безпеки, розробки програмного забезпечення та пошуку вузьких місць проекту?

Ймовірно, ви будете нещасливі в команді розробників протягом тривалого часу.

Командна робота - це те, з чим я дуже борюся останнім часом, тобто я просто плаваю в ній і намагаюся зрозуміти абсолютно інтуїтивно незрозумілі для мене принципи, яких я маю дотримуватися.

- Командна робота означає вироблення рішення, яке зрозуміле всій команді. Часто не найкращий. Це майже ніколи не буває елегантно. Насправді це завжди неефективно. Але вона має ту класну перевагу, що вся команда її розуміє і нею можна керувати в довгостроковій перспективі. Це надзвичайно важлива ідея. Тому що з великими проектами немає такого великого тиску, щоб бути ефективним, тому що як компанія ви можете масштабуватися за рахунок людей і у вас достатньо грошей. Набагато важливіше доставити речі вчасно, нехай навіть частково порушеними і з невідомими заздалегідь обмеженнями, але вчасно. Це пов'язано з тим, що рішення, яке ви надасте завтра (навіть якщо воно недосконале), має набагато більшу цінність для замовника, ніж на 100% налагоджене рішення, яке не буде існувати протягом року.
- Інновації та виштовхування - це не зовсім правильно. Це пов'язано з тим, що в компаніях працюють реальні люди, які мають сім'ї і хочуть працювати тільки в робочий час. Це обов'язково означає, що люди мають обмежений час для того, щоб вчитися і пробувати щось нове. По суті, компаніям доводиться впихати навчання та розвиток у робочий час людей, який можна використати для майбутньої роботи. Цікавим наслідком цього є відкладання прийняття рішень та вивчення нового на потрібний час. Зі свого боку, я розумію такий підхід і для мене він має багато сенсу. Якби у мене були співробітники, я б теж віддав перевагу спокійним людям, які протримаються в компанії, скажімо, 15 років, а не людям, які мають великий загальний огляд і хочуть рухатися далі, але це буде за рахунок колективу. Це правда, що колективне рішення ніколи не буде таким же, як індивідуальне, але це не означає, що воно буде гіршим.

Такі, як я, є потенційним джерелом проблем і конфліктів. Це круто, коли так думаєш.

При кодорецензуванні просто шукайте об'єктивні помилки
----------------------------------------

У кожній компанії є свої правила поведінки. На жаль. Мене це дуже дратувало спочатку.

Коли ви використовуєте одну з більш зрілих мов, таких як .NET, правила стилю коду, як правило, більш схожі. І тільки тоді ви дізнаєтесь, що PHP та JavaScript все ще існують у світі. Особливо це стосується PHP, який іноді трохи розчаровує. PHP - це дуже зріла мова з багатьма чудовими можливостями, але, з мого досвіду, вона використовується в компаніях приблизно на третину від свого загального потенціалу. Причини, як правило, різні, найчастіше - інерція.

У зв'язку з цим я давно шукав процедурне рішення для перегляду коду. Я давно граюся з PhpStan і стежу за ідеями навколо нього. Основна ідея PhpStan полягає в тому, що він висвітлює лише об'єктивні помилки, які неодмінно трапляються в певний момент. Чим більше я вивчаю PhpStan і виводжу його на новий рівень, тим більше я внутрішньо переконуюся в його істинності.

Було б добре, якби PhpStan був впроваджений хоча б у половині чеських компаній. Було б ще краще, якби хоча б до 6-го рівня. На практиці я бачив, що найкращі компанії мають 4-й або 5-й рівень.

Буквально на днях мені стало цікаво, чи може існувати реальний працюючий виробничий додаток, який має власну команду розробників, і він навіть не проходить рівень 0 - це рівень, який контролює речі, які ви очікуєте в будь-якому додатку. Щось на кшталт того, щоб переконатися, що всі класи і функції існують, файли не мають помилок розбору і так далі. І так, такі заявки є. Але в довгостроковій перспективі ситуація покращується. Сподіваюся.

Тому я дотримуюся аналогічного підходу до перегляду коду. Я повідомляю тільки те, що об'єктивно завжди неправильно. Я часто стикаюся з неправильною оцінкою ступеня - щось не так, але знову ж таки, це не така велика проблема, щоб її вирішувати. Багато проблем вирішуються шляхом конвенції, або декларуванням того, що ризик невеликий, тому немає сенсу його лікувати.

Я завжди вважав відсутність типів даних (навіть складених) критичною помилкою. Тоді я зрозумів, що є test and dump.

Я не думаю, що у мене є конкретний висновок в цій частині. Просто у мене є багато суб'єктивних коментарів з цього приводу, які скоріше можуть бути джерелом взаємного непорозуміння, тому я не буду їх публікувати. У довгостроковій перспективі я схиляюся до висновку, що не можу займатися код-рецензуванням - або я занадто суворий, або занадто доброзичливий. Я не можу сказати на загальному рівні, що дійсно важливо, а що не дуже. Мені було б дуже цікаво дізнатися, як це роблять інші люди. Ніхто поки що не зміг дати мені відповіді, якою я міг би скористатися.

На кастомну розробку грошей немає.
---------------------------------

У вас є агентство і ви займаєтеся веб-розробкою на замовлення? Якщо ви недостатньо великі і робите великі проекти для інших корпорацій, то, можливо, одного дня вас просто не стане.

Причиною цього є недостатнє фінансування замовних проектів. Ймовірно, це пов'язано з характером контрактів, які є більш вигідними для покупців. Насправді більшість агентств жорстоко недофінансовуються і приносять реальний прибуток лише власникам.

Коли ви внутрішньо розвиваєте проект як компанія для себе, то затримка поставки на місяць, напевно, не має такого великого значення. Як агентство, якщо ви не виконуєте роботу протягом місяця, ви гарантовано будете погано спати на роботі протягом цього місяця, послідовно руйнуючи своє здоров'я, клієнт буде лаятися в телефон і квитки, постійно питаючи, чи можна швидше, а в якості винагороди ви все одно будете платити неустойку за договором. А якщо ні, то клієнт затаврує вас як ненадійного підрядника і, можливо, піде в інше місце, де все одно буде не краще.

Але це правила гри, з якими я познайомився на практиці, і які пробили дірку в моєму бюджеті.

Укладання контрактів є чи не найскладнішою формою ведення бізнесу в ІТ. Ви не хочете займатися підрядами. Контрактація знищить вас. Вони будуть дзвонити у вихідні, вночі, на Різдво. Половину роботи, яку ти виконуєш, тобі не оплачують. Ви будете вибачатися за помилки, яких не можете зробити. Ви будете дивитися в Instagram на розповіді друзів, які поїхали у третю відпустку цього року, поки ви сидите в офісі о 3 годині ночі в суботу, закінчуючи клієнтський проект, за який вас все одно будуть сварити в понеділок, тому що в контракті було прописано більше, ніж ви змогли виконати. Люди підуть у відпустку, на лікарняний, а ви будете працювати замість них. Або тебе звільняють. І тоді ви будете із задоволенням платити за оренду.

Але знову ж таки, багато чому вчишся. Тому що саме під тиском ти повинен вчитися і бути ефективним, щоб наступного разу встигнути зробити трохи більше за той самий проміжок часу. Погано те, що ви не можете застосувати ці знання та досвід деінде, тому що компанії просто не зацікавлені (я пояснював вище).

На щастя, це історія 2019 року і до неї ще далеко.

Ідеального світу ніколи не буде
-------------------------

Якщо я роблю те, що мені подобається? А ти? :D

Я думаю, що це все питання міри. Ви, напевно, ніколи не будете виконувати роботу, яка приносить вам задоволення на 100%. Ймовірно, завжди знайдеться хтось, хто пояснить вам, що ви не можете зробити те, чого ви насильно вчилися протягом 10 років, а внутрішньо знаєте, що можете.

З іншого боку, за певну частку заперечення власної особистості ти отримуєш простір для того, щоб мати щось більше. Наприклад, вихідні дні, краще здоров'я, більше часу для себе, стабільне оточення тощо. Те, що вона не може бути стійкою в довгостроковій перспективі, також очевидно.

Мені подобається мати можливість пробувати різні речі, щоб дізнатися з перших вуст, як це відбувається в інших. Робота в команді розробників - це величезна нудьга в порівнянні з індивідуальною роботою.

Йдеться вже не про пошук найкращого і найшвидшого рішення, а про співпрацю. Йдеться про покращення комунікації, емоцій, а головне - про те, щоб навчитися бути людьми. І це теж величезна цінність.