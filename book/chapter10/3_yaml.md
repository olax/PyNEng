##Работа с файлами в формате YAML

YAML (YAML Ain't Markup Language) - еще один текстовый формат для записи данных.

YAML более приятен для восприятия человеком, чем JSON.

###Синтаксис YAML

Как и Python, YAML использует отступы для указания структуры документа.

Но в YAML можно использовать только пробелы и нельзя использовать знаки табуляции.

Еще одна схожесть с Python: комментарии начинаются с символа # и продолжаются до конца строки.

Пройдемся по тому как в YAML записываются различные форматы данных.

####Список

Список может быть записан в одну строку:
```yaml
[switchport mode access, switchport access vlan, switchport nonegotiate, spanning-tree portfast, spanning-tree bpduguard enable]
```

Или каждый элемент списка в своей строке:
```yaml
- switchport mode access
- switchport access vlan
- switchport nonegotiate
- spanning-tree portfast
- spanning-tree bpduguard enable
```

Когда список записан таким блоком, каждая строка должна начинаться с ```- ``` (минуса и пробела). И все строки в списке должны быть на одном уровне отступа.

####Словарь

Словарь также может быть записан в одну строку:
```yaml
{ vlan: 100, name: IT }
```

Или блоком:
```yaml
vlan: 100
name: IT
```

####Строки

Наверняка вы обратили внимание, что строки в YAML не обязательно брать в кавычки. Это удобно и приятно, но иногда всё же следует использовать кавычки. Например, когда в строке используется какой-то специальный символ (специальный для YAML).

Например, такую строку нужно взять в кавычки, чтобы она была корректно воспринята YAML:
```yaml
command: "sh interface | include Queueing strategy:"
```

####Комбинация элементов
Словарь, в котором есть два ключа access и trunk. Значения, которые соответствуют этим ключам - списки команд:
```yaml
access:
- switchport mode access
- switchport access vlan
- switchport nonegotiate
- spanning-tree portfast
- spanning-tree bpduguard enable

trunk:
- switchport trunk encapsulation dot1q
- switchport mode trunk
- switchport trunk native vlan 999
- switchport trunk allowed vlan
```

Список словарей:
```yaml
- BS: 1550
  IT: 791
  id: 11
  name: Liverpool
  to_id: 1
  to_name: LONDON
- BS: 1510
  IT: 793
  id: 12
  name: Bristol
  to_id: 1
  to_name: LONDON
- BS: 1650
  IT: 892
  id: 14
  name: Coventry
  to_id: 2
  to_name: Manchester
```