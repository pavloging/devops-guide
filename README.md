# DevOps Guide

# Шаг 1. Создаем VPS и подключаемся к серверу по ssh

# Шаг 2. Устанавливаем docker и docker-compose

### Установка docker:

1. Обновление системы
```bash
sudo apt update
```

2. Установливаем несколько необходимых пакетов, которые позволят aptиспользовать пакеты через HTTPS
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

3. Добавляем в свою систему ключ GPG
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

4. Добавляем репозиторий Docker в источники APT
```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```

5. Проверка
```bash
apt-cache policy docker-ce
```
Вы увидите такой вывод, хотя номер версии Docker может быть другим

docker-ce:
  Installed: (none)
  Candidate: 5:19.03.9~3-0~ubuntu-focal
  Version table:
     5:19.03.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages

6. Установка
```bash
sudo apt install docker-ce
```

# Устанавливаем Docker-Compose

1.
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

2. 
```bash
sudo chmod +x /usr/local/bin/docker-compose
```

3. 
```bash
docker-compose --version
```

Вывод будет выглядеть следующим образом:

Output
docker-compose version 1.26.0, build 8a1c60f6


# Удалить/очистить все данные Докера (контейнеры, образы, тома и сети)

## Одной строкой

```bash
docker stop $(docker ps -qa) && docker rm $(docker ps -qa) && docker rmi -f $(docker images -qa) && docker volume rm $(docker volume ls -q) && docker network rm $(docker network ls -q)
```
