# Домашнее задание к занятию 1 «Disaster recovery и Keepalived» - `Александра Бужор`
---

### Задание 1 

- Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
- На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
- Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
- Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
- На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

#### Ответ:

![image](https://github.com/user-attachments/assets/89c25134-08bb-496a-baa0-76665ca56699)

![image](https://github.com/user-attachments/assets/5367ea38-1066-4a08-aea7-7cf7f06f3670)

![image](https://github.com/user-attachments/assets/6ea5b051-5a8f-48b6-97d3-2dc16b02f99b)

### Ссылка на файл: [hsrp_advanced_DZ1.pkt](https://github.com/AngryCFO/DR/blob/4bad1d6091f8919c14a1cf00f31030652774e194/hsrp_advanced_DZ1.pkt)
---

### Задание 2 

- Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
- Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
- Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
- Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
- На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

#### Ответ:
```
#!/bin/bash
if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then
        exit 0
else
        sudo systemctl stop keepalived
fi
```

### Ссылка на файл: [keepalived.conf](https://github.com/AngryCFO/DR/blob/66ffad9f45a6623bacaa420a94890990ceb9e70c/keepalived.conf)

![image](https://github.com/user-attachments/assets/5201f6e1-191b-4c01-9e38-28448f98fe4e)
![image](https://github.com/user-attachments/assets/3ff5342b-7374-4190-9f55-4e11da5599dc)
![image](https://github.com/user-attachments/assets/4375de49-32d0-482d-9d75-1a4d6cc88ce8)
![image](https://github.com/user-attachments/assets/7980178d-fd53-4706-a058-d4e0850dcfab)

---

