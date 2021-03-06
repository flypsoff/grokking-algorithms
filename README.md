# Адитья Бхаргава. Грокаем алгоритмы. Конспект книги с примерами реализации алгоритмов на java script.

## Глава 1. Знакомство с алгоритмами

### Бинарный поиск
Алгоритм на входе получает отсортированный список элементов. Возвращает позицию искомого элемента или null.

Пример: игра "угадай число". Загадано число от 1 до 100. При каждой попытке возвращается ответ: "мало", "много" или "угадал".
Плохой способ – перебирать все числа подряд. При самом отрицательном сценарии потребуется 100 попыток.
Эффективный способ – начнем с 50. Если мало, то пробуем 75. Если много, то 63 и тд, каждый раз исключая половину оставшихся возможных вариантов.
Какое бы число не было задумано, его можно угадать не более чем за 7 попыток.

При простом поиске из 240 000 вариантов может потребоваться 240 000 попыток. При бинарном - максимум 18.
Для списка из n элементов простой поиск занимает n шагов, бинарный log2n шагов.

*Логарифм по смыслу противоположен возведению в степень. Логарифм по основанию 10 от 100 означает в какую степень нужно возвести 10, чтобы получить 100. Ответ 10*

В нотации "О большое"(об этом позже), log всегда означает 2. Для списка из 8 элементов log8 == 3, тк 2^3 === 8.

**Бинарный поиск работает только с отсортированным списком.**


### Время выполнения
Скорость измеряется не временем, а ростом кол-ва операций.

Если максимальное к-во попыток совпадает с размером списка, при простом поиске,  время выполнения - линейное время пыполнения.

При бинарном поиске - поиск выполняется за логарифмическое время.

Факториальное время - ужасный ужас - при очень длинном списке, поиск становится невероятно долгим. Наример, поиск кратчайшего расстояния для того, чтобы объехать n городов:
5 городов - 120 операций, 6 городов - 720, 7 городов - 5040.

**линейное время - O(n)**

**логарифмическое время - O(log n)**

**факториальное время - O(n!)**

[Реализация бинарного поиска](binarysearch.js)

[Упражнения](binarysearch-tasks.js)

## Глава 2. Сортировка выбором

### Как устроена память
Память компьютера можно представить в виде огромного шкафа с множеством ящиков. У каждого ящика есть адрес. 
Когда требуется сохранить в памяти какое-то значение, мы запрашиваем у компьютера место в памяти, а он выдает адрес для сохранения значения.
Если нужно сохранить несколько значений, есть 2 основных способа: массивы и связные списки.

### Массивы и связные списки
При использовании массива, все задачи хранятся в памяти непрерывно, друг за другом. 
В списках каждый элемент хранит в себе ссылку на следующий.
При этом элементы могут размещаться в памяти где угодно. 

Получить запись быстрее можно из массива - обратиться по нужному адресу. При такой же операции со списком нужно пройти по всей цепочке.
С записью - наоборот. Нужна всего одна операция для записи значения в список и n операций для записи в массив.

чтение из списка – O(n) запись в список – O(1) удаление из списка – O(1)

чтение из массива – O(1) запись в массив – O(n) удаление из массива – O(n)

### Сортировка выбором
Легкий для понимания алгоритм, но очень медленно работает – O(n^2);
Каждый раз перебирается n элементов-1

[Реализация сортировки выбором](selectionsort.js)

[Упражнения](selectionsort-tasks.js)


## Глава 3. Рекурсия
Рекурсия - вызов функции самой себя. Состоит из двух частей: базового и рекурсивного случая. В базовом - условие выхода.

### Стек вызовов
Под вызов каждой функции определяется блок в памяти для всех переменных. Блоки определяются в стек.
Вызов ф-и из другой ф-и приостанавливает ее действие - частично завершенное состояние.

[Пример рекурсии](recursion.js)

[Упражнения](recursion-tasks.js)

## Глава 4. Быстрая сортировка
Работает быстрее сортировки выбором и часто применяется. Базовый случай - пустой массив или массив из одного элемента.
O(n log n) – в среднем. В худшем случае – O(n^2); Зависит от опорного элемента.

[Реализация быстрой сортировки](quicksort.js)

[Упражнения](quicksort-tasks.js)

## Глава 5. Хеш-таблица
Хэш-функция – функция, которая получает строку(набор байтов) и возвращает число. Хэш-таблицы – структура данных, связывающая ключи со значениями.
O(1) – в среднем. Отлично подходят для хранения кэша. 

### Коллизии
Коллизия - ситуация, когда двум ключам назначается один элемент массива. Простейшее решение – связный список в этом элементе. Хорошая хэш-функция создает минимальное кол-во коллизий.

[Упражнения](hash-tasks.js)

## Глава 6. Поиск в ширину

### Знакомство с графами
Граф моделирует набор связей. Каждый граф состоит из узлов и ребер. 

### Поиск в ширину
Этот алгоритм отвечает на два вопроса: существует ли путь от одного узла к другому и какой путь кратчайший.
Поиск производится сначала по связям первого уровня, потом второго урвня и тд. Связи, по которым нужно продолжать поиск добавляются в список
и образуют очередь. Очередь относится к категории структур FIFO (First In, First Out).

Время выполнения – O(V+E) V – кол-во вершин, E – кол-во ребер;

Дерево - граф, в котором нет ребер, указывающих в обратном направлении

[Реализация поиска в ширину](breadthfirstsearch.js)

[Упражнения](breadthfirstsearch-tasks.js)


## Глава 7. Алгоритм Дейкстры
Если известна "стоимость" каждого ребра, граф – взвешенный. Для поиска кратчайшего пути во взвешенном(без отрицательных весов), направленном графе, используется
алгоритм Дейкстры.

[Реализация поиска в ширину](dijkstra.js)

[Упражнения](dijkstra-tasks.js)

## Глава 8. Жадные алгоритмы
На каждом шаге алгоритма выбирается локальное оптимальное решение. В итоге получается глобально-оптимальное.
Время выполнения – O(n^2)

[Реализация жадного алгоритма](greedy.js)











