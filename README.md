# Домашнее задание к занятию "`Базы данных, их типы`" - `Сулименков Алексей`

---

### Задание 1. СУБД

Кейс

Крупная строительная компания, которая также занимается проектированием и девелопментом, решила создать правильную архитектуру для работы с данными. Ниже представлены задачи, которые необходимо решить для каждой предметной области.

Какие типы СУБД, на ваш взгляд, лучше всего подойдут для решения этих задач и почему?

1.1. Бюджетирование проектов с дальнейшим формированием финансовых аналитических отчётов и прогнозирования рисков. СУБД должна гарантировать целостность и чёткую структуру данных.

1.1.* Хеширование стало занимать длительно время, какое API можно использовать для ускорения работы?

1.2. Под каждый девелоперский проект создаётся отдельный лендинг, и все данные по лидам стекаются в CRM к маркетологам и менеджерам по продажам. Какой тип СУБД лучше использовать для лендингов и для CRM? СУБД должны быть гибкими и быстрыми.

1.2.* Можно ли эту задачу закрыть одной СУБД? И если да, то какой именно СУБД и какой реализацией?

1.3. Отдел контроля качества решил создать базу по корпоративным нормам и правилам, обучающему материалу и так далее, сформированную согласно структуре компании. СУБД должна иметь простую и понятную структуру.

1.3.* Можно ли под эту задачу использовать уже существующую СУБД из задач выше и если да, то как лучше это реализовать?

1.4. Департамент логистики нуждается в решении задач по быстрому формированию маршрутов доставки материалов по объектам и распределению курьеров по маршрутам с доставкой документов. СУБД должна уметь быстро работать со связями.

1.4.* Можно ли к этой СУБД подключить отдел закупок или для них лучше сформировать свою СУБД в связке с СУБД логистов?

1.5.* Можно ли все перечисленные выше задачи решить, используя одну СУБД? Если да, то какую именно?


## Ответ:
1.1. Гарантия целостности и чёткой структуры данных - важнейшая функция реляционной базы данных, поэтому подходят PostgresSQL, MySQL/MariaBD, MSSQL, Oracle SQL
1.1.* Можно использвать memcashed или radis
1.2. Если потребуется  реализовать какую-либо бизнес-логику на уровне базы данных, то это проще сделать в реляционных БД (PostgresSQL, MySQL/MariaBD, MSSQL, Oracle SQL)
1.2.* Да, подойте PostgresSQL/MSSQL/MySQL
1.3. Подойдет MongoDB (документоориентированная БД) 
1.3.* MongoDB позволит использовать уже существующую СУБД
1.4. Лучше всего подойдут графовые базы данных по типу Neo4j.
1.4.* Для отдела закупок лучше организовать свою СУБД.
1.5.* Если стьруктура и бизнес-логика на начальном этапе проектирования была правильно пределена, то можно обойтись одной СУБД на выбор PostgresSQL, MSSQL, Oracle SQL
---

### Задание 2. Транзакции

2.1. Пользователь пополняет баланс счёта телефона, распишите пошагово, какие действия должны произойти для того, чтобы транзакция завершилась успешно. Ориентируйтесь на шесть действий.

2.1.* Какие действия должны произойти, если пополнение счёта телефона происходило бы через автоплатёж?

## Ответ
2.1.
Если черем мобильный банк то так: 
- Аутентификация и авторизация пользователя
- Проверка правильности введеногое номера и принадлежность к оператору
- Проверка количества денег на банковском счету, с которого производится оплата
- Подтвержение оплаты от пользователя
- Оплата
- Зачисление на счету мобильного оператора
- Уведомление со стороны оператора

2.1.*
- Проверка количества денег на банковском счету, с которого производится оплата
- Оплата
- Уведомление о оплате со стороны банка
- Зачисление на счету мобильного оператора
- Уведомление со стороны оператора


### Задание 3. SQL vs NoSQL

3.1. Напишите пять преимуществ SQL-систем по отношению к NoSQL.

3.1.* Какие, на ваш взгляд, преимущества у NewSQL систем перед SQL и NoSQL.

## Ответ
1. Cоответствие базы данных требованиям ACID, целостность данных, структурированность.
2. Стабильности работы
3. Язык SQL универсален для всех реляционных хранилищ и поэтому в случае смены СУБД не придётся переписывать весь код.
4. Процесс создания реляционного хранилища включает в себя этап проектирования модели данных. На этой стадии можно оценить узкие места выбранной стратегии и спроектировать действительно надежную и удобную систему.
5. Широкая поддержка интеграци и большое комьюнити.. 
---

### Задание 4. Кластеры

Необходимо производить большое количество вычислений при работе с огромным количеством данных, под эту задачу выделено 1000 машин.
На основе какого критерия будете выбирать тип СУБД и какая модель распределённых вычислений здесь справится лучше всего и почему?

## Ответ

Необходимо выбрать Distributed SQL такую как YDB или F1, которые имеют преимущества как реляционных БД так и NoSQL и были созданны именно под эти задачи.

---