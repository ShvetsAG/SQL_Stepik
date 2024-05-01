# Решение заданий с курса по SQL на платформе [Stepik](https://stepik.org/catalog)

### 1.1   Отношение (таблица)

Шаг_8. Сформулируйте SQL запрос для создания таблицы book. [(сайт)](https://stepik.org/lesson/297508/step/8?unit=279268)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE book(
    book_id INT PRIMARY KEY AUTO_INCREMENT, 
    title VARCHAR(50),
    author 	VARCHAR(30),
    price  DECIMAL(8, 2),
    amount INT
)
```

</details>

Шаг_9. Занесите новую строку в таблицу book (текстовые значения (тип VARCHAR) заключать либо в двойные, либо в одинарные кавычки). [(сайт)](https://stepik.org/lesson/297508/step/9?unit=279268)

<details>
  <summary>Решение</summary>

```mysql
INSERT INTO book (book_id,	title,	author,	price,	amount) 
VALUES (1,	'Мастер и Маргарита',	'Булгаков М.А.',	670.99,	3)
```

</details>

Шаг_10. Занесите три последние записи в таблицу book,  первая запись уже добавлена на предыдущем шаге: [(сайт)](https://stepik.org/lesson/297508/step/10?unit=279268)

<details>
  <summary>Решение</summary>

```mysql
INSERT INTO book (title, author, price, amount)
VALUES ('Белая гвардия', 'Булгаков М.А.', 540.50, 5);
INSERT INTO book (title, author, price, amount)
VALUES ('Идиот', 'Достоевский Ф.М.', 460.00, 10);
INSERT INTO book (title, author, price, amount)
VALUES ('Братья Карамазовы', 'Достоевский Ф.М.', 799.01, 2);
SELECT * FROM book
```

</details>


### 1.2   Выборка данных

Шаг_2. Вывести информацию о всех книгах, хранящихся на складе. [(сайт)](https://stepik.org/lesson/297509/step/2?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select * from book
```

</details>

