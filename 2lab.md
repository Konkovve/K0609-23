https://hub.docker.com/r/konkovvv/flask-demo

1. Первый Dockerfile
Создал простое приложение и Dockerfile, потом собрал образ: "docker build -t myapp:bad ."
Он получился очень большим (около 1 ГБ), потому что использовался полный образ Python и копировалось всё подряд.
Запустил: "docker run -d -p 5000:5000 --name app-bad myapp:bad, curl localhost:5000". Приложение работает.
<img width="1280" height="631" alt="image" src="https://github.com/user-attachments/assets/69477c00-71a0-4d9a-a203-d8da0f6f5cf1" />

2. Улучшение образа
Сделал более правильный Dockerfile: использовал python:3.12-slim, добавил .dockerignore, убрал лишние файлы.
Собрал: "docker build -t myapp:good .". Размер стал намного меньше.
<img width="862" height="198" alt="image" src="https://github.com/user-attachments/assets/3bff05fd-e372-42d6-9799-a04972877b78" />

3. Ограничение ресурсов
Запустил контейнер с лимитами: "docker run -d -p 5001:5000 --name app-good --memory="128m" --cpus="0.5" myapp:good".
Проверил: "docker stats app-good". Видно, что контейнер не превышает заданные лимиты.
<img width="963" height="140" alt="image" src="https://github.com/user-attachments/assets/30418644-77c4-47cb-8b1a-458c311d48a9" />

4. СЛои
Посмотрел структуру образа: "docker history myapp:good"
Видно, из каких слоёв он состоит (база, зависимости, приложение).
<img width="1175" height="492" alt="image" src="https://github.com/user-attachments/assets/a14e5e8e-716f-43ba-8064-c63a72a0c07e" />
<img width="1175" height="492" alt="image" src="https://github.com/user-attachments/assets/4beae478-af78-41f7-8c3d-e0ba31a1a1d7" />

5. Публикация
Загрузил образ в Docker Hub: "docker tag myapp:good <username>/flask-demo:v1.0, docker push <username>/flask-demo:v1.0"


Контрольный вопрос: Почему образ такой большой?

Образ получился большим, потому что используется базовый образ python:3.12, который сам по себе тяжёлый, и в него копируется весь проект целиком. Также при pip install остаётся кэш и лишние файлы, что дополнительно увеличивает размер. 
