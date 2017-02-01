### Ad Hoc команды

Ad-hoc команды - это возможность запустить какое-то действие Ansible из командной строки.

Такой вариант используется, как правило, в тех случаях, когда надо что-то проверить, например, работу модуля.
Или просто выполнить какое-то разовое действие, которое не нужно сохранять.

В любом случае, это простой и быстрый способ начать использовать Ansible.

Сначала нужно создать в локальном каталоге инвентарный файл. Назовем его myhosts:
```
[cisco-routers]
192.168.100.1
192.168.100.2
192.168.100.3

[cisco-switches]
192.168.100.100
```

> При подключении к устройствам первый раз, сначала лучше подключиться к ним вручную, чтобы ключи устройств были сохранены локально. В Ansible есть возможность отключить эту первоначальную проверку ключей. В разделе о конфигурационном файле мы посмотрим как это делать (такой вариант может понадобиться, если надо подключаться к большому количеству устройств).

Пример ad-hoc команды:
```
$ ansible cisco-routers -i myhosts -m raw -a "sh ip int br" -u cisco --ask-pass
```

Разберемся с параметрами команды:
* ```cisco-routers``` - группа устройств, к которым нужно применить действия
 * эта группа должна существовать в инвентарном файле
 * это может быть конкретное имя или адрес
 * если нужно указать все хосты из файла, можно использовать значение all или *
 * Ansible поддерживает более сложные варианты указания хостов, с регулярными выражениями и разными шаблонами. Подробнее об этом в [документации](http://docs.ansible.com/ansible/intro_patterns.html)
* ```-i myhosts``` - параметр -i позволяет указать инвентарный файл
* ```-m raw -a "sh ip int br"``` - параметр ```-m raw``` означает, что используется модуль raw
 * этот модуль позволяет отправлять команды в SSH сессии, но при этом не загружает на хост модуль Python. То есть, этот модуль просто отправляет указанную команду как строку и всё
 * плюс модуля raw в том, что он может использоваться для любой системы, которую поддерживает Ansible
 * ```-a "sh ip int br"``` - параметр ```-a``` указывает какую команду отправить
* ```-u cisco``` - подключение выполняется от имени пользователя cisco
* ```--ask-pass``` - параметр который нужно указать, чтобы аутентификация была по паролю, а не по ключам


Результат выполнения будет таким:
```
$ ansible cisco-routers -i myhosts -m raw -a "sh ip int br" -u cisco --ask-pass
```

![ad-hoc-fail](https://raw.githubusercontent.com/natenka/PyNEng/master/images/15_ansible/2_ad-hoc-fail.png)


Ошибка значит, что нужно установить программу sshpass.
Эта особенность возникает только когда используется аутентификацию по паролю.

Установка sshpass:
```
$ sudo apt-get install sshpass
```

Команду надо выполнить повторно:
```
$ ansible cisco-routers -i myhosts -m raw -a "sh ip int br" -u cisco --ask-pass
```

![ad-hoc](https://raw.githubusercontent.com/natenka/PyNEng/master/images/15_ansible/1_ad-hoc.png)



Теперь всё прошло успешно.
Команда выполнилась и отобразился вывод с каждого устройства.

Аналогичным образом можно попробовать выполнять и другие команды и/или на других комбинациях устройств.