Шаг_3. Выбрать авторов, название книг и их цену из таблицы book. [(сайт)](https://stepik.org/lesson/297509/step/3?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select author, title, price
from book
```

</details>

Шаг_4. Выбрать названия книг и авторов из таблицы book, для поля title задать имя(псевдоним) Название, для поля author –  Автор. [(сайт)](https://stepik.org/lesson/297509/step/4?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select author, title, price
from book
```

</details>

Шаг_5. Для упаковки каждой книги требуется один лист бумаги, цена которого 1 рубль 65 копеек. Посчитать стоимость упаковки для каждой книги (сколько денег потребуется, чтобы упаковать все экземпляры книги). В запросе вывести название книги, ее количество и стоимость упаковки, последний столбец назвать pack.  [(сайт)](https://stepik.org/lesson/297509/step/5?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select title, amount, amount*1.65 as pack
from book
```

</details>

Шаг_6. В конце года цену каждой книги на складе пересчитывают – снижают ее на 30%. Написать SQL запрос, который из таблицы book выбирает названия, авторов, количества и вычисляет новые цены книг. Столбец с новой ценой назвать new_price, цену округлить до 2-х знаков после запятой.  [(сайт)](https://stepik.org/lesson/297509/step/6?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select title, author, amount, round(price*0.7,2) as new_price
from book
```

</details>

Шаг_7. При анализе продаж книг выяснилось, что наибольшей популярностью пользуются книги Михаила Булгакова, на втором месте книги Сергея Есенина. Исходя из этого решили поднять цену книг Булгакова на 10%, а цену книг Есенина - на 5%. Написать запрос, куда включить автора, название книги и новую цену, последний столбец назвать new_price. Значение округлить до двух знаков после запятой.  [(сайт)](https://stepik.org/lesson/297509/step/7?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select author, title, 
       round(if(author = 'Булгаков М.А.',price*1.1,if(author = 'Есенин С.А.',price*1.05,price)),2) as new_price
from   book   
```

</details>

Шаг_8. Вывести автора, название  и цены тех книг, количество которых меньше 10.  [(сайт)](https://stepik.org/lesson/297509/step/8?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select author, title,  price 
from book
where amount < 10 
```

</details>

Шаг_9. Вывести название, автора,  цену  и количество всех книг, цена которых меньше 500 или больше 600, а стоимость всех экземпляров этих книг больше или равна 5000.  [(сайт)](https://stepik.org/lesson/297509/step/9?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select  title, author, price, amount
from book 
where (price < 500 or price > 600)
  and amount*price >= 5000
```

</details>

Шаг_10. Вывести название и авторов тех книг, цены которых принадлежат интервалу от 540.50 до 800 (включая границы),  а количество или 2, или 3, или 5, или 7.  [(сайт)](https://stepik.org/lesson/297509/step/10?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select title, author
from book
where price BETWEEN 540.50 and 800
  and amount in (2,3,5,7)
```

</details>

Шаг_11. Вывести  автора и название  книг, количество которых принадлежит интервалу от 2 до 14 (включая границы). Информацию  отсортировать сначала по авторам (в обратном алфавитном порядке), а затем по названиям книг (по алфавиту).  [(сайт)](https://stepik.org/lesson/297509/step/11?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select author, title 
from book 
where amount between 2 and 14
order by 1 desc, 2 asc
```

</details>

Шаг_12.* Вывести название и автора тех книг, название которых состоит из двух и более слов, а инициалы автора содержат букву «С». Считать, что в названии слова отделяются друг от друга пробелами и не содержат знаков препинания, между фамилией автора и инициалами обязателен пробел, инициалы записываются без пробела в формате: буква, точка, буква, точка. Информацию отсортировать по названию книги в алфавитном порядке.  [(сайт)](https://stepik.org/lesson/297509/step/12?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
select title, author
from book
where trim(title) like '% %'
  and author like '%С.%'
order by title
```

</details>

Шаг_13. Магазин счёл, что классика уже не пользуется популярностью, поэтому необходимо в выборке:
1. Сменить всех авторов на "Роулинг Джоан".
2. К названию каждой книги в начале дописать "Гарри Поттер и".
3. Цену поднять на 42%.
4. Отсортировать по убыванию длинны названия.  [(сайт)](https://stepik.org/lesson/297509/step/13?unit=279269)

<details>
  <summary>Решение</summary>

```mysql
SELECT 'Роулинг Джоан'AS author,
        CONCAT_WS(' ', 'Гарри Поттер и', title) AS title,
        ROUND(price*1.42,2) AS price
FROM book
ORDER BY LENGTH (title) DESC
```

</details>

### 1.3   Запросы, групповые операции

Шаг_2. Отобрать различные (уникальные) элементы столбца amount таблицы book. [(сайт)](https://stepik.org/lesson/297515/step/2?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select distinct amount
from book
```

</details>

Шаг_3. Посчитать, количество различных книг и количество экземпляров книг каждого автора , хранящихся на складе.  Столбцы назвать Автор, Различных_книг и Количество_экземпляров соответственно. [(сайт)](https://stepik.org/lesson/297515/step/3?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select author as "Автор", 
       count(book_id) as "Различных_книг",
       sum(amount) as "Количество_экземпляров"
from  book 
group by author
```

</details>

Шаг_4. Вывести фамилию и инициалы автора, минимальную, максимальную и среднюю цену книг каждого автора . Вычисляемые столбцы назвать Минимальная_цена, Максимальная_цена и Средняя_цена соответственно. [(сайт)](https://stepik.org/lesson/297515/step/4?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select  author,
        MIN(price) AS "Минимальная_цена",
        MAX(price) AS "Максимальная_цена",
        AVG(price) AS "Средняя_цена"
from   book
group by author
```

</details>

Шаг_5. Для каждого автора вычислить суммарную стоимость книг S (имя столбца Стоимость), а также вычислить налог на добавленную стоимость  для полученных сумм (имя столбца НДС ) , который включен в стоимость и составляет 18% (k=18),  а также стоимость книг  (Стоимость_без_НДС) без него. Значения округлить до двух знаков после запятой. В запросе для расчета НДС(tax)  и Стоимости без НДС(S_without_tax). [(сайт)](https://stepik.org/lesson/297515/step/5?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select author, 
       sum(price*amount) as "Стоимость",
       round(sum(price*amount*0.18/1.18),2) as "НДС",
       round(sum(price*amount/1.18),2) as "Стоимость_без_НДС"
from  book      
group by author
```

</details>

Шаг_6. Вывести цену самой дешевой книги, цену самой дорогой и среднюю цену всех книг на складе. Названия столбцов Минимальная_цена, Максимальная_цена, Средняя_цена соответственно. Среднюю цену округлить до двух знаков после запятой. [(сайт)](https://stepik.org/lesson/297515/step/6?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select min(price) as "Минимальная_цена",
       max(price) as "Максимальная_цена",
       round(avg(price),2) as "Средняя_цена"
from  book  
```

</details>

Шаг_7. Вычислить среднюю цену и суммарную стоимость тех книг, количество экземпляров которых принадлежит интервалу от 5 до 14, включительно. Столбцы назвать Средняя_цена и Стоимость, значения округлить до 2-х знаков после запятой. [(сайт)](https://stepik.org/lesson/297515/step/7?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select round(avg(price),2) as "Средняя_цена",
       sum(price*amount) as "Стоимость"       
from book 
where amount between 5 and 14  
```

</details>

Шаг_8. Посчитать стоимость всех экземпляров каждого автора без учета книг «Идиот» и «Белая гвардия». В результат включить только тех авторов, у которых суммарная стоимость книг (без учета книг «Идиот» и «Белая гвардия») более 5000 руб. Вычисляемый столбец назвать Стоимость. Результат отсортировать по убыванию стоимости. [(сайт)](https://stepik.org/lesson/297515/step/8?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select author, sum(price*amount) as "Стоимость"
from book
where title not in("Идиот", "Белая гвардия")
group by author
having  sum(price*amount) > 5000
order by Стоимость desc  
```

</details>

Шаг_9. Вывести авторов и суммарную стоимость их книг, если хотя бы одна их книга по цене выше средней. [(сайт)](https://stepik.org/lesson/297515/step/9?unit=279275)

<details>
  <summary>Решение</summary>

```mysql
select  author, sum(price*amount) as "Стоимость" 
from book 
group by author
having sum(amount) > avg(amount)  
```

</details>

### 1.4   Вложенные запросы

Шаг_2. Вывести информацию (автора, название и цену) о  книгах, цены которых меньше или равны средней цене книг на складе. Информацию вывести в отсортированном по убыванию цены виде. Среднее вычислить как среднее по цене книги. [(сайт)](https://stepik.org/lesson/297514/step/2?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
select author, title, price 
from book
where price <= (select avg(price) from book)
order by price desc
```

</details>

Шаг_3. Вывести информацию (автора, название и цену) о тех книгах, цены которых превышают минимальную цену книги на складе не более чем на 150 рублей в отсортированном по возрастанию цены виде. [(сайт)](https://stepik.org/lesson/297514/step/3?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
SELECT author, title, price
FROM book
WHERE (price - (SELECT MIN(price) FROM book)) <=150
ORDER BY price
```

</details>

Шаг_4. Вывести информацию (автора, книгу и количество) о тех книгах, количество экземпляров которых в таблице book не дублируется. [(сайт)](https://stepik.org/lesson/297514/step/4?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
select author, title, amount 
from book
where amount in (
                select amount from book
                group by amount  
                having count(*) = 1
                )
```

</details>

Шаг_5. Вывести информацию о книгах(автор, название, цена), цена которых меньше самой большой из минимальных цен, вычисленных для каждого автора. [(сайт)](https://stepik.org/lesson/297514/step/5?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
select author, title, price
from book
where price < ANY( SELECT MIN(price) 
                   FROM book 
                   GROUP BY author
                   having MIN(price)
                  )
```

</details>

Шаг_6. Посчитать сколько и каких экземпляров книг нужно заказать поставщикам, чтобы на складе стало одинаковое количество экземпляров каждой книги, равное значению самого большего количества экземпляров одной книги на складе. Вывести название книги, ее автора, текущее количество экземпляров на складе и количество заказываемых экземпляров книг. Последнему столбцу присвоить имя Заказ. В результат не включать книги, которые заказывать не нужно. [(сайт)](https://stepik.org/lesson/297514/step/6?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
select title, author, amount, ((select max(amount) from book) - amount) as "Заказ" 
from book
where ((select max(amount) from book) - amount) <> 0 
```

</details>

Шаг_7. При продаже всех книг, какая книга принесет больше всего выручки, в процентах.
Отсортировать по убыванию процентов. [(сайт)](https://stepik.org/lesson/297514/step/7?unit=279274)

<details>
  <summary>Решение</summary>

```mysql
select author, title, price, amount, round(price*amount/(select sum(price*amount) from book)*100,2) as  income_percent 
from book
order by 5 desc 
```

</details>

### 1.5 Запросы корректировки данных

Шаг_2. Создать таблицу поставок (supply), которая имеет ту же структуру, что и таблиц book. [(сайт)](https://stepik.org/lesson/305012/step/2?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE supply(
    supply_id INT PRIMARY KEY AUTO_INCREMENT, 
    title VARCHAR(50),
    author 	VARCHAR(30),
    price  DECIMAL(8, 2),
    amount INT
)
```

</details>

Шаг_3. Занесите в таблицу supply четыре записи. [(сайт)](https://stepik.org/lesson/305012/step/3?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
insert into supply (title, author, price, amount)
values 
    ('Лирика', 'Пастернак Б.Л.', 518.99, 2),
    ('Черный человек', 'Есенин С.А.', 570.20, 6),
    ('Белая гвардия', 'Булгаков М.А.', 540.50, 7),
    ('Идиот', 'Достоевский Ф.М.', 360.80, 3);
select * from supply
```

</details>

Шаг_4. Добавить из таблицы supply в таблицу book, все книги, кроме книг, написанных Булгаковым М.А. и Достоевским Ф.М. [(сайт)](https://stepik.org/lesson/305012/step/4?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
insert into book (title,author,price,amount)
select title,author,price,amount
from supply 
WHERE author NOT IN ('Булгаков М.А.', 'Достоевский Ф.М.')
```

</details>

Шаг_5. Занести из таблицы supply в таблицу book только те книги, авторов которых нет в  book. [(сайт)](https://stepik.org/lesson/305012/step/5?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
insert into book (title,author,price,amount)
select title,author,price,amount
from supply 
WHERE author NOT IN (select author from book)
```

</details>

Шаг_6. Уменьшить на 10% цену тех книг в таблице book, количество которых принадлежит интервалу от 5 до 10, включая границы. [(сайт)](https://stepik.org/lesson/305012/step/6?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
UPDATE book 
SET price = 0.9 * price 
WHERE amount between 5 and 10
```

</details>

Шаг_7. В таблице book необходимо скорректировать значение для покупателя в столбце buy таким образом, чтобы оно не превышало количество экземпляров книг, указанных в столбце amount. А цену тех книг, которые покупатель не заказывал, снизить на 10%. [(сайт)](https://stepik.org/lesson/305012/step/7?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
UPDATE book 
SET buy = IF(amount < buy, buy-(buy - amount) , buy),
price = IF(amount-buy > buy, price -(price * 0.1) , price)
```

</details>

Шаг_8. Для тех книг в таблице book , которые есть в таблице supply, не только увеличить их количество в таблице book ( увеличить их количество на значение столбца amountтаблицы supply), но и пересчитать их цену (для каждой книги найти сумму цен из таблиц book и supply и разделить на 2). [(сайт)](https://stepik.org/lesson/305012/step/8?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
UPDATE book, supply
SET book.amount = book.amount + supply.amount,
    book.price = (book.price + supply.price) / 2
WHERE book.title = supply.title AND book.author = supply.author;

SELECT * FROM book;
```

</details>

Шаг_9. Удалить из таблицы supply книги тех авторов, общее количество экземпляров книг которых в таблице book превышает 10. [(сайт)](https://stepik.org/lesson/305012/step/9?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
DELETE FROM supply 
WHERE author  IN (
        SELECT author  
        FROM book
        GROUP BY author
        HAVING SUM(amount) > 10
       );


SELECT * FROM supply;
```

</details>

Шаг_10*. Создать таблицу заказ (ordering), куда включить авторов и названия тех книг, количество экземпляров которых в таблице book меньше среднего количества экземпляров книг в таблице book. В таблицу включить столбец   amount, в котором для всех книг указать одинаковое значение - среднее количество экземпляров книг в таблице book. [(сайт)](https://stepik.org/lesson/305012/step/10?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE ordering AS
SELECT author, title,  @AVG as amount
FROM book
WHERE amount < (@AVG := (SELECT ROUND(AVG(amount)) FROM book));
SELECT * FROM ordering;
```

</details>

Шаг_11. Занести из таблицы supply в таблицу book только те книги, названия которых отсутствуют в таблице book, при этом количество этих книг в таблице supply должно обнулиться. Т.е. все эти книги со склада передали в магазин. [(сайт)](https://stepik.org/lesson/305012/step/11?unit=287020)

<details>
  <summary>Решение</summary>

```mysql
/* Вставляем из нужных строк все значения, кроме amount */
INSERT INTO book (title, author, price)
SELECT title, author, price FROM supply
WHERE (title, author) NOT IN (SELECT title, author FROM book);
/* Обновляем amount в двух таблицах*/
UPDATE book, supply SET
    book.amount = supply.amount,
    supply.amount = 0
WHERE book.title = supply.title AND book.amount IS NULL;
```

</details>

### 1.6 Таблица "Командировки", запросы на выборку

Шаг_2. Вывести из таблицы trip информацию о командировках тех сотрудников, фамилия которых заканчивается на букву «а», в отсортированном по убыванию даты последнего дня командировки виде. В результат включить столбцы name, city, per_diem, date_first, date_last. [(сайт)](https://stepik.org/lesson/297510/step/2?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, city, per_diem, date_first, date_last
from trip
where name like '%а %'
order by date_last desc
```

</details>

Шаг_3. Вывести в алфавитном порядке фамилии и инициалы тех сотрудников, которые были в командировке в Москве. [(сайт)](https://stepik.org/lesson/297510/step/3?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select distinct name 
from trip
where city = 'Москва'
order by name asc 
```

</details>

Шаг_4. Для каждого города посчитать, сколько раз сотрудники в нем были.  Информацию вывести в отсортированном в алфавитном порядке по названию городов. Вычисляемый столбец назвать Количество.  [(сайт)](https://stepik.org/lesson/297510/step/4?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select city, count(name) as 'Количество'
from trip
group by city
order by city asc 
```

</details>

Шаг_5. Вывести два города, в которых чаще всего были в командировках сотрудники. Вычисляемый столбец назвать Количество.  [(сайт)](https://stepik.org/lesson/297510/step/5?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select city, count(name) as 'Количество'
from trip 
group by city 
order by 2 desc
limit 2
```

</details>

Шаг_6. Вывести информацию о командировках во все города кроме Москвы и Санкт-Петербурга (фамилии и инициалы сотрудников, город ,  длительность командировки в днях, при этом первый и последний день относится к периоду командировки). Последний столбец назвать Длительность. Информацию вывести в упорядоченном по убыванию длительности поездки, а потом по убыванию названий городов (в обратном алфавитном порядке).  [(сайт)](https://stepik.org/lesson/297510/step/6?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, city, DATEDIFF(date_last,date_first)+1 as 'Длительность'
from trip
where city not in('Москва','Санкт-Петербург')
order by 3 desc, 2 desc
```

</details>

Шаг_7. Вывести информацию о командировках сотрудника(ов), которые были самыми короткими по времени. В результат включить столбцы name, city, date_first, date_last.  [(сайт)](https://stepik.org/lesson/297510/step/7?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, city, date_first, date_last
from trip
where DATEDIFF(date_last,date_first) in (
    select MIN(DATEDIFF(date_last,date_first)) as 'min'
    from trip)
```

</details>

Шаг_8. Вывести информацию о командировках, начало и конец которых относятся к одному месяцу (год может быть любой). В результат включить столбцы name, city, date_first, date_last. Строки отсортировать сначала  в алфавитном порядке по названию города, а затем по фамилии сотрудника .  [(сайт)](https://stepik.org/lesson/297510/step/8?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, city, date_first, date_last
from trip
where MONTH(date_first) = MONTH(date_last)
order by city asc, name asc  
```

</details>

Шаг_9. Вывести название месяца и количество командировок для каждого месяца. Считаем, что командировка относится к некоторому месяцу, если она началась в этом месяце. Информацию вывести сначала в отсортированном по убыванию количества, а потом в алфавитном порядке по названию месяца виде. Название столбцов – Месяц и Количество.  [(сайт)](https://stepik.org/lesson/297510/step/9?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select MONTHNAME(date_first) as  'Месяц' , count(*) as 'Количество'
from trip 
group by 1
order by 2 desc, 1 asc  
```

</details>

Шаг_10. Вывести сумму суточных (произведение количества дней командировки и размера суточных) для командировок, первый день которых пришелся на февраль или март 2020 года. Значение суточных для каждой командировки занесено в столбец per_diem. Вывести фамилию и инициалы сотрудника, город, первый день командировки и сумму суточных. Последний столбец назвать Сумма. Информацию отсортировать сначала  в алфавитном порядке по фамилиям сотрудников, а затем по убыванию суммы суточных.  [(сайт)](https://stepik.org/lesson/297510/step/10?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, city, date_first, per_diem * (DATEDIFF(date_last,date_first)+1) as 'Сумма'
from trip
where MONTH(date_first) in (2,3) and YEAR(date_first) = 2020 
order by name asc, per_diem asc 
```

</details>

Шаг_11. Вывести фамилию с инициалами и общую сумму суточных, полученных за все командировки для тех сотрудников, которые были в командировках больше чем 3 раза, в отсортированном по убыванию сумм суточных виде. Последний столбец назвать Сумма.  [(сайт)](https://stepik.org/lesson/297510/step/11?unit=279270)

<details>
  <summary>Решение</summary>

```mysql
select name, sum(per_diem*(datediff(date_last,date_first)+1)) as 'Сумма'
from trip 
where name in (select name
               from trip
               group by name
               having count(*)>3)
group by name
order by 2 desc
```

</details>

### 1.7 Таблица "Нарушения ПДД", запросы корректировки

Шаг_2. Создать таблицу fine. [(сайт)](https://stepik.org/lesson/305762/step/2?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE fine(
    fine_id INT PRIMARY KEY AUTO_INCREMENT, 
    name VARCHAR(30),
    number_plate VARCHAR(6),
    violation VARCHAR(50),
    sum_fine  DECIMAL(8, 2),
    date_violation date,
    date_payment date)
```

</details>

Шаг_3. В таблицу fine первые 5 строк уже занесены. Добавить в таблицу записи с ключевыми значениями 6, 7, 8. [(сайт)](https://stepik.org/lesson/305762/step/3?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
INSERT INTO fine
(name, number_plate, violation, sum_fine, date_violation, date_payment)
VALUES
('Баранов П.Е.', 'Р523ВТ', 'Превышение скорости(от 40 до 60)', Null, '2020-02-14', Null),
('Абрамова К.А.', 'О111АВ', 'Проезд на запрещающий сигнал', Null, '2020-02-23', Null),
('Яковлев Г.Р.', 'Т330ТТ', 'Проезд на запрещающий сигнал', Null, '2020-03-03', Null);
SELECT * FROM fine
```

</details>

Шаг_4. Занести в таблицу fine суммы штрафов, которые должен оплатить водитель, в соответствии с данными из таблицы traffic_violation. При этом суммы заносить только в пустые поля столбца  sum_fine. Таблица traffic_violationсоздана и заполнена. Важно! Сравнение значения столбца с пустым значением осуществляется с помощью оператора IS NULL. [(сайт)](https://stepik.org/lesson/305762/step/4?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
UPDATE fine
SET sum_fine=(SELECT sum_fine FROM traffic_violation WHERE traffic_violation.violation=fine.violation)
WHERE sum_fine is NULL
```

</details>

Шаг_5. Вывести фамилию, номер машины и нарушение только для тех водителей, которые на одной машине нарушили одно и то же правило   два и более раз. При этом учитывать все нарушения, независимо от того оплачены они или нет. Информацию отсортировать в алфавитном порядке, сначала по фамилии водителя, потом по номеру машины и, наконец, по нарушению. [(сайт)](https://stepik.org/lesson/305762/step/5?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
SELECT name, number_plate, violation
FROM fine
GROUP BY name, number_plate, violation
HAVING COUNT(*)>1
ORDER BY name;
```

</details>

Шаг_6*. В таблице fine увеличить в два раза сумму неоплаченных штрафов для отобранных на предыдущем шаге записей.  [(сайт)](https://stepik.org/lesson/305762/step/6?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
update fine
set sum_fine = sum_fine * 2
where date_payment is null and 
(name, number_plate, violation) in
(select * from (select name, number_plate, violation
                from fine
                group by name, number_plate, violation
                having count(*) > 1) as T);
```

</details>

Шаг_7. Водители оплачивают свои штрафы. В таблице payment занесены даты их оплаты:  [(сайт)](https://stepik.org/lesson/305762/step/7?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
UPDATE   fine f, payment p 
SET f.date_payment = p.date_payment, 
    f.sum_fine = IF( DATEDIFF(p.date_payment, p.date_violation) <= 20, f.sum_fine / 2, f.sum_fine) 
WHERE (f.name, f.number_plate, f.violation) = (p.name, p.number_plate, p.violation)
       AND f.date_payment IS null;  
   
SELECT * FROM fine;
```

</details>

Шаг_8. Создать новую таблицу back_payment, куда внести информацию о неоплаченных штрафах (Фамилию и инициалы водителя, номер машины, нарушение, сумму штрафа  и  дату нарушения) из таблицы fine.  [(сайт)](https://stepik.org/lesson/305762/step/8?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE back_payment AS
 (
    SELECT name, number_plate, violation, sum_fine, date_violation
    FROM fine AS f
    WHERE f.date_payment IS NULL
  )
```

</details>

Шаг_9. Удалить из таблицы fine информацию о нарушениях, совершенных раньше 1 февраля 2020 года.   [(сайт)](https://stepik.org/lesson/305762/step/9?unit=287773)

<details>
  <summary>Решение</summary>

```mysql
delete from fine
where date_violation < '2020-02-01'
```

</details>

### 2.1 Связи между таблицами

Шаг_6. Создать таблицу author. [(сайт)](https://stepik.org/lesson/308885/step/6?unit=291011)

<details>
  <summary>Решение</summary>

```mysql
create table author (
  author_id  INT PRIMARY KEY AUTO_INCREMENT,
  name_author VARCHAR(50))
```

</details>

Шаг_7. Заполнить таблицу author. [(сайт)](https://stepik.org/lesson/308885/step/7?unit=291011)

<details>
  <summary>Решение</summary>

```mysql
insert into author (name_author  )
value ('Булгаков М.А.'),
        ('Достоевский Ф.М.'),
        ('Есенин С.А.'),
        ('Пастернак Б.Л.')
```

</details>

Шаг_8. Перепишите запрос на создание таблицы book , чтобы ее структура соответствовала структуре, показанной на логической схеме (таблица genre уже создана, порядок следования столбцов - как на логической схеме в таблице book, genre_id  - внешний ключ) . Для genre_id ограничение о недопустимости пустых значений не задавать. В качестве главной таблицы для описания поля  genre_idиспользовать таблицу genre. [(сайт)](https://stepik.org/lesson/308885/step/8?unit=291011)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT, 
    title VARCHAR(50), 
    author_id INT NOT NULL, 
    genre_id INT,
    price DECIMAL(8,2), 
    amount INT, 
    FOREIGN KEY (author_id)  REFERENCES author (author_id),
    FOREIGN KEY (genre_id)  REFERENCES genre (genre_id) 
);
```

</details>

Шаг_9. Создать таблицу book той же структуры, что и на предыдущем шаге. Будем считать, что при удалении автора из таблицы author, должны удаляться все записи о книгах из таблицы book, написанные этим автором. А при удалении жанра из таблицы genre для соответствующей записи book установить значение Null в столбце genre_id.  [(сайт)](https://stepik.org/lesson/308885/step/9?unit=291011)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE book (
    book_id INT PRIMARY KEY AUTO_INCREMENT, 
    title VARCHAR(50), 
    author_id INT NOT NULL, 
    genre_id INT,
    price DECIMAL(8,2), 
    amount INT, 
    FOREIGN KEY (author_id)  REFERENCES author (author_id) ON DELETE CASCADE,
    FOREIGN KEY (genre_id)  REFERENCES genre (genre_id) ON DELETE SET NULL
);
```

</details>

Шаг_11. Добавьте три последние записи (с ключевыми значениями 6, 7, 8) в таблицу book.  [(сайт)](https://stepik.org/lesson/308885/step/11?unit=291011)

<details>
  <summary>Решение</summary>

```mysql
insert into book (title, author_id, genre_id,price, amount)
value ('Стихотворения и поэмы', 3, 2, 650.00, 15),
      ('Черный человек', 3, 2, 570.20, 6),
      ('Лирика', 4, 2, 518.99, 2)
```

</details>


### 2.2 Запросы на выборку, соединение таблиц

Шаг_2. Вывести название, жанр и цену тех книг, количество которых больше 8, в отсортированном по убыванию цены виде. [(сайт)](https://stepik.org/lesson/308886/step/2?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select title, name_genre, price 
from book b inner join  genre g
 on b.genre_id = g.genre_id
where amount > 8 
order by price desc
```

</details>

Шаг_3. Вывести все жанры, которые не представлены в книгах на складе. [(сайт)](https://stepik.org/lesson/308886/step/3?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select name_genre
from genre left join book
on genre.genre_id = book.genre_id
where title is null
```

</details>

Шаг_4. Необходимо в каждом городе провести выставку книг каждого автора в течение 2020 года. Дату проведения выставки выбрать случайным образом. Создать запрос, который выведет город, автора и дату проведения выставки. Последний столбец назвать Дата. Информацию вывести, отсортировав сначала в алфавитном порядке по названиям городов, а потом по убыванию дат проведения выставок. [(сайт)](https://stepik.org/lesson/308886/step/4?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select name_city,name_author, DATE_ADD('2020-01-01', INTERVAL ROUND(RAND() * 365) DAY) AS Дата
from city cross join author
order by name_city asc, Дата desc
```

</details>

Шаг_5. Вывести информацию о книгах (жанр, книга, автор), относящихся к жанру, включающему слово «роман» в отсортированном по названиям книг виде. [(сайт)](https://stepik.org/lesson/308886/step/5?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
SELECT name_genre, title, name_author
from book join genre using(genre_id)
          join author using(author_id)
where name_genre = 'Роман'
order by title
```

</details>

Шаг_6. Посчитать количество экземпляров  книг каждого автора из таблицы author.  Вывести тех авторов,  количество книг которых меньше 10, в отсортированном по возрастанию количества виде. Последний столбец назвать Количество. [(сайт)](https://stepik.org/lesson/308886/step/6?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select name_author, sum(amount) as 'Количество'
from book right join author
          using(author_id)          
group by name_author
having Количество < 10 or Количество is null
order by Количество asc
```

</details>

Шаг_7. Вывести в алфавитном порядке всех авторов, которые пишут только в одном жанре. Поскольку у нас в таблицах так занесены данные, что у каждого автора книги только в одном жанре,  для этого запроса внесем изменения в таблицу book. Пусть у нас  книга Есенина «Черный человек» относится к жанру «Роман», а книга Булгакова «Белая гвардия» к «Приключениям» (эти изменения в таблицы уже внесены). [(сайт)](https://stepik.org/lesson/308886/step/7?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
 select name_author 
 from  author
 where author_id in        
                    (select author_id
                    from book join genre using(genre_id)
                    group by author_id
                    having count(distinct genre_id) = 1)
order by name_author asc
```

</details>

Шаг_8. Вывести информацию о книгах (название книги, фамилию и инициалы автора, название жанра, цену и количество экземпляров книги), написанных в самых популярных жанрах, в отсортированном в алфавитном порядке по названию книг виде. Самым популярным считать жанр, общее количество экземпляров книг которого на складе максимально. [(сайт)](https://stepik.org/lesson/308886/step/8?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select  title, name_author, name_genre, price, amount              
from book join genre  using(genre_id)
          join author  using(author_id) 
where genre_id in ( select  genre_id
                    from book  
                    group by genre_id
                    having sum(amount) = (SELECT SUM(amount)
                                          FROM book
                                          GROUP BY genre_id
                                          limit 1))                                           
order by  title
```

</details>

Шаг_9. Если в таблицах supply  и book есть одинаковые книги, которые имеют равную цену,  вывести их название и автора, а также посчитать общее количество экземпляров книг в таблицах supply и book,  столбцы назвать Название, Автор  и Количество. [(сайт)](https://stepik.org/lesson/308886/step/9?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select title as 'Название' ,name_author as 'Автор' , book.amount+supply.amount as 'Количество'
from book join author using(author_id)
          join supply USING(title, price)
where price in (select distinct price
                from supply)
```

</details>

Шаг_10. Для каждого автора из таблицы author вывести количество книг, написанных им в каждом жанре.
Вывод: ФИО автора, жанр, количество. Отсортировать по фамилии, затем - по убыванию количества написанных книг. [(сайт)](https://stepik.org/lesson/308886/step/10?unit=291012)

<details>
  <summary>Решение</summary>

```mysql
select name_author, name_genre, count(title) as количество
from author  inner join genre
left join book using(author_id, genre_id)
group by name_author, name_genre
order by name_author, количество desc
```

</details>

### 2.3 Запросы корректировки, соединение таблиц

Шаг_2. Для книг, которые уже есть на складе (в таблице book), но по другой цене, чем в поставке (supply),  необходимо в таблице book увеличить количество на значение, указанное в поставке,  и пересчитать цену. А в таблице  supply обнулить количество этих книг. [(сайт)](https://stepik.org/lesson/308887/step/2?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
UPDATE book 
     INNER JOIN author ON author.author_id = book.author_id
     INNER JOIN supply ON book.title = supply.title 
                         and supply.author = author.name_author
SET book.amount = book.amount + supply.amount, supply.amount = 0,
book.price = (book.price*book.amount + supply.price*supply.amount)/(book.amount + supply.amount)
WHERE book.price <> supply.price;

SELECT * FROM book;

SELECT * FROM supply;
```

</details>

Шаг_3. Включить новых авторов в таблицу author с помощью запроса на добавление, а затем вывести все данные из таблицы author.  Новыми считаются авторы, которые есть в таблице supply, но нет в таблице author. [(сайт)](https://stepik.org/lesson/308887/step/3?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
insert into author (name_author)
select supply.author
from supply left join author on supply.author = author.name_author
where name_author is null
```

</details>

Шаг_4. Добавить новые книги из таблицы supply в таблицу book на основе сформированного выше запроса. Затем вывести для просмотра таблицу book. [(сайт)](https://stepik.org/lesson/308887/step/4?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
INSERT INTO book (title, author_id, price, amount)
SELECT title, author_id, price, amount
FROM 
    author 
    INNER JOIN supply ON author.name_author = supply.author
WHERE amount <> 0;

SELECT * FROM book; 
```

</details>

Шаг_5. Занести для книги «Стихотворения и поэмы» Лермонтова жанр «Поэзия», а для книги «Остров сокровищ» Стивенсона - «Приключения». (Использовать два запроса) [(сайт)](https://stepik.org/lesson/308887/step/5?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
UPDATE book
SET genre_id=2
WHERE book_id=10;
UPDATE book
SET genre_id=3 
WHERE book_id=11;
SELECT*FROM book;
```

</details>

Шаг_6. Удалить всех авторов и все их книги, общее количество книг которых меньше 20. [(сайт)](https://stepik.org/lesson/308887/step/6?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
delete from author
where author_id in (
                    select author_id
                    from book
                    group by   author_id 
                    having sum(amount) < 20)
```

</details>

Шаг_7. Удалить все жанры, к которым относится меньше 4-х наименований книг. В таблице book для этих жанров установить значение Null. [(сайт)](https://stepik.org/lesson/308887/step/7?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
DELETE FROM genre
WHERE genre_id IN ( SELECT genre_id
                   FROM book
                   GROUP BY genre_id
                   HAVING count(title) < 4);
SELECT *
FROM book;

SELECT *
FROM genre;
```

</details>

Шаг_8. Удалить всех авторов, которые пишут в жанре "Поэзия". Из таблицы book удалить все книги этих авторов. В запросе для отбора авторов использовать полное название жанра, а не его id. [(сайт)](https://stepik.org/lesson/308887/step/8?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
DELETE FROM author
USING 
    author 
    LEFT JOIN book ON author.author_id = book.author_id
    LEFT JOIN genre on genre.genre_id = book.genre_id
WHERE genre.name_genre = 'Поэзия';

SELECT * FROM author;

SELECT * FROM book;
```

</details>


Шаг_9. Добавим книги, которых нет в book, из supply. Для этого сначала добавим авторов в author, затем книги, затем вручную укажем жанр новым книгам.
Изменим цену книг в book, заменив ее на среднюю цену книг того же жанра. То есть в основном запросе на изменение цены UPDATE book SET... мы пишем подзапрос, который считает среднюю цену книг каждого жанра (AVG(price), GROUP BY genre_id) и обновляет цену в зависимости от того, к какому жанру принадлежит конкретная книга. [(сайт)](https://stepik.org/lesson/308887/step/9?unit=291013)

<details>
  <summary>Решение</summary>

```mysql
select * from genre;
INSERT INTO genre (name_genre) VALUES ('Страшилка');
select * from genre;

select * from book;

UPDATE book
SET genre_id = (
    SELECT
        genre_id
    FROM genre
    WHERE name_genre = 'Страшилка')
WHERE author_id IN (
    SELECT 
        author_id
    FROM author
    WHERE name_author IN ('Достоевский Ф.М.', 'Булгаков М.А.'));
select * from book;


select * from supply;

UPDATE supply
SET amount = supply.amount + 100
WHERE author IN ('Достоевский Ф.М.', 'Булгаков М.А.');
```

</details>

### 2.4 База данных «Интернет-магазин книг», запросы на выборку

Шаг_5. Вывести все заказы Баранова Павла (id заказа, какие книги, по какой цене и в каком количестве он заказал) в отсортированном по номеру заказа и названиям книг виде. [(сайт)](https://stepik.org/lesson/308891/step/5?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
select distinct buy_id, title, price, buy_book.amount 
from buy_book inner join book 
              using (book_id)
              inner join buy
              using (buy_id)
              inner join client
              using (client_id)
where name_client = 'Баранов Павел'
order by 1,2
```

</details>

Шаг_6. Посчитать, сколько раз была заказана каждая книга, для книги вывести ее автора (нужно посчитать, в каком количестве заказов фигурирует каждая книга).  Вывести фамилию и инициалы автора, название книги, последний столбец назвать Количество. Результат отсортировать сначала  по фамилиям авторов, а потом по названиям книг. [(сайт)](https://stepik.org/lesson/308891/step/6?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
select name_author, title, count(buy_id) as 'Количество'
from buy_book right join book using (book_id)
              join author using (author_id)
group by name_author, title
order by 1,2
```

</details>

Шаг_7. Вывести города, в которых живут клиенты, оформлявшие заказы в интернет-магазине. Указать количество заказов в каждый город, этот столбец назвать Количество. Информацию вывести по убыванию количества заказов, а затем в алфавитном порядке по названию городов. [(сайт)](https://stepik.org/lesson/308891/step/7?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
select  name_city, count(client_id)  as 'Количество'
from city join client using(city_id)
          join buy using(client_id)
group by name_city
order by 2 desc, 1 asc
```

</details>

Шаг_8. Вывести номера всех оплаченных заказов и даты, когда они были оплачены. [(сайт)](https://stepik.org/lesson/308891/step/8?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
select buy_id, date_step_end
from buy_step join step using(step_id)
where name_step = 'Оплата' and date_step_end
```

</details>

Шаг_9. Вывести информацию о каждом заказе: его номер, кто его сформировал (фамилия пользователя) и его стоимость (сумма произведений количества заказанных книг и их цены), в отсортированном по номеру заказа виде. Последний столбец назвать Стоимость. [(сайт)](https://stepik.org/lesson/308891/step/9?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
select buy.buy_id, name_client, sum(buy_book.amount*price) as 'Стоимость'
from buy join client using(client_id)
         join buy_book using(buy_id)
         join book using(book_id)
group by  buy.buy_id, name_client
order by 1
```

</details>

Шаг_10. Вывести номера заказов (buy_id) и названия этапов,  на которых они в данный момент находятся. Если заказ доставлен –  информацию о нем не выводить. Информацию отсортировать по возрастанию buy_id. [(сайт)](https://stepik.org/lesson/308891/step/10?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT buy_id, name_step
FROM buy_step JOIN step USING(step_id)
WHERE date_step_beg AND date_step_end IS NULL
ORDER BY 1;
```

</details>

Шаг_11*. В таблице city для каждого города указано количество дней, за которые заказ может быть доставлен в этот город (рассматривается только этап Транспортировка). Для тех заказов, которые прошли этап транспортировки, вывести количество дней за которое заказ реально доставлен в город. А также, если заказ доставлен с опозданием, указать количество дней задержки, в противном случае вывести 0. В результат включить номер заказа (buy_id), а также вычисляемые столбцы Количество_дней и Опоздание. Информацию вывести в отсортированном по номеру заказа виде. [(сайт)](https://stepik.org/lesson/308891/step/11?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT
    buy_id,
    (@D := DATEDIFF(date_step_end, date_step_beg)) AS Количество_дней,
    GREATEST(@D - days_delivery, 0) AS Опоздание
FROM
    buy
     JOIN buy_step USING(buy_id)
     JOIN step     USING(step_id)
     JOIN client   USING(client_id)
     JOIN city     USING(city_id)
WHERE
    name_step = 'Транспортировка' AND date_step_end 
ORDER BY buy_id;
```

</details>

Шаг_12. Выбрать всех клиентов, которые заказывали книги Достоевского, информацию вывести в отсортированном по алфавиту виде. В решении используйте фамилию автора, а не его id. [(сайт)](https://stepik.org/lesson/308891/step/12?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT DISTINCT name_client FROM author
    JOIN book ON (author.author_id=book.author_id) AND (author.name_author="Достоевский Ф.М.")
    JOIN buy_book USING(book_id)
    JOIN buy USING(buy_id)
    JOIN client USING(client_id)
ORDER BY name_client;
```

</details>

Шаг_13. Вывести жанр (или жанры), в котором было заказано больше всего экземпляров книг, указать это количество. Последний столбец назвать Количество. [(сайт)](https://stepik.org/lesson/308891/step/13?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT genre.name_genre, SUM(buy_book.amount) AS Количество
FROM buy_book JOIN book using(book_id)
              JOIN genre using(genre_id) 
GROUP BY genre.genre_id
HAVING SUM(buy_book.amount) = 
            (SELECT MAX(sum_amount) AS max_sum_amount FROM (SELECT SUM(buy_book.amount) AS sum_amount 
            FROM buy_book 
            INNER JOIN book ON buy_book.book_id=book.book_id
            INNER JOIN genre ON book.genre_id=genre.genre_id
            GROUP BY genre.genre_id)mg)    
```

</details>

Шаг_14. Сравнить ежемесячную выручку от продажи книг за текущий и предыдущий годы. Для этого вывести год, месяц, сумму выручки в отсортированном сначала по возрастанию месяцев, затем по возрастанию лет виде. Название столбцов: Год, Месяц, Сумма. [(сайт)](https://stepik.org/lesson/308891/step/14?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT Year(date_payment) as 'Год' ,MONTHNAME(date_payment) as 'Месяц', sum(amount*price) as 'Сумма' 
FROM 
    buy_archive
group by Year(date_payment),MONTHNAME(date_payment)   
UNION ALL
SELECT Year(date_step_end),MONTHNAME(date_step_end), sum(buy_book.amount*price)
FROM 
    book 
    INNER JOIN buy_book USING(book_id)
    INNER JOIN buy USING(buy_id) 
    INNER JOIN buy_step USING(buy_id)
    INNER JOIN step USING(step_id)                  
WHERE  date_step_end IS NOT Null and name_step = "Оплата" 
group by Year(date_step_end),MONTHNAME(date_step_end)
order by Месяц asc,  Год asc  
```

</details>

Шаг_15. Для каждой отдельной книги необходимо вывести информацию о количестве проданных экземпляров и их стоимости за 2020 и 2019 год . За 2020 год проданными считать те экземпляры, которые уже оплачены. Вычисляемые столбцы назвать Количество и Сумма. Информацию отсортировать по убыванию стоимости. [(сайт)](https://stepik.org/lesson/308891/step/15?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT result.title, sum(result.Количество) 'Количество', sum(result.Стоимость) 'Сумма'
FROM 
    (SELECT book.title, buy_book.amount 'Количество', price * buy_book.amount 'Стоимость'  
     FROM book  JOIN buy_book USING (book_id) 
                JOIN buy USING (buy_id) 
                JOIN buy_step USING (buy_id) 
     WHERE date_step_end is not null and step_id = 1     

     UNION ALL

     SELECT 
     title, buy_archive.amount 'Стоимость', buy_archive.price * buy_archive.amount 'Количество'
     FROM buy_archive
     INNER JOIN book USING (book_id)) as result

GROUP BY 1
ORDER BY 3 DESC; 
```

</details>

Шаг_16. Вывести названия книг, которые ни разу не были заказаны, отсортировав в алфавитном порядке. [(сайт)](https://stepik.org/lesson/308891/step/16?unit=291017)

<details>
  <summary>Решение</summary>

```mysql
SELECT book.title FROM book
LEFT JOIN buy_book USING(book_id)
WHERE buy_book.amount IS NULL
ORDER BY 1;
```

</details>

### 2.5 База данных «Интернет-магазин книг», запросы корректировки

Шаг_2. Включить нового человека в таблицу с клиентами. Его имя Попов Илья, его email popov@test, проживает он в Москве. [(сайт)](https://stepik.org/lesson/310417/step/2?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
Insert into  client  (name_client, city_id, email)
select 'Попов Илья', (select city_id from city where name_city='Москва'), 'popov@test'
```

</details>

Шаг_3. Создать новый заказ для Попова Ильи. Его комментарий для заказа: «Связаться со мной по вопросу доставки». [(сайт)](https://stepik.org/lesson/310417/step/3?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
Insert into  buy  ( buy_description, client_id)
select 'Связаться со мной по вопросу доставки',
(select client_id from client where name_client='Попов Илья')
```

</details>

Шаг_4. В таблицу buy_book добавить заказ с номером 5. Этот заказ должен содержать книгу Пастернака «Лирика» в количестве двух экземпляров и книгу Булгакова «Белая гвардия» в одном экземпляре. [(сайт)](https://stepik.org/lesson/310417/step/4?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
Insert into  buy_book  ( buy_id, book_id, amount )

select 5, (select book_id from book join author using(author_id)
           where title ='Лирика' and name_author like 'Пастер%'), 2
           
UNION ALL

select 5, (select book_id from book join author using(author_id)
           where title ='Белая гвардия' and name_author like 'Булгак%'), 1
```

</details>

Шаг_5. Количество тех книг на складе, которые были включены в заказ с номером 5, уменьшить на то количество, которое в заказе с номером 5  указано. [(сайт)](https://stepik.org/lesson/310417/step/5?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
update book inner join buy_book using (book_id)
set book.amount=book.amount-buy_book.amount
where buy_book.buy_id=5;
```

</details>

Шаг_6. Создать счет (таблицу buy_pay) на оплату заказа с номером 5, в который включить название книг, их автора, цену, количество заказанных книг и  стоимость. Последний столбец назвать Стоимость. Информацию в таблицу занести в отсортированном по названиям книг виде. [(сайт)](https://stepik.org/lesson/310417/step/6?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE buy_pay AS
SELECT title, name_author, price, buy_book.amount, buy_book.amount * book.price AS Стоимость
FROM book JOIN buy_book USING (book_id)
          JOIN author USING (author_id)
WHERE buy_id=5
ORDER BY title;
```

</details>

Шаг_7. Создать общий счет (таблицу buy_pay) на оплату заказа с номером 5. Куда включить номер заказа, количество книг в заказе (название столбца Количество) и его общую стоимость (название столбца Итого). Для решения используйте ОДИН запрос. [(сайт)](https://stepik.org/lesson/310417/step/7?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
CREATE TABLE buy_pay AS
SELECT buy_book.buy_id, sum(buy_book.amount) Количество, sum(buy_book.amount * book.price) Итого
FROM book
INNER JOIN buy_book USING (book_id)
WHERE buy_id=5
group by 1;
```

</details>

Шаг_8. В таблицу buy_step для заказа с номером 5 включить все этапы из таблицы step, которые должен пройти этот заказ. В столбцы date_step_beg и date_step_end всех записей занести Null. [(сайт)](https://stepik.org/lesson/310417/step/8?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
INSERT INTO buy_step (buy_id, step_id, date_step_beg, date_step_end)
SELECT '5', step_id, NULL, NULL 
FROM step
WHERE step_id in (SELECT distinct step_id FROM step);
```

</details>

Шаг_9. В таблицу buy_step занести дату 12.04.2020 выставления счета на оплату заказа с номером 5. Правильнее было бы занести не конкретную, а текущую дату. Это можно сделать с помощью функции Now(). Но при этом в разные дни будут вставляться разная дата, и задание нельзя будет проверить, поэтому  вставим дату 12.04.2020. [(сайт)](https://stepik.org/lesson/310417/step/9?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
UPDATE buy_step
SET date_step_beg = '2020-04-12'
WHERE buy_id = 5 AND step_id = (SELECT step_id FROM step WHERE name_step = 'Оплата');
```

</details>

Шаг_10. Завершить этап «Оплата» для заказа с номером 5, вставив в столбец date_step_end дату 13.04.2020, и начать следующий этап («Упаковка»), задав в столбце date_step_beg для этого этапа ту же дату. Реализовать два запроса для завершения этапа и начала следующего. Они должны быть записаны в общем виде, чтобы его можно было применять для любых этапов, изменив только текущий этап. Для примера пусть это будет этап «Оплата». [(сайт)](https://stepik.org/lesson/310417/step/10?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
UPDATE buy_step SET date_step_end='2020-04-13'
WHERE buy_id=5 AND step_id IN (SELECT step_id FROM step WHERE name_step ='Оплата');
UPDATE buy_step SET date_step_beg='2020-04-13'
WHERE buy_id=5 AND step_id IN (SELECT step_id FROM step WHERE name_step ='Упаковка');
SELECT * FROM buy_step WHERE buy_id=5;
```

</details>

Шаг_10. Ввести количество заказов, находящихся в каждом из статусов. [(сайт)](https://stepik.org/lesson/310417/step/11?unit=292723)

<details>
  <summary>Решение</summary>

```mysql
SELECT name_step, count(bs.step_id) "Количество заказов"
FROM step s LEFT JOIN buy_step bs 
ON s.step_id=bs.step_id and date_step_beg AND date_step_end IS NULL
GROUP BY name_step 
ORDER BY 1
```

</details>



