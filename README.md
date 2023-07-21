## A project to demonstrate webhook bots in the Compass app
This project is an example of Demobot to learn how webhook bots work in Compass messenger.

## Adding a bot token to the project
To configure bot accesses, you need to get an authorization token inside the app.<br>
The bot token is issued when the bot is created, after which the token becomes available in the bot card.<br>
After creating a bot, you need to add token to the project config on the path `config/const.template.php`.
```php
// adding the previously received bot authorization token
define("DEMOBOT_USERBOT_TOKEN", "00000000-0000-0000-0000-0000000000000");
```

## Deploying the bot
### Manual method

- `config/const.template.php` - example of a bot config;
- `cli/init_bot.php` - script for initializing the bot.

The Demobot project must be added to your server, and then do the following:
- export the value for the token variable:<br>
  `export DEMOBOT_USERBOT_TOKEN=your-token-here`
- replace the config `config/const.template.php` to another config file as `config/const.php`:<br>
  `envsubst < config/const.template.php > config/const.php;`
- run the script located on the path: `cli/init_bot.php`. This script will completely update the list of commands of your bot in the Compass app, adding commands to demonstrate the work of Demobot;
- configure the web server so that requests are redirected to the entrypoint of the project, accessible on the path: `entrypoint/demobot/index.php`.

### Using Docker

For your convenience, docker-compose have been added to the project so that it is possible to deploy the bot using containers.<br>
To work with containers, you must have Docker installed on the web server.

The Demobot project must be added to your server, and then do the following:
- export the value for the token variable:<br>
  `export DEMOBOT_USERBOT_TOKEN=your-token-here`
- run the command to launch containers:<br>
  `docker-compose up -d --build`
- configure the web server so that requests are redirected to the nginx container.

### Demobot performance check
To make sure that Demobot is installed correctly on your server, do the following:

- check that the bot has updated list of commands in the Compass app. Example of test commands:
    - `/message to chat`
    - `/message to thread`
    - `/add reaction`
- send a command from the chat with the bot to make sure that the request is sent to the webhook you specified.<br>
  Example of a webhook for Demobot: `https://your-domain.com/entrypoint/demobot/index.php`
- after sending the command, check that the response from Demobot has returned to the chat with the bot - this is part of the demo work of Demobot.

Learn more about how bots work by clicking on this link:<br>
[The bots' Userbot API](https://github.com/getCompass/userbot).
