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

https://drive.google.com/file/d/1dyozJ6ognU81kKghTuAB4xoyVVtKzMyu/view?usp=sharing 

### Задание 2

Что нужно сделать:
1. Создайте новый проект pipeline.
2. Перепишите сборку из задания 1 на declarative в виде кода.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---
```
pipeline {
 agent any
 stages {
  stage('Git') {
   steps {
    git branch: 'main', url: 'https://github.com/VN351/sdvps-materials.git'
   }
  }
  stage('Test') {
   steps {
    sh 'go test .'
   }
  }
  stage('Build') {
   steps {
    sh 'docker build .'
   }
  }
 }
}
```
---
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-2-1.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-2-2.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-2-3.png)

### Задание 3-4

Что нужно сделать:

1. Установите на машину Nexus.
2. Создайте raw-hosted репозиторий.
3. Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
4. Загрузите файл в репозиторий с помощью jenkins.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---
```
pipeline {
    agent any
    stages {
        stage('Git') {
            steps {
                git branch: 'main', url: 'https://github.com/VN351/sdvps-materials.git'
            }
        }
        stage('Test') {
            steps {
                sh 'go test .'
            }
        }
        stage('Build') {
            steps {
                sh 'CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o app .'
            }
        }
        stage('Push') {
            steps {
                sh 'curl -v -u admin:admin --upload-file ./app "http://192.168.90.56:8081/repository/task3/myapp/myapp:v${BUILD_NUMBER}"'
            }
        }
    }
}
```
---
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-3-1.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-3-2.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/Task-3-3.png)
