Прежде чем приступить к выполнению задания, необходимо установить Oracle Linux на VirtualBox.

После установки Oracle Linux убедитесь, что он работает корректно, 

после проверки вам необходимо открыть командную строку и приступать к работе с командной строкой.

Лаб 1
1.Начинаем установку sudo yum install wget

![image](https://github.com/user-attachments/assets/21ee432b-11fe-4bbd-9e57-c80567a52b6e)

2.Установка sudo yum install curl

![image](https://github.com/user-attachments/assets/3d7833ab-8b79-406c-ad23-4566b7b4b0d3)

3.Установка sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo

![image](https://github.com/user-attachments/assets/29ebcbbd-9be4-4e96-a215-38f94f7fc218)

4.Установка docker, sudo yum install docker-ce docker-ce-cli containerd.io

![image](https://github.com/user-attachments/assets/44734710-688b-4c0b-bd85-6cfed88917d6)
![image](https://github.com/user-attachments/assets/ecd0ce93-e16c-41d4-bb5e-72bc8bdbedf6)

5.Запускаем его и разрешаем автозапуск с помощью команды: sudo systemctl enable docker --now

![image](https://github.com/user-attachments/assets/b3441a4c-069d-4aa8-8b58-06d0fc20eeec)
