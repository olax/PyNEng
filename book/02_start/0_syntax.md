##Синтаксис Python

Первое, что, как правило, бросается в глаза, если говорить о синтаксисе Python, это то, что отступы имеют значение:
* они определяют какие выражения попадают в блок кода
* когда блок кода заканчивается

Пример кода Python:
```python
a = 10
b = 5

if a > b:
    print "A больше B"
    print "Тут можно выполнить ещё что-то"
else:
    print "B больше или равно A"
    print "Продолжаем тут же"

print "The End"
```

Несмотря на то, что еще не рассматривалась конструкция if/else, всё должно быть понятно.

Python понимает какие строки относятся к if на основе отступов.
Выполнение части ```if a > b``` заканчивается, когда встречается строка с тем же отступом, что и сама строка ```if a > b```.

Аналогично с блоком else.

Вторая особенность Python: после некоторых выражений должно идти двоеточие (например, после if a > b или после else).

Несколько правил и рекомендаций:
* В качестве отступов могут использоваться Tab или пробелы. 
  * лучше использовать пробелы
    * а точнее, настроить редактор так, чтобы Tab был равен 4 пробелам (тогда, при использовании Tab, будут ставиться 4 пробела)
* Количество пробелов должно быть одинаковым в одном блоке.
  * лучше чтобы количество пробелов было одинаковым во всем коде
  * популярный вариант использовать 2-4 пробела (в курсе используются 4 пробела)

> **Note** Для того чтобы проблем с отступами не было, надо сразу настроить редактор таким образом, чтобы отступы делались автоматически.


Еще одна особенность приведенного примера кода: пустые строки.
Таким образом код форматируется, чтобы его было проще читать.

Остальные особенности синтаксиса будут показаны в процессе знакомства с структурами данных в Python.

### Комментарии

При написании кода, часто нужно написать комментарий.
Например, чтобы описать особенности работы кода.

Комментарии в Python могут быть однострочными:
```python
#Очень важный комментарий
a = 10
b = 5 #Очень нужный комментарий
```
Однострочные комментарии начинаются со знака #.

Обратите внимание, что коментарий может быть и в строке где находится код, и сам по себе.

При необходимости написать несколько строк с комментариями, чтобы не ставить перед каждой решетку, можно сделать многострочный комментарий:
```python
"""Очень важный
и длинный комментарий
"""
a = 10
b = 5
```

Комментарии могут использоваться как для того, чтобы комментировать, что происходит в коде, так и для того, чтобы закомментировать временно какое-то выражение.
