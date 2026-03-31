# 🐷 Smart Piggy API (Java Edition)

Концепт легковесного REST API на **Spring Boot** для управления личными накоплениями. Система отслеживает прогресс достижения финансовой цели и уведомляет пользователя через Telegram при её достижении.

---

## 📋 API Контракт (Endpoints)

| Метод    | Эндпоинт        | Описание                        | Тело запроса (JSON)                                     |
| :------- | :-------------- | :------------------------------ | :------------------------------------------------------ |
| `GET`    | `/api/goal`     | Текущий статус и прогресс       | —                                                       |
| `PUT`    | `/api/goal`     | Установить/изменить цель        | `{"title": "BMW M3 Competition G80", "targetAmount": 5000000}`   |
| `POST`   | `/api/income`   | Внести деньги в копилку         | `{"amount": 15000.50}`                                  |
| `DELETE` | `/api/reset`    | Сбросить прогресс (разбить)     | —                                                       |

---

## 🤖 Логика уведомлений
Проект реализует автоматическую проверку условий при каждом `POST` запросе:
1.  При пополнении баланса API высчитывает остаток до цели.
2.  Если условие `currentAmount >= targetAmount` выполняется, инициируется вызов метода `telegramService.sendWinMessage()`.
3.  Пользователь получает сообщение: *"Поздравляю! Цель [Название] достигнута! 🚗"*

---

## 🚀 Как запустить (Development)

1.  **Клонировать репозиторий:**
    ```bash
    git clone [https://github.com/your-username/smart-piggy-api.git](https://github.com/your-username/smart-piggy-api.git)
    ```
2.  **Собрать проект (Maven):**
    ```bash
    ./mvnw clean install
    ```
3.  **Запустить приложение:**
    ```bash
    ./mvnw spring-boot:run
    ```

API будет доступно по адресу: `http://localhost:8080`

---

## 🧪 Примеры запросов (cURL)

**Пополнить копилку:**
```bash
curl -X POST http://localhost:8080/api/income \
     -H "Content-Type: application/json" \
     -d '{"amount": 500}'
