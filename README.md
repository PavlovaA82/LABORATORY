Прежде чем приступить к выполнению задания, необходимо установить Oracle Linux на VirtualBox.
После установки Oracle Linux убедитесь, что он работает корректно.

После проверки вам необходимо открыть командную строку и приступать к работе с командной строкой.

Приступаем к установке Docker:

Чтобы установить утилиту `wget` с помощью пакетного менеджера `yum` , выполните команду:

-`sudo yum install wget`

![image](https://github.com/user-attachments/assets/21ee432b-11fe-4bbd-9e57-c80567a52b6e)

Затем устанавливаем утилиту `curl`:

-`sudo yum install curl`

![image](https://github.com/user-attachments/assets/3d7833ab-8b79-406c-ad23-4566b7b4b0d3)

Выполняем скачивание репозитория Docker:

Команда `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo` используется для скачивания файла репозитория Docker и сохранения его в директорию /etc/yum.repos.d/ на системе Oracle Linux.

![image](https://github.com/user-attachments/assets/29ebcbbd-9be4-4e96-a215-38f94f7fc218)

Команда `sudo yum install docker-ce docker-ce-cli containerd.io` служит для установки Docker  и сопутствующих компонентов на Oracle Linux-систему с помощью пакетного менеджера `yum` :

![image](https://github.com/user-attachments/assets/44734710-688b-4c0b-bd85-6cfed88917d6)
![image](https://github.com/user-attachments/assets/ecd0ce93-e16c-41d4-bb5e-72bc8bdbedf6)

С помощью команды `sudo systemctl enable docker --now` выполняется включение и запуск службы Docker на системе, управляемой через `systemd`:

![image](https://github.com/user-attachments/assets/b3441a4c-069d-4aa8-8b58-06d0fc20eeec)

Далее пишем команду:

`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Эта команда извлекает номер тега последней версии Docker Compose с помощью API GitHub и сохраняет его в переменной `COMVER`.

![image](https://github.com/user-attachments/assets/b0fa8028-ee55-4d6d-8841-3ab1c5d56058)

