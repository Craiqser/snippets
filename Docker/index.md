# **[Snippets](../README.md) - Docker**

[docker.com](https://www.docker.com/)
[docs](https://docs.docker.com/)

## Основные команды

Посмотреть список команд, посмотреть версию:
```bash
docker
docker version
```

Посмотреть список текущих образов докера:
```bash
docker images
```

Скачать nodejs-образ последней версии (hub.docker.com):
```bash
docker pull node
```

Создание образа на основе команд в Dockerfile,
создание образа с именем:
```bash
docker build .
docker build -t nodeapp:latest .
```

Информация по образу:
```bash
docker image inspect imageId
```

Переименование образа:
```bash
docker tag oldName newName
```

Запуск образа, т.е. создание нового контейнера (вместо названия можно указать id образа),
запуск образа в интерактивном режиме (для взаимодействия),
запуск с пробросом порта докера к локальному порту,
запуск в фоном режиме (-d - detach),
запуск с заданием пользовательского имени для контейнера:
```bash
docker run node
docker run -it node
docker run -p 80:3000 imageId
docker run -d -p 80:3000 imageId
docker run -d -p 80:3000 --name coolname imageId
```
Дополнительно через ключ --rm можно задать автоудаление контейнера после его остановки.

Запуск контейнера (вместо названия можно указать id контейнера):
```bash
docker start node
```

Остановка контейнера (вместо названия можно указать id контейнера):
```bash
docker stop containerId
```

Посмотреть список всех контейнеров, запущенных контейнеров:
```bash
docker ps -a
docker ps
```

Присоединить текущие каналы ввода/вывода/ошибок к запущенному контейнеру:
```bash
docker attach containerId
```

Посмотреть вывод контейнера:
```bash
docker logs containerId
```

Удаление контейнера, удаление всех остановленных контейнеров:
```bash
docker rm containerId
docker container prune
```

Удаление образа:
```bash
docker rmi imageId
```

## Работа с Dockerfile

```Dockerfile
FROM node # Исходный образ
WORKDIR /app # Рабочая директория проекта
COPY package.json /app
RUN npm install # Команда, запускаемая при инсталляции образа
COPY . . # Копируем файлы из локального проекта (точка - текущая папка, для src - это каталог с Dockerfile, для dst - это каталог WORKDIR)
EXPOSE 3000 # Указываем используемый порт
VOLUME ["./app/data"] # Монтируем папку
CMD ["node", "app.js"] # Команда, запускаемая при запуске образа на выполнение
```

## .dockerignore

```bash
.git/
node_modules/

Dockerfile
```

## Docker Hub

Переименовываем образ, отпрвляем в свой хаб:
```bash
docker tag imageName craiqser/imageName
docker push craiqser/imageName
```

## ENV-переменные

Пример установки переменной в Dockerfile:
```Dockerfile
ENV PORT 3000
EXPOSE $PORT
```

Пример установки переменной из консоли:
```bash
docker run -e PORT=80 imageName
```

Пример установки переменной из env-файла:
```bash
local.env file:
PORT=3000


docker run --env-file ./local.env imageName
```

## Volumes

Создание именованного тома с именем appdata и относительным путём ./app/data:
```bash
docker run ... -v appdata:./app/data
```

Просмотр, инспектирование:
```bash
docker volume ls
docker volume inspect aappdata
```
