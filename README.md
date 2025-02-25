Прежде чем приступить к выполнению задания, необходимо установить Oracle Linux на VirtualBox.
После установки Oracle Linux убедитесь, что он работает корректно.

После проверки вам необходимо открыть командную строку и приступать к работе с командной строкой.

Приступаем к установке Docker:

Чтобы установить утилиту `wget` с помощью пакетного менеджера `yum` , выполните команду:

➝`sudo yum install wget`

![image](https://github.com/user-attachments/assets/a9ba59f3-595d-403f-89a3-9b6fb8e99578)

Затем устанавливаем утилиту `curl`:

➝`sudo yum install curl`

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

➝`COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Эта команда извлекает номер тега последней версии Docker Compose с помощью API GitHub и сохраняет его в переменной `COMVER`.

![image](https://github.com/user-attachments/assets/b0fa8028-ee55-4d6d-8841-3ab1c5d56058)

➝`sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

Данная команда загружает и устанавливает Docker Compose в системный каталог, соответствующий вашей операционной системе и архитектуре. 

![image](https://github.com/user-attachments/assets/6fe49830-c73e-40d3-b173-e31bc4a0f033)

Команды, которые используются:

➝`sudo chmod +x /usr/bin/docker-compose`

➝`docker-compose --version`

Данная команда делает файл `docker-compose` в каталоге `/usr/bin/` исполняемым, что позволяет запускать его из командной строки. Следующая команда выводит установленную версию Docker Compose системе.

![image](https://github.com/user-attachments/assets/91876f6e-1940-4f7d-a91b-b4c81d993132)

Эта команда клонирует репозиторий `grafana_stack_for_docker` с GitHub на вашу локальную машину:

➝`git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/56aeca34-c4b3-4335-9c09-91e4c2dc408e)

Далее выполняем следующие команды:

➤`cd grafana_stack_for_docker` — переходит в каталог с конфигурацией Grafana. 

➜`sudo mkdir -p /mnt/common_volume/swarm/grafana/config` — создает каталог для конфигурации Grafana.

➝`sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}` — создает каталоги для конфигурации и данных Grafana и Prometheus.  

➝`sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}` — изменяет владельца каталогов на текущего пользователя. 

➝`touch /mnt/common_volume/grafana/grafana-config/grafana.ini` — создает файл конфигурации Grafana, если его нет.

➝`cp config/* /mnt/common_volume/swarm/grafana/config/` — копирует файлы конфигурации в нужную директорию. 

➝`mv grafana.yaml docker-compose.yaml` — переименовывает конфигурационный файл для Docker Compose.

![image](https://github.com/user-attachments/assets/024ca827-c94a-42c9-8ca8-4e7f61de6bb2)


