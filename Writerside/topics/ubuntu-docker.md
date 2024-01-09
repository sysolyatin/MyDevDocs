# Установка Docker в Ubuntu

```bash
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce
sudo systemctl status docker
```

Для установки docker-compose необходимо узнать версию последнего релиза в 
[репозитории](https://github.com/docker/compose/releases) и подставить её в ссылку

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

Затем полученный файл необходимо сделать исполняемым и проверить, что всё хорошо

```bash
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```