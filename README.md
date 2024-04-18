
# Домашнее задание к занятию 1 «Disaster recovery и Keepalived»



### Задание 1
- Дана [схема](1/hsrp_advanced.pkt) для Cisco Packet Tracer, рассматриваемая в лекции.
- На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
- Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
- Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
- На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

### *Ответ*

<details>

![Снимок01](https://github.com/George210890/1.md/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA01.PNG)

![Снимок02](https://github.com/George210890/1.md/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA02.PNG)

![Снимок03](https://github.com/George210890/1.md/blob/main/%D0%A1%D0%BD%D0%B8%D0%BC%D0%BE%D0%BA03.PNG)

Файл PKT https://github.com/George210890/1.md/blob/main/hsrp_advanced_DZ1.pkt

</details>

------

### Задание 2
- Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного [файла](1/keepalived-simple.conf).
- Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
- Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
- Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
- На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

### *Ответ*

<details>

```
#!/bin/bash
if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then
        exit 0
else
        sudo systemctl stop keepalived
fi
```

Файл конфига https://github.com/Ivashka80/Disaster-recovery_Keepalived/blob/main/keepalived.conf

![image](https://github.com/Ivashka80/Disaster-recovery_Keepalived/assets/121082757/fbf9888d-5acc-4217-95af-2b33df123c20)

![image](https://github.com/Ivashka80/Disaster-recovery_Keepalived/assets/121082757/33d85673-d882-434f-9da8-49d8612cbf84)

![image](https://github.com/Ivashka80/Disaster-recovery_Keepalived/assets/121082757/cdcf9435-0a52-4e49-9686-51a9070ef5fe)

![image](https://github.com/Ivashka80/Disaster-recovery_Keepalived/assets/121082757/bcfaa39d-3104-4576-b8bc-df45b850793d)

</details>


------

<details>

