# Домашнее задание к лекции №7

В домашнем задании к лекции №6 мы описали классы моделей реализующие сущности **Task** (Задача) и **Roadmap** (Дорожная карта) и представления для работы с этими сущностями. Необходимо описать класс модели реализующий новую сущность **Scores** (Очки), содержащий:
-   ссылочное поле **task** (Задача) на модель **Task** (Задача)
-   поле **date** (Время зачисления) типа datetime.datetime (дата и время)
-   поле **points** (Количество зачисленных очков) типа decimal.Decimal (число)

При завершении задачи (перевод в статус **ready**), мы должны добавлять пользователю некоторое количество очков. Значение должно расчитываться по формуле - (**today** - **create date** / **estimate** - **create date**) + (**estimate** - **create date** / **max estimate**), где:
-   **estimate** - ожидаемая дата завершения задачи
-   **today** - фактическая дата завершения задачи
-   **create date** - дата создания задачи
-   **max estimate** - максимально большой интервал времени **estimate** - **create date** зарегистрированный в системе (необходимо выбрать это значение из сохраненных записей модели **Task**)

### Статистика

Необходимо реализовать новое представление, выводящее пользователю системы статистику по его задачам для каждой дорожной карты задач.

Представление должно содержать две таблицы данных:
-   Статистика "Созданные/Решенные", где значения сгруппированы по неделям и есть поля:
    -   поле **Номер недели** в году типа int (целое число)
    -   поле **Интервал дат** типа str (строка), где
        -   значение формируется по шаблону "Y-m-d / Y-m-d"
        -   начало интервала - первый день недели
        -   конец интервала - последний день недели
    -   поле **Создано** типа int (целое число), содержащее количество всех задач, созданных в указанный интервал
    -   поле **Решено** типа int (целое число), содержащее количество всех задач, переведенных в статус **ready**
-   Статистика "Очки", где значения сгруппированы по месяцам и есть поля:
    -   поле **Месяц** типа str (строка), где
        -   значение формируется по шаблону "Y-m"
    -   поле **Зачислено** типа decimal.Decimal (число), содержащее сумму очков, зачисленных в указаный интервал

Для решения поставленных задач необходимо применять фреймворк Django и его возможности (модели, аггрегирующие функции, транзакции, маршруты, представления, стандартные шаблоны).

## Полезные ссылки

1.  [Запросы к СУБД, Queries](https://docs.djangoproject.com/en/1.11/topics/db/queries/)
2.  [Аггрегирующие запросы к СУБД, Aggregation](https://docs.djangoproject.com/en/1.11/topics/db/aggregation/)
3.  [Транзакции, Database transactions](https://docs.djangoproject.com/en/1.11/topics/db/transactions/)

### Самостоятельная работа *

Таблицы данных сложно воспринимать, для отображения статистической информации целесобразно использовать графики. Современные веб-приложения при этом активно используют такие javascript-библиотеки как, например, [D3](https://d3js.org/). Проект распространяется под BSD-лицензией, его [исходный код](https://github.com/d3/d3) можно найти на GitHub, там же присуствует и довольно полная [документация](https://github.com/d3/d3/wiki/Tutorials). Огромное количество примеров можно найти на [странице](https://bl.ocks.org/mbostock) Майка Бостока, основного контрибутора проекта D3.

![D3.js](https://habrastorage.org/files/273/96e/849/27396e84912546b7b1c7f94ffe50b43f.jpg)

#### Примечание

\* Работа выполняется по желанию