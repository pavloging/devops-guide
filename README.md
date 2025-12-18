# DevOps Guide

# Шаг 1. Создаем VPS и подключаемся к серверу по ssh

Выберите любой VPS сервис который вам нравится. p.s. Лично я использую Beget

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


# Шаг 3. Запускаем docker-compose
1. Клонируем нужный репозиторий и заходим в него. Например: Клонируем - https://github.com/pavloging/devops-guide и заходим - cd devops-guide
2. Далее создаем docker-compose.yml и в каждом сервисе создаем Dockerfile и .dockerignore так же настраиваем их.
3. Запускаем
```bash
docker-compose up -d
```

4. Проверяем
После запуска должно появиться сообщение об успешном старте ваших сервисов. Рекомендуется проверить логи каждого контейнера для проверки их работоспособности.
```bash
docker ps
```

Копируем CONTAINER ID и вставляем
```bash
docker logs ВАШ_ID
```

5. Ошибка?
Если у вас возникает ошибка, то попробуйте повторить алгоритм заного, заранее удалить созданные образы руководстом ниже - Удачи!

# Удалить/очистить все данные Докера (контейнеры, образы, тома и сети)

## Одной строкой

Linux
```bash
docker stop $(docker ps -qa) && docker rm $(docker ps -qa) && docker rmi -f $(docker images -qa) && docker volume rm $(docker volume ls -q) && docker network rm $(docker network ls -q)
```

Win
```bash
docker stop $(docker ps -q -a); docker rm $(docker ps -q -a); docker rmi -f $(docker images -q -a); docker volume rm $(docker volume ls -q); docker network rm $(docker network ls -q)
```
