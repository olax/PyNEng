## Цикл for

Цикл for позволяет проходится по элементам последовательности.

Пример шаблона templates/for.txt с использованием цикла:
```
hostname {{ name }}

interface Loopback0
 ip address 10.0.0.{{ id }} 255.255.255.255

{% for vlan, name in vlans.iteritems() %}
vlan {{ vlan }}
 name {{ name }}
{% endfor %}

router ospf 1
 router-id 10.0.0.{{ id }}
 auto-cost reference-bandwidth 10000
{% for networks in ospf %}
 network {{ networks.network }} area {{ networks.area }}
{% endfor %}
```

Файл data_files/for.yml с переменными:
```yml
id: 3
name: R3
vlans:
  10: Marketing
  20: Voice
  30: Management
ospf:
  - network: 10.0.1.0 0.0.0.255
    area: 0
  - network: 10.0.2.0 0.0.0.255
    area: 2
  - network: 10.1.1.0 0.0.0.255
    area: 0
```

В цикле for мы можем проходится и по элементам списка (например, список ospf), так и по словарю (словарь vlans). И, аналогичным образом, по любой последовательности.

> **Note** Элементы словаря не упорядочены. Поэтому, если нужно получить упорядоченные элементы, можно либо использовать отсортированый список кортежей, либо использовать упорядоченный словарь collections.OrderedDict.

Результат выполнения будет таким:
```
$ python cfg_gen.py templates/for.txt data_files/for.yml
hostname R3

interface Loopback0
 ip address 10.0.0.3 255.255.255.255

vlan 10
 name Marketing
vlan 20
 name Voice
vlan 30
 name Management

router ospf 1
 router-id 10.0.0.3
 auto-cost reference-bandwidth 10000
 network 10.0.1.0 0.0.0.255 area 0
 network 10.0.2.0 0.0.0.255 area 2
 network 10.1.1.0 0.0.0.255 area 0
```
