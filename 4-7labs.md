# 4 Лабораторная:

1. Чему научился:

В ходе выполнения лабораторной работы был получен базовый практический опыт работы с Kubernetes-кластером.
Понял как подключаться к контейнеру, и что там можно увидеть. Понял, что кубернетис при принудительном завершении процесса - перезагружается. И в целом, понял зачем Pod нужен.

2. Возникшие проблемы и способы их решения

Основная проблема с тем, что я делал с ks3, а много команд написаны под minikube. и переодически я просто не понимал почему у меня не запускается что-то.

<img width="1173" height="532" alt="image" src="https://github.com/user-attachments/assets/840627db-894d-47dd-8c69-b22eba18231e" />
<img width="1280" height="738" alt="image" src="https://github.com/user-attachments/assets/fee1149d-215c-4ab7-9b66-3fb50b20e049" />
<img width="964" height="389" alt="image" src="https://github.com/user-attachments/assets/ec1317b8-d59d-4056-9c63-15cbf55545ff" />
<img width="1280" height="444" alt="image" src="https://github.com/user-attachments/assets/bb5198a1-947f-41b1-b148-0c7c0e2859b2" />
<img width="359" height="166" alt="image" src="https://github.com/user-attachments/assets/52b5a872-1595-4674-9c76-d8f7c83e03e8" />


<img width="1174" height="386" alt="image" src="https://github.com/user-attachments/assets/b261e918-57ab-4393-b634-93828d81ad7f" />
<img width="1245" height="1011" alt="image" src="https://github.com/user-attachments/assets/b18c8baa-1231-453e-b41b-ac9ebab501ea" />
<img width="1056" height="642" alt="image" src="https://github.com/user-attachments/assets/cd9434bc-b4f4-4bb4-9b62-5c5f270ca9e4" />
<img width="1280" height="980" alt="image" src="https://github.com/user-attachments/assets/aed79293-8e59-49c9-8243-68fd15514d0d" />


<img width="1280" height="980" alt="image" src="https://github.com/user-attachments/assets/09a2ba42-6328-4290-ba6a-8e81ba33ff21" />
<img width="910" height="483" alt="image" src="https://github.com/user-attachments/assets/08729357-77cf-4625-b68f-27cec90c27b7" />
<img width="1280" height="687" alt="image" src="https://github.com/user-attachments/assets/1d02ab7b-c60b-4e4b-aae1-3a2c7f802520" />
<img width="892" height="977" alt="image" src="https://github.com/user-attachments/assets/4cd320f0-e8f3-47a1-8876-4f3846ec77fb" />


<img width="892" height="977" alt="image" src="https://github.com/user-attachments/assets/bb304b40-f063-4eba-bb95-f8dab5c4800d" />



3. Ответы на контрольные вопросы

Вопрос 1: Какие pod-ы в kube-system должны быть всегда Running?

kube-apiserver, kube-controller-manager, kube-scheduler, etcd, coredns, kube-proxy - они обеспечивают функционирование всего Kubernetes-кластера.

Вопрос 2: Почему Pod перезапускается после завершения процесса? Кто за это отвечает?

Kubernetes постоянно отслеживает состояние Pod через kubelet. Если основной процесс контейнера завершается, система автоматически пытается восстановить его в соответствии с заданной политикой, поэтому он перезапускается.

Вопрос 3: Чем Pod отличается от контейнера?

Контейнер - это отдельный запущенный процесс с изоляцией.
Pod - более глобальная система в плане того, что он может включать в себя нескоько контейнеров, которые объеденены общей ссетью, диском, настройками.
