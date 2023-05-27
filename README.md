# Домашнее задание к занятию "Резервное копирование" - `Хамов Олег`

### Задание 1

Полное резервное копирование (Full Backup)
Создается полная копия набора данных. С точки зрения скорости восстановления и уровня надежности считается наиболее выигрышным вариантом бэкапа. Однако у полного резервного копирования есть и минусы — full backup требует много времени для создания копии и создает существенную нагрузку на сеть.
Плюсы:
    • высокая скорость восстановления данных;
    • высокий уровень надежности — все данные в одном бэкапе;
    • простота управления.
Минусы:
    • необходимо много места для хранения копий;
    • высокая нагрузка на сеть;
    • требует много времени для создания бэкапа.

Дифференциальное резервное копирование (Differential Backup)
Подразумевает создание резервной копии, которая включает только те данные, которые были изменены с момента создания предыдущего полного бэкапа.
Плюсы:
    • более высокая скорость создания копий по сравнению с full backup;
    • по скорости восстановления быстрее инкрементного, но медленнее полного бэкапа;
    • по надежности выигрывает у инкрементного бэкапа.
Минусы:
    • каждый новый дифференциальный бэкап требует создается дольше и требует больше места, чем предыдущий.

Инкрементальное резервное копирование (Incremental Backup)
При использовании этого метода резервная копия будет содержать только изменения, сделанные с момента последнего резервного копирования.
Плюсы:
    • высокая скорость создания копий;
    • копии занимают мало места;
    • бэкапы занимают мало места;
    • не создает высокой нагрузки на сеть.
Минусы:
    • трудоемкость восстановления данных;
    • риск неудачного восстановления при повреждении какого-либо сегмента из цепочки бэкапа.

### Задание 2

Установил ПО Bacula, настроил bacula-dir, bacula-sd, bacula-fd. Протестировал работу сервисов.

. `Выполнил все этапы по заданию`

![bacula-dir.conf.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-dir.conf.png)`

![bacula-dir.conf2.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-dir.conf2.png)`

![bacula-dir.conf3.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-dir.conf3.png)`

![bacula-dir.conf4.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-dir.conf4.png)`

![bacula-fd.conf.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-fd.conf.png)`

![bacula-sd.conf.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-sd.conf.png)`

![bacula-sd.conf2.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-sd.conf2.png)`

![bacula-sd.conf3.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/bacula-sd.conf3.png)`

![result1.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/result1.png)`

![result2.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/result2.png)`

### Задание 3

Установил ПО Rsync. Настроил синхронизацию на двух нодах. Протестировал работу сервиса.

Сначала я создал на клиенте пустой каталог /data и его бекапил, потом в этом каталоге насоздовал подкаталогов "oleghamov 1,2,3", а в них файлы "test_file.txt 1,2,3,4,5" и сбекапил содержимое каталога /data.
Дальше я изменил в конфигурации папку, которая будет архивироваться с /data на /home и бекапнул её (сделал скриншоты всех этапов, а также конфигов и содержимое каталогов на обеих нодах)

1. `Выполнил все этапы по заданию`

Сервер backup-node1.sh:

....#!/bin/bash
....date
....syst_dir=/backup/
srv_name=node2 #из тестовой конфигурации
srv_ip=192.168.1.11
srv_user=backup
srv_dir=home
echo "Start backup ${srv_name}"
mkdir -p ${syst_dir}${srv_name}/increment/
/usr/bin/rsync -avz --progress --delete --password-file=/etc/rsyncd.scrt ${srv_user}@${srv_ip}::${srv_dir} ${syst_dir}${srv_name}/current/ --backup --backup-dir=${syst_dir}${srv_name}/increment/`date +%Y-%m-%d`/
/usr/bin/find ${syst_dir}${srv_name}/increment/ -maxdepth 1 -type d -mtime +30 -exec rm -rf {} \;
date
echo "Finish backup ${srv_name}"

Клиент rsyncd.conf:

pid file = /var/run/rsyncd.pid
log file = /var/log/rsyncd.log
transfer logging = true
munge symlinks = yes
[home]
path = /home
uid = root
read only = yes
list = yes
comment = Data backup Dir
auth users = backup
secrets file = /etc/rsyncd.scrt

![Config_backup-node1.sh.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/Config_backup-node1.sh.png)`

![node1_backup_&_dir-scripts.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_backup_%26_dir-scripts.png)`

![node2-mkdir_&_touch.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2-mkdir_%26_touch.png)`

![node1_data_backup.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_data_backup.png)`

![node2_dir-etc.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2_dir-etc.png)`

![node2_config_rsyncd.conf_home.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2_config_rsyncd.conf_home.png)`

![node1_home_backup.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_home_backup.png)`
















