# Решение заданий с курса по SQL на платформе [Stepik](https://stepik.org/catalog)

1.1 Отношение (таблица)

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

Шаг_10. Занесите три последние записи в таблицуbook,  первая запись уже добавлена на предыдущем шаге: [(сайт)](https://stepik.org/lesson/297508/step/10?unit=279268)

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


1.2 Выборка данных

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

