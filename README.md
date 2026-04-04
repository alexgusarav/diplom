# DIPLOM MyCloud

## инструкция по развертыванию на Linux Ubuntu 24.04 LTS

**1. Копируем проект**
git clone https://github.com/alexgusarav/diplom.git

**2. Переходим в директорию проекта**
cd diplom

**3. Вносим изменения в секции ALLOWED_HOSTS, CSRF_TRUSTED_ORIGINS, CORS_ALLOWED_ORIGINS файла settings.py (указываем ip адрес сервера)**
nano backend/backend/settings.py

**4. Вносим изменения в секцию const HOST_URL файла requests.js (указываем ip адрес сервера)**
nano frontend/src/apiService/requests.js

**5. Вносим изменения в секцию server_name файла nginx.conf (указываем ip адрес сервера)**
nano frontend/nginx.conf

**6. Создать файл .env с настройками ключей**
nano .env
```
#setting DB
DB_PASSWORD=

#setting Django
SECRET_KEY=

#setting Redux
VITE_KEY_REDUX=
```

**6. Перед началом установки новых приложений обновите списки пакетов в системе:**
apt-get update

**7.Затем установите необходимые для дальнейшей работы зависимости:**
apt-get install ca-certificates curl gnupg

**8. устанавливите GPG-ключ, который будет использоваться пакетным менеджером apt для проверки подлинности пакетов из репозитория Docker**
install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
chmod a+r /etc/apt/keyrings/docker.gpg

**9.добавьте в систему APT-репозиторий Docker**
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null

**10.обновите список пакетов через загрузку index-файлов с каждого подключённого репозитория**
apt-get update

**11. установите Docker**
apt-get install docker.io docker-compose docker-compose-plugin docker-buildx-plugin -y

**12. Запускаем контейнеры db, backend, frontend**
docker compose up -d

**13. применяем миграции в БД**
docker compose exec backend python manage.py migrate