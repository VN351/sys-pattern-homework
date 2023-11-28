# Домашнее задание к занятию "`Защита хоста`" - `Невзоров Владислав Викторович`


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
# Задание 1
1. Установите eCryptfs.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/install-ecryptfs.png)
2. Добавьте пользователя cryptouser.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/create-cryptouser.png)
3. Зашифруйте домашний каталог пользователя с помощью eCryptfs.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cryptouser-file.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cryptouser-crypt.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cryptouser-after-crypt.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/cryptouser-eror.png)

В качестве ответа пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.

# Задание 2
1. Установите поддержку LUKS.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/install-LUKS.png)
2. Создайте небольшой раздел, например, 100 Мб.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/create-disk.png)
3. Зашифруйте созданный раздел с помощью LUKS.
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/crypto-disk.png)
![alt text](https://github.com/VN351/sys-pattern-homework/raw/main/img/mount-crypto-disk.png)

В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.
