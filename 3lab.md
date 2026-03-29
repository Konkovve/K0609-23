1. Сеть
Создал сеть: "docker network create app-network". Запустил контейнеры и проверил связь: "ping db" - контейнеры видят друг друга по имени.
<img width="863" height="889" alt="image" src="https://github.com/user-attachments/assets/2ac4e25a-c6e7-42ce-a26a-51ef60dc1693" />

2. Volume
Создал volume и запустил PostgreSQL: "docker volume create pgdata". Создал таблицу, потом удалил контейнер и запустил заново.
Данные сохранились — значит volume работает.
<img width="1039" height="353" alt="image" src="https://github.com/user-attachments/assets/195ce11b-68da-406f-8991-44e6e301a10c" />

3. Docker Compose
Создал docker-compose.yml с тремя сервисами: db(postgre), backend (flask), frontend (nginx).
Запустил: "docker compose up -d --build".
Проверил: "docker compose ps". Все сервисы работают.
<img width="1280" height="126" alt="image" src="https://github.com/user-attachments/assets/7946669a-a89e-4505-aeb3-0d3996af6e46" />

4. Проверка работы
Создал данные: "docker compose exec db ...".
Проверил API: "curl localhost:8080/api/items". Ответ пришёл — значит связка frontend -> backend -> db работает.

5. Масштабирование
Увеличил количество backend: "docker compose up -d --scale backend=3".
Проверил: "docker compose ps". Появилось 3 контейнера backend.
<img width="1280" height="166" alt="image" src="https://github.com/user-attachments/assets/766f4ef1-bab2-44e2-8c7c-d889b4a5df0a" />

Проблем с лабой вроде не было, я уже забыл на момент коммита отчёта.
