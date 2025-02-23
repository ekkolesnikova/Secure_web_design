1,2. Установили PostgreSQL сервер и создали БД lib.

3. Применили к ней скрипты из папки db. Скрипты выполним в порядке, указанном в имени файла. 
3.1 Восстановили данные из файла data.sql.

![image](https://user-images.githubusercontent.com/91749695/149949009-e03b8fae-d0e5-46a2-9bd6-0a96de3df163.png)
![image](https://user-images.githubusercontent.com/91749695/149949057-1201f40c-6aa0-4774-976e-dc6ff8fffcf7.png)

4. Установили nodejs.

 ![image](https://user-images.githubusercontent.com/91749695/149949108-87396b54-9c16-4377-b6e7-c78339f8c6ac.png)

5. Перейдем в папку lab2 и выполним в ней команду npm install.

![image](https://user-images.githubusercontent.com/91749695/149949132-538dded2-8ad5-48b4-9a41-43dccf8a1fb1.png)

6. Запустили сайт через Visual Studio Code или через команду npm start.
 
![image](https://user-images.githubusercontent.com/91749695/149949165-47ce0fa6-114c-4026-855c-3f0926a00399.png)
![image](https://user-images.githubusercontent.com/91749695/149949200-af66835c-e15f-412b-83f6-d7c036b67f84.png)

7. Войдем на сайт и увидим список книг и авторов.

 ![image](https://user-images.githubusercontent.com/91749695/149949235-037db49d-6b73-4c95-bbe3-61b9b833838d.png)

8. Обнаружим SQL – инъекцию.

![image](https://user-images.githubusercontent.com/91749695/149949270-aea9c020-fb98-4aff-82ce-a58f00d23ec7.png)

В случае неправильного заполнения поля «пароль», можно наблюдать полную команду SQL обращенную к базе данных Postrgres, эту команду и будем модифицировать.

Обход установленного фильтра, Получение данных из другой таблицы, Похищение пароля пользователя:

![image](https://user-images.githubusercontent.com/91749695/149949326-759068bf-0cd6-4994-87e4-14ac8e5841e1.png)
 
Воспользуемся этой уязвимостью для получения данных из другой таблицы с целью похищения пароля пользователя. Для этого введем в поле фильтра книг:
' union all select ba.id, users.name, users.pass from users, books_by_authors ba where ba.id = 1000--
 
 ![image](https://user-images.githubusercontent.com/91749695/149949447-0b13c190-3607-4dc6-971f-428df13d7ecb.png)

10. Исправить уязвимость.
Для того чтобы исправить уязвимость.

 ![image](https://user-images.githubusercontent.com/91749695/149949475-314f4cb7-9dd4-4613-9a6d-69f851df8572.png)

11. В отчёте привести пример того, что уязвимости больше не эксплуатируются.
Для того чтобы защитится от данной уязвимости нужно сделать невозможным добавление в поиск дополнительного подзапроса, для этого добавим в исключение символ «‘», который в случае нахождение будет сообщать о неправильно построенном запросе.

 ![image](https://user-images.githubusercontent.com/91749695/149949558-def6a41b-675c-460a-a8d6-ef7d9a718226.png)

Таким образом получим, правильный поиск.

 ![image](https://user-images.githubusercontent.com/91749695/149949585-1b866cca-6808-4925-b764-36f24f488e90.png)

И невозможность добавления sql инъекции.

 ![image](https://user-images.githubusercontent.com/91749695/149949620-be9246e5-99bc-4220-9ca0-bbb7f6a512b1.png)




