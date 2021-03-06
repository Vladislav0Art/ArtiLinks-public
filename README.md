# ArtiLinks - Bookmark Manager

### Deployment: https://artilinks.vercel.app/



### Идея проекта:

Приложение решает проблему сохранения и категоризации ссылок на полезные онлайн-сервисы.




### Cтек технологий:

1. `NextJS` - SSR, подгрузка данных пользователя до рендера приложения.

2. `JSON web tokens` - регистрация/аутентификация пользователя.

3. `Nodemailer` - подтверждение пользователем зарегистрированного email; восстановление пароля с помощью.

4. `MongoDB/Mongoose` - хранение данных пользователей, взаимодействие с данными.

5. `Axios` - создание API запросов.

6. `Open graph data scraping` - подтягивание информации с ресурсов, на которые указывает сохраняемая пользователем ссылка.

7. `React Transition Group` - создание анимаций при рендере компонентов.



### Функционал приложения:

1. Регистрация и авторизация пользователя в приложении.

2. Восстановление пароля от аккаунта пользователя.

3. Категоризация ссылок в приложении сделана с помощью структуры групп и коллекций: группа - контейнер, которых хранит в себе коллекции, коллекция - контейнер, хранящий в себе ссылки.

4. `CRUD` для групп, коллекций и ссылок.

5. Поиск ссылок внутри по названию ресурса внутри рассматриваемой коллекции.



### Увлекательная задача в проекте и возникшие сложности:

Наиболее трудоемкая и интересная часть была разработка JWT аутентификации/регистрации. Данный подход был для меня новым, поэтому мне пришлось уделить много времени на поиск информации о том, как нужно правильно писать такой функционал. В итоге я реализовал отдельный класс-сервис по работе с refresh/access-токенами. Основной проблемой было обновление access-токена в случае, когда пользователь отправил запрос на защищенный API путь, будучи аутентифицированным, но имея уже инвалидированный access-токен. Я узнал, что библиотека Axios поддерживает функционал интерсепторов, которые как раз могли решить мою проблему. При инвалидированном access-токене мой сервер возвращает ошибку авторизации 401, в интерсепторе ответа с сервера я отлавливаю данный тип ошибки, отправляю запрос на обновление токенов, а после пытаюсь повторить исходный запрос.
