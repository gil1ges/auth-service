# 🔐 Auth Service

Микросервис аутентификации с двухфакторной аутентификацией, JWT токенами и отправкой email через Resend.

## 🚀 Быстрый старт

### 1. Клонирование и настройка
```bash
git clone <https://github.com/Dmitriy4565/auth-service>
cd auth-service
cp .env.example .env
```
### 2. Настройка переменных окружения (.env)
```bash
# База данных
DB_HOST=localhost
DB_PORT=5432
DB_USER=postgres
DB_PASSWORD=password
DB_NAME=auth_service

# Сервер
PORT=8080
GIN_MODE=debug

# JWT 
JWT_SECRET=

# CORS
CORS_ALLOW_ORIGINS=http://localhost:3000,http://localhost:5173
CORS_ALLOW_CREDENTIALS=true

# Токены
ACCESS_TOKEN_EXPIRE_MINUTES=15
REFRESH_TOKEN_EXPIRE_DAYS=7

# Resend Email Service
RESEND_API_KEY=re_your_api_key_here
RESEND_FROM_EMAIL=noreply@yourdomain.com
RESEND_FROM_NAME=Auth Service

# Клиент
CLIENT_URL=http://localhost:3000
```
### 3. Запуск в Docker
```bash
docker compose up -d --build
```
### 4. Проверка работы
```bash
curl http://localhost:8080/health
```
### 📧 Настройка Resend

### 🔴 ВАЖНО: Требования для Resend
Resend требует верифицированный домен для отправки писем в продакшене!

### Шаги настройки:
Получите API ключ на resend.com

Добавьте и верифицируйте домен в Resend Dashboard

Используйте email с верифицированного домена:

```bash
env
RESEND_FROM_EMAIL=noreply@yourcompany.com
Тестовый режим
В тестовом режиме Resend позволяет отправлять письма только на email вашего аккаунта.
```
Тестовый режим
В тестовом режиме Resend позволяет отправлять письма только на email вашего аккаунта.

### 🛠️ API Endpoints

### Аутентификация

* POST /auth/register - Регистрация пользователя + отправка 2FA кода

* POST /auth/login - Вход с проверкой 2FA

* POST /auth/verify-email - Подтверждение 2FA кода

* POST /auth/refresh - Обновление JWT токена

* POST /auth/logout - Выход

### Сброс пароля

* POST /auth/request-reset-password - Запрос сброса пароля (отправка email)

* POST /auth/reset-password - Сброс пароля по токену

### Защищенные endpoints
* GET /auth/profile - Профиль пользователя (требует JWT)

### 🐳 Docker развертывание

Контейнеры

* auth-service-auth-service-1 - Go приложение (порт 8080)

* auth-service-postgres-1 - PostgreSQL (порт 5432)

### Утилиты управления
```bash
# Деплой на сервер
python deploy.py

# Перезапуск сервиса
python update_serv.py

# Очистка БД (осторожно!)
python snos_bd.py

# Подключение к серверу
python connect.py
```

### 🔐 Функциональность
✅ Регистрация с верификацией по email

✅ Двухфакторная аутентификация (2FA)

✅ JWT + Refresh токены

✅ Сброс пароля через email

✅ CORS настройка

✅ Docker контейнеризация

✅ Отправка email через Resend API

### 🚨 Ошибки
Письма не отправляются

* Проверьте RESEND_API_KEY

* Убедитесь что домен верифицирован в Resend

* В тестовом режиме используйте email вашего аккаунта Resend

### Сборка
```bash
go build -o auth-service cmd/server/main.go
```
### 📄 Лицензия
MIT License

Production URL: http://77.110.105.228:8080 
Database: 77.110.105.228:5432 
Resend Domain: noreply@rossttelecom.ru 
