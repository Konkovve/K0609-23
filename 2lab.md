https://hub.docker.com/r/konkovvv/flask-demo

<img width="1280" height="631" alt="image" src="https://github.com/user-attachments/assets/69477c00-71a0-4d9a-a203-d8da0f6f5cf1" /><img width="1280" height="631" alt="image" src="https://github.com/user-attachments/assets/f2f5d771-eb09-4292-9178-a30d2d430eee" />
<img width="1280" height="631" alt="image" src="https://github.com/user-attachments/assets/ff98f5ef-a74f-42a1-aee2-c24006f30354" />

Контрольный вопрос: Почему образ такой большой?

Образ получился большим, потому что используется базовый образ python:3.12, который сам по себе тяжёлый, и в него копируется весь проект целиком. Также при pip install остаётся кэш и лишние файлы, что дополнительно увеличивает размер. 

<img width="862" height="198" alt="image" src="https://github.com/user-attachments/assets/3bff05fd-e372-42d6-9799-a04972877b78" />
<img width="963" height="140" alt="image" src="https://github.com/user-attachments/assets/30418644-77c4-47cb-8b1a-458c311d48a9" />
<img width="1175" height="492" alt="image" src="https://github.com/user-attachments/assets/a14e5e8e-716f-43ba-8064-c63a72a0c07e" />
<img width="1175" height="492" alt="image" src="https://github.com/user-attachments/assets/4beae478-af78-41f7-8c3d-e0ba31a1a1d7" />
