# Домашнее задание к занятию "`Disaster recovery и Keepalived`" - `Невзоров Владислав Викторович`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

1. Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
2. На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
3. Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
4. Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
5. На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

---

![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-settings.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-1.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-2.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-3.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-4.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cisco-4.png) 

Ссылка на файл CPT
https://drive.google.com/file/d/1dyozJ6ognU81kKghTuAB4xoyVVtKzMyu/view?usp=sharing 


### Задание 2

1. Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
2. Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
3. Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
4. Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
5. На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

---
script
```
#!/bin/bash

# Проверка доступности порта веб-сервера nginx
nc -z localhost 80
if [ $? -ne 0 ]; then
    exit 1
fi

# Проверка существования файла index.html
if [ ! -f /var/www/html/index.html ]; then
    exit 1
fi

exit 0
```
keepalived-deb-1
```
vrrp_script check_webserver {
        script "/usr/port.sh"
        interval 3
        fall 2
        rise 2
    }
vrrp_instance VI_1 {
    state MASTER
    interface enp0s3
    virtual_router_id 15
    priority 201
    advert_int 1
    virtual_ipaddress {
       192.168.90.14/24
    }
    track_script {
       check_webserver
    }
}

```
keepalived-deb-2
```
vrrp_instance VI_1 {
        state BACKUP
        interface enp0s3
        virtual_router_id 15
        priority 200
        advert_int 1

        virtual_ipaddress {
              192.168.90.14/24
        }

}

```

VM1
---
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-settings-deb1.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-site-deb1.png) 

VM2
---
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-settings-deb2.png)
-
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-site-deb2.png) 
---
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-site.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-script.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-site-no-html.png) 
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/keepalived-site-stop-nginx.png) 
