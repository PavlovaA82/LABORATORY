
![image](https://github.com/user-attachments/assets/8679470b-6ce3-4288-a039-07795c07cacc)

Docker
--------------------------------------------------------------------------------------------

Прежде чем приступить к выполнению задания, необходимо установить Oracle Linux на VirtualBox.
После установки Oracle Linux убедитесь, что он работает корректно.

После проверки вам необходимо открыть командную строку и приступать к работе с командной строкой.

Приступаем к установке Docker:

Чтобы установить утилиту `wget` с помощью пакетного менеджера `yum` , выполните команду:

➤ `sudo yum install wget`

![image](https://github.com/user-attachments/assets/a9ba59f3-595d-403f-89a3-9b6fb8e99578)

Затем устанавливаем утилиту `curl`:

➤ `sudo yum install curl`

![image](https://github.com/user-attachments/assets/3d7833ab-8b79-406c-ad23-4566b7b4b0d3)

Выполняем скачивание репозитория Docker:

Команда `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo` используется для скачивания файла репозитория Docker и сохранения его в директорию `/etc/yum.repos.d/` на системе Oracle Linux.

![image](https://github.com/user-attachments/assets/29ebcbbd-9be4-4e96-a215-38f94f7fc218)

Команда `sudo yum install docker-ce docker-ce-cli containerd.io` служит для установки Docker  и сопутствующих компонентов на Oracle Linux-систему с помощью пакетного менеджера `yum` :

![image](https://github.com/user-attachments/assets/44734710-688b-4c0b-bd85-6cfed88917d6)
![image](https://github.com/user-attachments/assets/ecd0ce93-e16c-41d4-bb5e-72bc8bdbedf6)

С помощью команды `sudo systemctl enable docker --now` выполняется включение и запуск службы Docker на системе, управляемой через `systemd`:

![image](https://github.com/user-attachments/assets/b3441a4c-069d-4aa8-8b58-06d0fc20eeec)

Далее пишем команду:

➤ `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Эта команда извлекает номер тега последней версии Docker Compose с помощью API GitHub и сохраняет его в переменной `COMVER`.

![image](https://github.com/user-attachments/assets/b0fa8028-ee55-4d6d-8841-3ab1c5d56058)

➤ `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

Данная команда загружает и устанавливает Docker Compose в системный каталог, соответствующий вашей операционной системе и архитектуре. 

![image](https://github.com/user-attachments/assets/6fe49830-c73e-40d3-b173-e31bc4a0f033)

Команды, которые используются:

➤ `sudo chmod +x /usr/bin/docker-compose`

➤ `docker-compose --version`

Данная команда делает файл `docker-compose` в каталоге `/usr/bin/` исполняемым, что позволяет запускать его из командной строки. Следующая команда выводит установленную версию Docker Compose системе.

![image](https://github.com/user-attachments/assets/91876f6e-1940-4f7d-a91b-b4c81d993132)

Эта команда клонирует репозиторий `grafana_stack_for_docker` с GitHub на вашу локальную машину:

➤ `git clone https://github.com/skl256/grafana_stack_for_docker.git`

![image](https://github.com/user-attachments/assets/56aeca34-c4b3-4335-9c09-91e4c2dc408e)

Далее выполняем следующие команды:

➤ `cd grafana_stack_for_docker` — переходит в каталог с конфигурацией Grafana. 

➤ `sudo mkdir -p /mnt/common_volume/swarm/grafana/config` — создает каталог для конфигурации Grafana.

➤ `sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}` — создает каталоги для конфигурации и данных Grafana и Prometheus.  

➤ `sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}` — изменяет владельца каталогов на текущего пользователя. 

➤ `touch /mnt/common_volume/grafana/grafana-config/grafana.ini` — создает файл конфигурации Grafana, если его нет.

➤ `cp config/* /mnt/common_volume/swarm/grafana/config/` — копирует файлы конфигурации в нужную директорию. 

➤ `mv grafana.yaml docker-compose.yaml` — переименовывает конфигурационный файл для Docker Compose.

![image](https://github.com/user-attachments/assets/024ca827-c94a-42c9-8ca8-4e7f61de6bb2)

➤ `sudo docker compose up -d`

создает и запускает контейнеры согласно файлу docker-compose.yaml. Флаг -d позволяет запускать их в фоновом режиме.

![image](https://github.com/user-attachments/assets/cfb0f6ff-90b9-433f-a58c-9c8e8595e2ea)

На скриншоте представлен файл `docker-compose.yaml`, открытый в редакторе `vi` с правами `sudo`.

➤ `sudo vi docker-compose.yaml`

Это позволяет редактировать файл, который описывает сервис Grafana в Docker Compose, включая образ, порты, переменные окружения и настройки хранения данных.

![image](https://github.com/user-attachments/assets/24c86f75-5e42-4a0f-ad86-8d3ffc44fda5)

➤ `sudo docker compose stop` — останавливает запущенные контейнеры, но не удаляет их. 

![image](https://github.com/user-attachments/assets/105f5e1c-c7b1-4388-ac59-b51e74ef41cd)

➤ `sudo docker compose up -d` — создает и запускает контейнеры в фоновом режиме, если они не запущены.

![image](https://github.com/user-attachments/assets/c3b9a10c-17df-4185-80e3-55303f367351)

➤ `sudo docker compose down` — останавливает и удаляет контейнеры, а также сеть, созданную для них.

![image](https://github.com/user-attachments/assets/ccd4c819-9fb7-4f3f-b7ee-e41fcb2b098f)

На скриншоте выполняются следующие действия:  

1. Клонирование репозитория LABORATORY1 с GitHub.
    
   Команда:  
  
   ➤ `sudo git clone https://github.com/PavlovaA82/LABORATORY1.git`
   
2. Переход в каталог LABORATORY1 и просмотр файлов.  
   Команды:  
  ➤ `cd LABORATORY1`
   `ls`
   
3. Открытие файла README.md с правами sudo.  
   Команда:  
   ➤ `sudo rm README.md`
   
4. Переход в подкаталог 12 и просмотр его содержимого.  
   Команды:  
   ➤ `cd 12`
   `ls`
   
6. Вывод полного пути текущего каталога.
   
   Команда:
   ➤ `pwd`
   
7. Копирование всех файлов из `/home/pavlova/LABORATORY1/12/` в `/home/pavlova/grafana_stack_for_docker`.  

   Команда:
  
   ➤ `cp /home/pavlova/LABORATORY1/12/* /home/pavlova/grafana_stack_for_docker`
   
![image](https://github.com/user-attachments/assets/ed976a97-8d95-44c4-b7cb-03797cd577c5)

На скриншоте выполняются следующие действия в терминале Linux:  

1. Переход между директориями с помощью cd:  
   ➤ `cd ..` — переход в родительскую директорию.  
   ➤ `cd grafana_stack_for_docker/` — вход в папку `grafana_stack_for_docker`.  

2. Просмотр содержимого директории с помощью ls:  
  Отображение файлов и папок, включая `docker-compose.yaml`, `Readme.md`, `Screenshot_Loki.png`, `Screenshot_Prometheus.png` и папку `config`.  

3. Просмотр полного пути текущей директории с помощью `pwd`.  

4. Удаление файла `docker-compose.yam` с помощью `rm docker-compose.yam.`  
Повторный просмотр содержимого папкики с `ls`, где удалённый файл уже отсутствует.

![image](https://github.com/user-attachments/assets/53b05971-831d-4841-a635-12dcdcd5cd7f)

С помощью команды `sudo vi prometheus.yaml `открываем редактор `vi`. Tак же прописываем команду `cd /mnt/common_volume/swarm/grafana/config`. В этом файле необходимо изменить первый IP-адрес на тот, который мы должны были сохранить в памяти. Вставляем его в раздел targets меняем его на `exporter:9100`

![image](https://github.com/user-attachments/assets/8b5a205f-8202-469d-aa87-2f5302c6e27e)

Перед началом работы необходимо проверить файл `ptometeus.yaml` на наличие ошибок и исправить его на `ptometheus.yaml`. В противном случае может возникнуть ошибка открытия несуществующего или некорректного файла.
Выполняем  команды, связанные с управлением контейнерами через Docker Compose. Команда 
`sudo vi ptometheus.yaml` предназначена для открытия файла `ptometheus.yaml` в редакторе `vi` с правами суперпользователя. Команда `sudo docker compose up -d` запускает контейнеры, определенные в `docker-compose.yaml`, в фоновом режиме.

![image](https://github.com/user-attachments/assets/5aa98d9b-d9d1-458f-8d35-5ebbc06c905f)

Grafana
-----------------------------------------------------------------------------------------------------------------------------------------------------

1. В Oracle Linux переходим на сайт: `localhost:3000`

   ➤ User & Password: admin
 
      * Код графаны: 3000

      * Код прометеуса: http://prometheus:9090

2. В меню выбираем вкладку Dashboards и создаем Dashboard

   ➤ Ждем кнопку +Add visualization, а после "Configure a new data source", выбираем Prometheus
   
3. Connection: `http://prometheus:9090`

4. Authentication

    ➤ Basic authentication

      * User: admin

      * Password: admin

    ➤ После нажатия кнопки «Save & test» убедитесь, что в результате появится зелёная галочка.

5. В меню необходимо выбрать вкладку «Dashboards» и создать Dashboard. Затем следует дождаться появления кнопки «Import dashboard». Далее в строку `Find and import dashboards for common applications at grafana.com/dashboards` вписываем `1860`. Ждем кнопку Load
   
6. Select Prometheus ждем кнопку "Import"

   Результат:

![image](https://github.com/user-attachments/assets/398b9736-50ee-4bcd-b9f5-94675a85a3d3)


VicroriaMetrics
----------------------------------------------------------------------------------------------------------------------------------------

 ➤ Первым делом заходим на сайт: 

`localhost:3000`

   * Переходим в меню в connection 
 
   * Там пишем http://victoriametrics:8428
 
   * Далее заменяем имя из "Prometheus" на "Vika"
 
   * Нажимаем на dashboards add visualition выбираем "Vika"
 
   * Снизу меняем на "cod"

Далее переходим в командную строку и пишем команду:

`echo -e "# TYPE OILCOINT_metric1 gauge\nOILCOINT_metric1 0" | curl --data-binary @- http://localhost:8428/api/v1/import/prometheus`

Эта команда создаёт метрику `OILCOINT_metric1` типа gauge со значением 0 и отправляет её в Prometheus через HTTP-запрос на `http://localhost:8428/api/v1/import/prometheus.` Это используется для добавления метрик в Prometheus вручную.

Полученный результат:

На сайте: `localhost:3000` 

![image](https://github.com/user-attachments/assets/eb8d3e64-25b1-4359-a4ce-a2e39db52b9b)

На сайте: `localhost:8428`

![image](https://github.com/user-attachments/assets/066dbd87-fdf7-4f8c-8373-bf571de81b6f)

Настройка второй виртуалки
----------------------------------------------------------------------------------------------------------------------------------------

Перед началом работы создаем новую виртуалку и устанавливаем Oracle Linux. После установки нужно установить Docker и docker-compose. 

Устанавливаем команду `sudo yum install wget`:

`sudo` — выполнение команды с правами суперпользователя. `yum` — менеджер пакетов в старых версиях RHEL/Oracle Linux (в новых версиях заменён на dnf). `install wget` — установка пакета `wget` (утилита для загрузки файлов из интернета).

![image](https://github.com/user-attachments/assets/be65805d-4729-44c2-b4ed-7be4ab59bd1b)

Вводим команду `sudo dnf install git-all`

`dnf` — современный менеджер пакетов (аналог `yum` в новых версиях RHEL/Oracle Linux). `git-all`— метапакет, который должен установить Git и дополнительные компоненты (например, GUI-инструменты).

![image](https://github.com/user-attachments/assets/ff1161be-5416-4d82-8665-6373e6234a53)


Далее вводим эти команды:

Скачиваем файл репозитория: 
 
➤ `sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo`

Устанавливаем docker: 
 
 ➤  `sudo yum install docker-ce docker-ce-cli containerd.io`

Запускаем его и разрешаем автозапуск: 
 
 ➤  `sudo systemctl enable docker --now`
 
Для этого сначала убедимся в наличие пакета curl. На системы RPM: 
 
 ➤  `sudo yum install curl` - `curl` — утилита для передачи данных по различным сетевым протоколам

 ![image](https://github.com/user-attachments/assets/4ec0fcbe-962c-4132-ad31-41b6363738f4)

Эта команда получает последнюю версию Docker Compose из GitHub API, извлекает номер версии и сохраняет его в переменную COMVER.

➤ `COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)`

Tеперь скачиваем скрипт docker-compose и помещаем его в каталог /usr/bin: 
 
➤ `sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose`

Даем права файлу на исполнение:  `sudo chmod +x /usr/bin/docker-compose` 
 
Запускаем docker-compose с выводом его версии:  `docker-compose –version`

Настройка брандмауэра
----------------------------------------------------------------------------------------------------------------------------------------

Если на нашем сервере работает брандмауэр, необходимо открыть некторые порты: 
 * 9090/tcp — веб-интерфейс для работы с Prometheus. 
 * 3000/tcp — графана.

 ➤ `firewall-cmd --permanent --add-port={3000,9090}/tcp`

Далее вводим команду: 

 ➤ `firewall-cmd –reload`-применение изменений firewall.

 ![image](https://github.com/user-attachments/assets/b3791a30-bca4-47a4-af17-21661f30d676)


 
 





   
  

   



