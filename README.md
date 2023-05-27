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

### Задание 3

Установил ПО Rsync. Настроил синхронизацию на двух нодах. Протестировал работу сервиса.

1. `Выполнил все этапы по заданию`

![Config_backup-node1.sh.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/Config_backup-node1.sh.png)`

![node1_backup_&_dir-scripts.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_backup_%26_dir-scripts.png)`

![node2-mkdir_&_touch.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2-mkdir_%26_touch.png)`

![node2_config_rsyncd.conf.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2_config_rsyncd.conf.png)`

![node2_config_rsyncd.conf_home.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2_config_rsyncd.conf_home.png)`

![node2_dir-etc.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node2_dir-etc.png)`

![node1_data_backup.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_data_backup.png)`

![node1_home_backup.png](https://github.com/oleghamov/Reserv_copy-10-04-27-05-23-hw-/blob/master/node1_home_backup.png)`
















