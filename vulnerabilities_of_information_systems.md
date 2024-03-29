# Домашнее задание к занятию «Уязвимости и атаки на информационные системы»

### Инструкция по выполнению домашнего задания

1. Сделайте fork [репозитория c шаблоном решения](https://github.com/netology-code/sys-pattern-homework) к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/gitlab-hw или https://github.com/имя-вашего-репозитория/8-03-hw).
2. Выполните клонирование этого репозитория к себе на ПК с помощью команды `git clone`.
3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
   - впишите вверху название занятия и ваши фамилию и имя;
   - в каждом задании добавьте решение в требуемом виде: текст/код/скриншоты/ссылка;
   - для корректного добавления скриншотов воспользуйтесь инструкцией [«Как вставить скриншот в шаблон с решением»](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md);
   - при оформлении используйте возможности языка разметки md. Коротко об этом можно посмотреть в [инструкции по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md).
4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`).
5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
6. Любые вопросы задавайте в чате учебной группы и/или в разделе «Вопросы по заданию» в личном кабинете.

Желаем успехов в выполнении домашнего задания.

------

### Задание 1

Скачайте и установите виртуальную машину Metasploitable: https://sourceforge.net/projects/metasploitable/.

Это типовая ОС для экспериментов в области информационной безопасности, с которой следует начать при анализе уязвимостей.

Просканируйте эту виртуальную машину, используя **nmap**.

Попробуйте найти уязвимости, которым подвержена эта виртуальная машина.

Сами уязвимости можно поискать на сайте https://www.exploit-db.com/.

Для этого нужно в поиске ввести название сетевой службы, обнаруженной на атакуемой машине, и выбрать подходящие по версии уязвимости.

Ответьте на следующие вопросы:

- Какие сетевые службы в ней разрешены?
- Какие уязвимости были вами обнаружены? (список со ссылками: достаточно трёх уязвимостей)
  
*Приведите ответ в свободной форме.*  


Ответ:

![Скриншот-1](https://github.com/olegstrigunov/Sec/blob/main/screanshots/1.png)

Разрешены следующие службы: ftp, ssh, telnet, smtp, domain, http, rpcbind, netbios-ssn, exec, login, tcpwrapped, java-rmi, bindshell, nfs, ftp, mysql, postgresql, vnc, X11, irc, ajp13, http

Уязвимости:

https://www.exploit-db.com/exploits/17491

https://www.exploit-db.com/exploits/6122

https://www.exploit-db.com/exploits/30020
### Задание 2

Проведите сканирование Metasploitable в режимах SYN, FIN, Xmas, UDP.

Запишите сеансы сканирования в Wireshark.

Ответьте на следующие вопросы:

- Чем отличаются эти режимы сканирования с точки зрения сетевого трафика?
- Как отвечает сервер?

*Приведите ответ в свободной форме.

Ответ:

SYN - производится отправка SYN-пакета, с намерением открыть соединение, и ожидает ответ. Наличие флагов SYN|ACK в ответе указывает на то, что порт открыт и прослушивается. Флаг RST в ответе означает обратное. Если Nmap принимает пакет SYN|ACK, то отправляет RST-пакет для сброса соединения.

![Скриншот-2](https://github.com/olegstrigunov/Sec/blob/main/screanshots/2.png)

FIN - производдится отправка FIN-пакет, в TCP заголовок ставится флаг FIN. Согласно RFC 793, на полученый FIN-пакет на закрытый порт сервер отвечает пакетом RST. FIN-пакеты на открытые порты игнорируются сервером. По этому различию становится возможным отличить закрытый порт от открытого.

![Скриншот-3](https://github.com/olegstrigunov/Sec/blob/main/screanshots/3.png)

Xmas - Устанавливаются FIN, PSH и URG флаги. Если в результате FIN-сканирования мы получили список открытых портов, то это не Windows. Если же все эти методы выдали результат, что все порты закрыты, а SYN-сканирование обнаружило открытые порты, то мы скорей всего имеете дело с ОС Windows, Cisco, BSDI, IRIX, HP/UX и MVS. Все эти ОС не отправляют RST-пакеты.

![Скриншот-4](https://github.com/olegstrigunov/Sec/blob/main/screanshots/4.png)

UDP - На каждый порт сканируемой машины отправляется UDP-пакет без данных. Это нужно чтобы понять, какие UDP-порты на сканируемом хосте являются открытыми.Если в ответ было получено ICMP-сообщение "порт недоступен", то порт закрыт. В противном случае предполагается, что сканируемый порт открыт.

![Скриншот-5](https://github.com/olegstrigunov/Sec/blob/main/screanshots/5.png)
