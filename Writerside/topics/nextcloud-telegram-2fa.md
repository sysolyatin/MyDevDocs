# 2FA через Telegram

В панели управления необходимо установить соответствующее приложение, а затем необходимо привязать 
заранее созданного бота к инстансу некстклауда.

```Bash
sudo docker exec -u 33 -ti nextcloud-23 /bin/bash

# далее внутри контейнера
./occ twofactorauth:gateway:configure telegram
Please enter your Telegram bot token: 123456789:AAbbCCddEEffGGhhIIjjKKllMMnnOOppQQ
Using 123456789:AAbbCCddEEffGGhhIIjjKKllMMnnOOppQQ.
```

Далее необходимо включить второй фактор в настройках пользователя

![telegram-nextcloud-2fa.png](telegram-nextcloud-2fa.png)

И в глобальных настройках безопасности запретить вход без второго фактора.