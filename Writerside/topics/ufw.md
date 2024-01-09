# UFW

Настройка политик по умолчанию

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

Настройка SSH

```bash
sudo ufw allow proto tcp from 10.10.10.10 to any port 22 comment sysolyatin
```

Активация ufw

```bash
sudo ufw enable
```

Удаление правил

```bash
sudo ufw status numbered
sudo ufw delete <номер>
```

Отключение и сброс

```bash
sudo ufw disable
sudo ufw reset
```