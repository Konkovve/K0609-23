1.
Для начала были просмотрены namespace-ы текущего процесса. После выполнения команды был получен список неймспейсов, связанных с текущим процессом. Каждый из них отвечает за какойто аспект изоляции (PID, сеть, файловая система и т.д.). ТУт понимаем, что в линуксе процессы могут работать в разных пространствах. Также команда: "lsns" - показала список всех неймспейсов в системе. Видно, что у разных процессов свои неймспейсы, то есть они уже изолированы друг от друга.
<img width="1103" height="1009" alt="image" src="https://github.com/user-attachments/assets/b799d9ac-0d41-4ebc-b2cd-056d4bbe685c" />

Запустил bash в новом PID namespace: "sudo unshare --pid --fork --mount-proc /bin/bash"
Проверил PID: "echo $$". Показало 1, то есть внутри этого окружения мой процесс стал главным.
Дальше: "ps aux". Вывод показал только несколько процессо. Остальных процессов системы нет — значит изоляция работает.
После проверка сети: "sudo unshare --net /bin/bash, ip link show". Отобразился только интерфейс lo (loopback). Обычных интерфейсов типа eth0 нет - это значит, что сеть полностью изолирована.
<img width="884" height="521" alt="image" src="https://github.com/user-attachments/assets/c69c92e9-f888-4e4e-9773-eda7df96779a" />

Контрольный вопрос: Почему после exit процессы хоста остались нетронутыми?

Процессы хоста не затронулись, потому что я работал в отдельном PID namespace. Внутри него все процессы изолированы и имеют свою нумерацию (bash был PID 1). После exit завершились только процессы внутри этого namespace, а процессы хоста остались работать, так как находятся в другом пространстве имён.




2.
Создал свою cgroup: "sudo mkdir /sys/fs/cgroup/mytest, echo "20000 100000" | sudo tee /sys/fs/cgroup/mytest/cpu.max" - это ограничивает CPU примерно до 20%.
Запустил нагрузку: "stress-ng --cpu 1 --timeout 30s &".
Добавил процесс в группу: "echo $! | sudo tee /sys/fs/cgroup/mytest/cgroup.procs"
Проверил: "cat /sys/fs/cgroup/mytest/cpu.max". Показало 20000 100000, то есть лимит применился.
Также: "cat /sys/fs/cgroup/mytest/cpu.stat". Там видно, что процесс тротлит.
<img width="900" height="472" alt="image" src="https://github.com/user-attachments/assets/b914175a-a243-42d2-8248-12f4d142f556" />
<img width="682" height="196" alt="image" src="https://github.com/user-attachments/assets/eea8f864-4433-44b9-8db7-5c2236245c64" />
<img width="1145" height="977" alt="image" src="https://github.com/user-attachments/assets/69cd8fb9-d0ba-4e51-abc7-9c03874e34d9" />

Контрольный вопрос: Что произойдёт если лимит памяти превысить? (OOM-killer)

Если процесс превысит лимит памяти, сработает OOM-killer. Он выберет и завершит один из процессов (обычно тот, кто потребляет больше всего памяти), чтобы освободить ресурсы.



Создал минимальную файловую систему: "mkdir -p /tmp/myroot/{bin,lib,lib64,proc,dev}, cp /bin/bash /tmp/myroot/bin/, cp /bin/ls /tmp/myroot/bin/"
Скопировал зависимости и зашёл: "sudo chroot /tmp/myroot /bin/bash"
Внутри проверил: "ls /".
Видны только те папки, которые я сам создал. /home, /etc и т.д. - их нет.
<img width="1197" height="963" alt="image" src="https://github.com/user-attachments/assets/114ea78e-2b8d-4eb4-baff-08396bae4e92" />
<img width="1162" height="312" alt="image" src="https://github.com/user-attachments/assets/ab41ab18-580f-43c3-8694-a45c35f01dc7" />
