[![Main Kittygram workflow](https://github.com/stremousoff/kittygram_final/actions/workflows/main.yml/badge.svg)](https://github.com/stremousoff/kittygram_final/actions/workflows/main.yml)
	![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) ![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white) ![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray) ![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white) ![Nginx](https://img.shields.io/badge/nginx-%23009639.svg?style=for-the-badge&logo=nginx&logoColor=white) 	![Gunicorn](https://img.shields.io/badge/gunicorn-%298729.svg?style=for-the-badge&logo=gunicorn&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
# KittyGram - Учебный проект от ЯндексПрактикума
## Описание
Сайт для публикаций своих любимых кошечек.

---
### Установка проекта на локальный компьютер из репозитория

#### Клонирование проекта
- Клонировать репозиторий: `git clone <адрес вашего репозитория>`
- Перейти в директорию с клонированным репозиторием.
- В корневой директории проекта создать файл `.env` и заполнить его переменными по примеру из файла `.env.example`.

#### Настройка Nginx
- Установить Nginx: `sudo apt install nginx -y`
- Запустить Nginx: `sudo systemctl start nginx`
- Установить ограничения на открытые порты: `sudo ufw allow 'Nginx Full' && sudo ufw allow OpenSSH`
- Включить файервол: `sudo ufw enable`
- Открыть конфигурационный файл Nginx по адресу `/etc/nginx/sites-enabled/default` и редактировать его:
```nginx
server {
    server_name IP_адрес_сервера домен_сервера;
    server_tokens off;
    
    location / {
        proxy_pass http://127.0.0.1:9000;
    }
}
```
- Сохранить изменения, выйти из редактора и проверить корректность настроек: `sudo nginx -t`
- Перезапустить Nginx для применения изменений: `sudo systemctl reload nginx`

#### Получение и настройка SSL-сертификата
- Находясь на сервере, последовательно выполните команды в терминале: 
```bash
sudo apt install snapd 
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```
- Проверить что сертифика появился в настройках Nginx `/etc/nginx/sites-enabled/default`
- Перезагрузить конфигурацию `Nginx sudo systemctl reload nginx`

#### Настройка и установка Docker:
- Находясь на сервере, последовательно выполните команды в терминале установки Docker Compose:
```bash
sudo apt update
sudo apt install curl
curl -fSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh
sudo apt-get install docker-compose-plugin
```
- Далее, выполните следующие команды для запуска проекта на локальной машине:
```bash
sudo docker compose -f docker-compose.production.yml pull
sudo docker compose -f docker-compose.production.yml down
sudo docker compose -f docker-compose.production.yml up -d
sudo docker compose -f docker-compose.production.yml exec backend python manage.py migrate
sudo docker compose -f docker-compose.production.yml exec backend python manage.py collectstatic
sudo docker compose -f docker-compose.production.yml exec backend cp -r /app/collect_static/. /static_backend/static/
```
### Как посмотреть проект:
Проект будет доступен по адресу: `http://localhost:9000/`

---
автор проекта: [Антон Стремоусов](https://github.com/stremousoff)

