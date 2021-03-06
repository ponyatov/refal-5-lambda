  Цель исследования: изучить эквивалентные преобразования программ, научившись
конвертировать программы на полном Рефале-5 в подмножество Базисного Рефала
Рефал-5. Здесь под подмножеством Базисного Рефала Рефала-5 подразумевается
язык Рефал-5, из которого исключены только две конструкции: условия и блоки.
Формально в подмножество Базисного Рефала (так, как это определено в учебнике
к языку) также не должны входить копилка и метафункции, но здесь задача
эмуляции этих средств средствами Базисного Рефала не ставится.

  Результаты.
  1. Удалось написать такой конвертор, однако в две попытки.
  Первая попытка была в 2015 году и она провалилась по нескольким причинам.
  Во-первых, не было разделения на уровни абстракции — при обходе
синтаксического дерева одновременно я пытался конвертировать и условия, и блоки.
Это сильно усложняло код.
  Во-вторых, одновременно с этим я пытался избегать потери и дублирования
повторных переменных. Что тоже, очевидно, вносило постороннюю сложность.
  И, самое главное, в-третьих, у меня не было цельного представления, во что
преобразовывать условия (пытался делать по частям, реализуя условия без
открытых e-переменных, с одной переменной, с несколькими…, но без понимания
общей картины).
  Вторая попытка (этого года) учла уроки прошлого.
  Преобразование было разделено на два прохода: устранение блоков и устранение
условий. Блоки можно преобразовывать в дополнительные функции независимо
от условий, а уже потом о блоках можно забыть.
  Было решено отказаться от отслеживания дублирования переменных. Во-первых,
ради упрощения логики (ведь суть задачи — выражение этих управляющих конструкций
более примитивными средствами языка), во-вторых, на практике, по моему опыту,
дубликаты больших переменных встречаются крайне редко, в-третьих, необходимость
копирования есть деталь конкретной реализации РЕФАЛа-5.
  И наконец, до написания кода было сформулировано чёткое и ясное представление
о виде кода — был подробно разобран витиеватый пример с тремя открытыми
e-переменными, сгенерированные конструкции рассмотрены и обобщены, выделены
правила для переписывания. Файл «Подход к преобразованию условий.md» в текущей
папке описывает весь ход моих рассуждений.
  2. Побочным продуктом написания конвертора стали front-end РЕФАЛа-5 и обратный
преобразователь синтаксического дерева в исходный текст. Здесь между ними
находится преобразователь, но если его убрать, получается утилита для проверки
на ошибки синтаксиса (включая семантические) и автоматического форматирования.