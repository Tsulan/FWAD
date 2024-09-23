# Лабораторная работа №1. Основы HTTP

## Цель
Целью данной лабораторной работы является изучение основных принципов протокола HTTP.

Описание работы: [01_http_basics](https://github.com/MSU-Courses/frameworks-for-web-development/blob/main/ru/lab/01_http_basics/readme.md)

## Выполнение работы

### Задание №1. Анализ HTTP-запросов

1. Зайдите на сайт [http://sandbox.usm.md/login](http://sandbox.usm.md/login).
2. Откройте вкладку `Network` в инструментах разработчика браузера.
3. Введите неверные данные для входа (например, `username: student`, `password: studentpass`).
4. Проанализируйте запросы, которые были отправлены на сервер.
5. Ответьте на следующие вопросы:
   - Какой метод HTTP был использован для отправки запроса?
   - Какие заголовки были отправлены в запросе?
   - Какие параметры были отправлены в запросе?
   - Какой код состояния был возвращен сервером?
   - Какие заголовки были отправлены в ответе?
6. Повторите шаги 3-5, введя верные данные для входа (`username: admin`, `password: password`).

#### Неверные данные

При введении неверных данных (`username: student`, `password: studentpass`) и нажатии на копку `Login`, был отправлен следующий запрос:
```http
POST /login/process.php HTTP/1.1
Host: sandbox.usm.md
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 37
```

Тот же запрос в формате cURL:
```cmd
curl "http://sandbox.usm.md/login/process.php" ^
  -H "Accept: */*" ^
  -H "Accept-Language: en-US,en;q=0.9,ru;q=0.8,ru-RU;q=0.7,ro;q=0.6" ^
  -H "Cache-Control: no-cache" ^
  -H "Connection: keep-alive" ^
  -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" ^
  -H "Origin: http://sandbox.usm.md" ^
  -H "Pragma: no-cache" ^
  -H "Referer: http://sandbox.usm.md/login/" ^
  -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36" ^
  -H "X-Requested-With: XMLHttpRequest" ^
  --data-raw "username=student&password=studentpass" ^
  --compressed ^
  --insecure
 ``` 

- Какой метод HTTP был использован для отправки запроса?
**POST**
- Какие заголовки были отправлены в запросе? 
**Accept, Accept-Encoding, Accept-Language, Cache-Control, Connection, Content-Length, Content-Type, Host, Origin, Pragma, Referer, User-Agent, X-Requested-With, XMLHttpRequest**
![request headers for invalid request](./.images/image.png)
- Какие параметры были отправлены в запросе?
**Был отправлен Path параметр к файлу `process.php`**
- Какой код состояния был возвращен сервером?
**`401 Unauthorized`**
- Какие заголовки были отправлены в ответе?
**Connection, Content-Type, Date, Server, Transfer-Encoding**
![response invalid](./.images/image01.png)

Статус аутентификации показал ошибку:
![error login](./.images/image05.png)

#### Верные данные

При введении верных данных (`username: admin`, `password: password`) и нажатии на копку `Login`, был отправлен следующий запрос:
```http
POST /login/process.php HTTP/1.1
Host: sandbox.usm.md
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36
Connection: keep-alive
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 32
```

*По сути, отправился тот же HTTP запрос, что и в случае с неверными данными. Отличие только в отсылаемых данных*

Тот же запрос в формате cURL:
```cmd
curl "http://sandbox.usm.md/login/process.php" ^
  -H "Accept: */*" ^
  -H "Accept-Language: en-US,en;q=0.9,ru;q=0.8,ru-RU;q=0.7,ro;q=0.6" ^
  -H "Cache-Control: no-cache" ^
  -H "Connection: keep-alive" ^
  -H "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" ^
  -H "Origin: http://sandbox.usm.md" ^
  -H "Pragma: no-cache" ^
  -H "Referer: http://sandbox.usm.md/login/" ^
  -H "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36" ^
  -H "X-Requested-With: XMLHttpRequest" ^
  --data-raw "username=admin&password=password" ^
  --compressed ^
  --insecure
 ``` 

- Какой метод HTTP был использован для отправки запроса?
**POST**
- Какие заголовки были отправлены в запросе? 
**Accept, Accept-Encoding, Accept-Language, Cache-Control, Connection, Content-Length, Content-Type, Host, Origin, Pragma, Referer, User-Agent, X-Requested-With, XMLHttpRequest**
![request headers for valid request](./.images/image02.png)
- Какие параметры были отправлены в запросе?
**Был отправлен Path параметр к файлу `process.php`**
- Какой код состояния был возвращен сервером?
**`200 OK`**
- Какие заголовки были отправлены в ответе?
**Connection, Content-Type, Date, Server, Transfer-Encoding**
![response valid request](./.images/image03.png)

Статус аутентификации показал успех:
![success login](./.images/image04.png)

### Задание №2. Составление HTTP-запросов

1. Составьте `GET`-запрос к серверу по адресу `http://sandbox.com`, указав в заголовке `User-Agent` ваше имя и фамилию.

   ```http
   GET / HTTP/1.1
   Host: sandbox.com
   User-Agent: Tulan Vladislav
   ```

2. Составьте `POST`-запрос к серверу по адресу `http://sandbox.com/cars`, указав в теле запроса следующие параметры:
   - `make: Toyota`
   - `model: Corolla`
   - `year: 2020`

   ```http
   POST /cars HTTP/1.1
   Host: sandbox.com
   Connection: keep-alive
   Content-Type: application/json

   {
     "make": "Toyota",
     "model": "Corolla",
     "year": 2020
   }
   ```

3. Составьте `PUT`-запрос к серверу по адресу `http://sandbox.com/cars/1`, указав в заголовке `User-Agent` ваше имя и фамилию, в заголовке `Content-Type` значение `application/json` и в теле запроса следующие параметры:
   ```json
   {
     "make": "Toyota",
     "model": "Corolla",
     "year": 2021
   }
   ```
   ```http
   PUT /cars/1 HTTP/1.1
   Host: sandbox.com
   User-Agent: Tulan Vladislav
   Connection: keep-alive
   Content-Type: application/json

   {
     "make": "Toyota",
     "model": "Corolla",
     "year": 2021
   }
   ```

4. Напишите один из возможных вариантов ответа сервера следующий запрос.
   ```http
   POST /cars HTTP/1.1
   Host: sandbox.com
   Content-Type: application/json
   User-Agent: John Doe
   model=Corolla&make=Toyota&year=2020
   ```
   Предположите ситуации, когда сервер может вернуть HTTP-коды состояния 200, 201, 400, 401, 403, 404, 500.

- `404`: Первым делом сервер может не иметь такого ендпоинта, как /cars, поэтому вернет соответсвующий код с текстом Not Found
- `400`: Bad request может прийти в случае если сервер валидирует входящий заголовок `User-Agent` и увидев там `John Doe`, вернет сообщение о неверном параметре.
- `401`: Сервер потребует дополнительный заголовок `authorization` с правильными данными, чтобы запрос был успешен.
- `403`: Доступ мог быть запрещен по IP, с которого отсылается request. Или же запрещен доступ для `John Doe`
- `500`: Что-то сломалось на стороне сервера, вылетела неожидаемая ошибка итп. Например, сервер не хорошо обрабатывал заголовок `User-Agent` и при получении значения `John Doe` возникло исключение, которое спровоцировало ошибку.
- `200`: Сервер ожидал указанные параметры и успешно их обработал. Мог быть создан новый объект автомобиля с указанными параметрами.
- `201`: Сервер также успешно обработал запрос и создал автомобиль, выдал в ответе сообщение `Created`

   При попытке отослать такой запрос:
   ```http
   curl -L -X POST "http://sandbox.com/cars" ^
     -H "Content-Type: application/json ^
     -H "User-Agent: John Doe" ^
     --data '{"model":"Corolla","make":"Toyota", "year": 2020}'
   ```

   Был получен следующий ответ:
   ![sandbox cars POST response](./.images/image06.png)

   ### Задание №3. Дополнительное задание. HTTP_Quest

1. Отправьте `POST`-запрос на сервер по адресу `http://sandbox.usm.md/quest`, указав в заголовке User-Agent вашу фамилию и имя (Например `User-Agent: John Doe`).

   ```bash
   curl -X POST http://sandbox.usm.md/quest -H  "User-Agent: Tulan Vladislav"
   ```

   **Результат:**
   ![quest step 1](./.images/image07.png)
591783
2. Отправка запроса с логином имея полученные данные. (Получены `id: 430129`, `token: HRQBNQZFFAkSECASATUe`)

   ```bash
   curl -X POST http://sandbox.usm.md/quest/login -H  "User-Agent: Tulan Vladislav"
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   ```

   **Результат:**
   ![quest step 2](./.images/image08.png)

   *Тут я не убрал заголовок `User-Agent` и заметил, что сервер обработал его повторно и выдал мне новый id и тотже токен, после чего он начал проверять следющий заголовок, который нужен был уже для 2-го шага. Полагаю, если бы я случайно не оставил первый заголовок и отправил только с `Authorization`, то такого интересного поведения сервера и не заметил бы :)*

3. Отправка запроса с возрастом. 

   Был составлен и отправлен следующий запрос:
   ```bash
   curl -X PUT http://sandbox.usm.md/quest/age 
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   -H "Content-Type: application/json"
   -d '{"age": 22}'
   ```

   **Результат:**
   ![quest step 3 failed attempt](./.images/image09.png)

   *Хм, неужели сервер хочет принять возраст как значение типа String, а не целочисленное*

   Новый запрос:
   ```bash
   curl -X PUT http://sandbox.usm.md/quest/age 
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   -H "Content-Type: application/json"
   -d '{"age": "22"}'
   ```

   И снова неудача
   ![quest step 3 failed attempt 2](./.images/image10.png)

   Немного stackoverflow:
   ![stackoverflow suggestion](./.images/image11.png)
   
   Пробую:
   ```bash
   curl -X PUT http://sandbox.usm.md/quest/age 
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   -d "{\"age\":\"22\"}"
   ```

   Уже лучше, почти у цели :D
   ![quest step 3 failed attempt 3](./.images/image12.png)

   Уберу кавычки у значения возраста:
   ```bash
   curl -X PUT http://sandbox.usm.md/quest/age 
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   -d "{\"age\":\22\}"
   ```

   Не помогло, получил то же сообщение

   Вернусь к заданию шага 3 и перечитаю его. Попробую задать возраст не в json, а прямо как указано в задании
   ```bash
   curl -X PUT http://sandbox.usm.md/quest/age 
   -H "Authorization: Bearer HRQBNQZFFAkSECASATUe"
   -d age=22
   ``` 

   Finally...
   ![Step 3 success mzfk!!!](./.images/image13.png)

   *Как же все таки важно внимательно читать инструкции и следовать им :)*

4. Финальный шаг с секретным словом.

   ```bash
   curl -X GET http://sandbox.usm.md/quest/secret?token=HRQBNQZFFAkSEFsACAcSXldTQVF5VlhhXVY=
   ``` 

   Та-даам:
   ![step 4 success](./.images/image14.png)

   **Секретное слово:** **`PTkDFwtpNQktBR0HCUAfYV1E`**

   хмм..что же оно значит?

   base64? 
   ![base64 secret decode](./.images/image15.png)
   нет

   Имя json файла также декодируется в что-то непонятное:
   ![alt text](./.images/image16.png)

   *Кажется я вспомнил, что на паре было сказано, что для расшифровки нужен private key...штош, не судьба узнать что скрывается за секретным словом :)*