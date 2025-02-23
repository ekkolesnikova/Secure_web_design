1-7. См. лабораторная №2.

8. На странице со списком книг найти
8.1 Reflected XSS в поиске книг.

Reflected XSS-уязвимость возникает, когда пользовательский ввод с URL-адреса или данных POST отражается на странице без сохранения, что позволяет злоумышленнику внедрить вредоносный контент.
 
![image](https://user-images.githubusercontent.com/91749695/149955377-5726252e-bac3-4c94-8616-943acf5b0bf3.png)
![image](https://user-images.githubusercontent.com/91749695/149955390-0f7774e8-b294-4223-9798-7aa30ea2d847.png)

 
Исправление уязвимости:

![image](https://user-images.githubusercontent.com/91749695/149956884-939a5b34-97f2-47e4-aff1-36d4835ff106.png)


8.2 Persisted (Stored) XSS при создании книги и отображении списка книг.

Stored XSS-уязвимость может возникнуть, если имя пользователя онлайн-доски объявлений не очищено должным образом при выводе на страницу. В этом случае злоумышленник может вставить вредоносный код при регистрации нового пользователя в форме.

 ![image](https://user-images.githubusercontent.com/91749695/149955535-f20f9599-45d4-4334-a289-938b33bd772d.png)

 
Исправление уязвимости:
let bname = req.body.bookname.replace(‘<’, ‘(’).replace(‘>’, ‘)’)

8.3 Потенциальную уязвимость через Cookie Injection

При входе на сайт генерируется сессионный Cookie файл, который позволяет авторизировать конкретного пользователя в сессии, что и может быть использовано во вред

 ![image](https://user-images.githubusercontent.com/91749695/149955978-8823d722-97ed-4ef5-9ad5-2ead8b4ff8a0.png)

8.4 Некорректное создание сессионной cookie, которое приводит к захвату сессии (Session hijacking)

Создание собственной сессионной куки для авторизации под пользователем admin

 ![image](https://user-images.githubusercontent.com/91749695/149956034-6604bd75-841f-4e8c-a7f2-64aa80708ee0.png)

Успешный доступ к списку книг от имени пользователя «admin» с помощью собственной созданной сессионной куки

![image](https://user-images.githubusercontent.com/91749695/149956630-feff6cbe-8417-469d-9737-fcc1134b5652.png)
 
Для уязвимостей Cookie установим флаг http-only, который запрещает любой доступ к куки из JavaScript, а также изменим значение, выводимое браузером в Value с помощью алгоритма хеширования Sha256:

![image](https://user-images.githubusercontent.com/91749695/149956676-aff4c5e8-2e00-47e2-8572-69ad854b5c5c.png)
![image](https://user-images.githubusercontent.com/91749695/149956782-7a1abe36-25fc-43f3-9d7d-3e3cd6d2a18d.png)


В результате санитайзинга доступ к Cookie также был невозможен.

 ![image](https://user-images.githubusercontent.com/91749695/149956721-2a69edbe-5d72-4fd0-bd3d-f8c1e06d870c.png)


