# FastAPI + Nginx Infrastructure

Реализация backend-приложения и reverse-proxy в изолированной Docker-сети.

## Технологии
- **Backend:** Python 3.11 (Alpine), FastAPI, Uvicorn.
- **Proxy:** Nginx 1.27 (Alpine).
- **Orchestration:** Docker Compose

## Архитектура
Проект использует схему **Reverse Proxy**:
- **Nginx** (порт 80) принимает внешние запросы и перенаправляет их на внутренний сервис.
- **Backend** (порт 8000) скрыт внутри приватной сети Docker и недоступен извне.
- **Healthcheck** гарантирует, что Nginx начнет работу только после полной готовности FastAPI.

**Схема взаимодействия:**

```text
[ Пользователь ] 
      │
      ▼
[ Хост (порт 80) ]
      │
      ▼
[ Контейнер NGINX ] ─── (Внутренняя сеть Docker) ───► [ Контейнер Backend (порт 8000) ]
```
## Запуск и проверка работоспособности
- **Запуск**
```bash
docker compose up --build -d
```
- **Проверка**
```bash
curl http://localhost/
```
