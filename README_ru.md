## Проект для демонстрации работы webhook ботов приложения Compass
Данный проект представляет собой пример Demobot для возможности ознакомиться с работой webhook ботов в мессенджере
Compass.

## Добавление в проект токена бота
Для настройки доступов бота необходимо получить токен авторизации внутри приложения.<br>
Токен бота выдается при создании бота, после чего токен становится доступен в карточке бота.<br>
После создания бота необходимо добавить токен в конфиг проекта по пути `config/const.template.php`.
```php
// добавляем ранее полученный токен авторизации бота
define("DEMOBOT_USERBOT_TOKEN", "00000000-0000-0000-0000-0000000000000");
```

## Разворачивание бота
### Ручной способ

- `config/const.template.php` - пример конфига бота;
- `cli/init_bot.php` - скрипт для инициализации бота.

Проект Demobot необходимо добавить на ваш сервер, после чего выполнить следующее:
- экспортировать значение для переменной токена:<br>
  `export DEMOBOT_USERBOT_TOKEN=токен-вашего-бота`
- выполнить замену конфига `config/const.template.php` в другой файл-конфиг как `config/const.php`:<br>
  `envsubst < config/const.template.php > config/const.php;`
- запустить скрипт, расположенный по пути: `cli/init_bot.php`. Данный скрипт полностью обновит список команд вашего бота в приложении Compass, добавив команды для демонстрации работы Demobot;
- настроить веб-сервер таким образом, чтобы запросы перенаправлялись на entrypoint проекта, доступный по пути: `entrypoint/demobot/index.php`.

### C помощью Docker 

Для вашего удобства в проект были добавлены docker-compose, чтобы была возможность развернуть бота с помощью контейнеров.<br>
Для работы с контейнерами необходимо иметь на веб-сервере установленный Docker.

Проект Demobot необходимо добавить на ваш сервер, после чего выполнить следующее:
- экспортировать значение для переменной токена:<br>
  `export DEMOBOT_USERBOT_TOKEN=токен-вашего-бота`
- выполнить команду для запуска контейнеров:<br>
  `docker-compose up -d --build`
- настроить веб-сервер таким образом, чтобы запросы перенаправлялись в контейнер nginx.

### Проверка работоспособности Demobot
Чтобы убедиться в том, что Demobot установлен верно на вашем сервере, сделайте следующее:

- в приложении Compass проверьте, что у бота обновился список команд. Пример тестовых команд:
    - `/message to chat`
    - `/message to thread`
    - `/add reaction`
- отправьте команду из чата с ботом, чтобы убедиться, что запрос отправляется на указанный вами webhook.<br>
  Пример webhook для Demobot: `https://your-domain.com/entrypoint/demobot/index.php`
- после отправки команды проверьте, что в чат с ботом вернулся ответ от Demobot - это часть демонстрационной работы Demobot.

Подробнее о работе ботов можно узнать, перейдя по ссылке:<br>
[Userbot API ботов](https://github.com/getCompass/userbot/blob/master/README_ru.md).
