# Kittygram

## Описание проекта
Kittygram — это социальная сеть для любителей котиков. Здесь вы можете публиковать фотографии своих питомцев, указывать их достижения и любоваться котиками других пользователей.

Проект переведен на микросервисную архитектуру и полностью контейнеризирован для обеспечения надежности и простоты развертывания.

## Стек технологий
*   **Backend:** Python 3.10, Django, Django REST Framework, Gunicorn.
*   **Frontend:** React, HTML5, Vanilla CSS.
*   **Database:** PostgreSQL 13.
*   **Web Server / Gateway:** Nginx.
*   **Infrastructure:** Docker, Docker Compose.
*   **CI/CD:** GitHub Actions, Ruff (Linting), Pytest.
*   **Notifications:** Telegram Bot API.

## Как запустить проект локально

### 1. Клонируйте репозиторий:
```bash
git clone https://github.com/ваш_логин/kittygram_final.git
```

### 2. Подготовьте файл .env:
Создайте файл `.env` в корневой папке и заполните его по примеру:
```env
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
POSTGRES_DB=kittygram
DB_HOST=db
DB_PORT=5432

SECRET_KEY=ваш_секретный_ключ_django
DEBUG=False
ALLOWED_HOSTS=127.0.0.1 localhost
```

### 3. Запустите проект через Docker Compose:
```bash
docker compose up -d --build
```

### 4. Выполните миграции и соберите статику:
```bash
docker compose exec backend python manage.py migrate
docker compose exec backend python manage.py collectstatic
docker compose exec backend cp -r /app/static/. /static/
```

Проект будет доступен по адресу: http://localhost:9000

## Автоматизация (CI/CD)
При каждом пуше в ветку `main` запускается GitHub Workflow:
1.  **Линтинг:** Проверка кода с помощью Ruff.
2.  **Тестирование:** Проверка бэкенда и фронтенда.
3.  **Сборка:** Обновление образов на Docker Hub.
4.  **Уведомление:** Отчет об успехе в Telegram.
