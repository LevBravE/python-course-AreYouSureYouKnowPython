# Часть 2
Так как вы знакомы с основными коллекциями в Python, я хочу познакомить вас с другими интересными структурами данных. Такими как:
- SimpleNamespace
- Deque
- PriorityQueue

### SimpleNamespace
Это достаточно интересная структура данных с атрибутивным доступом к элементам.

```python
from types import SimpleNamespace

some_obj = SimpleNamespace(x=1, y=2, z=3)
# Можно вызывать как атрибуты
print(some_obj.x, some_obj.y, some_obj.z)
# Можно инициализировать новые атрибуты
some_obj.some_attribute = 'value'
print(some_obj.some_attribute)
```
Достаточно интересная вещь. Работает это примерно так:
```python
class MySimpleNamespace:
   def __init__(self, **kwargs):
       for key, value in kwargs.items():
           self.__setattr__(str(key), value)
```
Выглядит просто, правда? На самом деле там “под капотом” все сложнее, но я это написал, чтобы просто передать суть её работы. Использовать это можно точно таким же образом:
```python
some_obj = MySimpleNamespace(x=1, y=2, z=3)
# Можно вызывать как атрибуты
print(some_obj.x, some_obj.y, some_obj.z)
# Можно инициализировать новые атрибуты
some_obj.some_attribute = 'value'
print(some_obj.some_attribute)
```
### Deque
В Python есть стеки. Да-да! Действительно, они там есть. В виде отдельного класса.
Напомню, что такое стек:
Стек - это такая структура данных, которая работает по принципу: последний вошел - первый вышел(LIFO)
Мой пример реализации:

```python
def convert_collection_to_stack(_collection):
   return Stack(*_collection.values()) if isinstance(_collection, dict) else Stack(*_collection)


class Stack:
   def __init__(self, *args):
       self._collection = list(args) if len(args) else []

   # Добавляем элемент в стек.
   def push(self, item):
       self._collection.append(item)

   # Забираем его по принципу: последний вошел - первый вышел(LIFO)
   def pop(self):
       return self._collection.pop() if len(self._collection) else None

   def get_stack_as_list(self):
       return self._collection
```
Вернемся, к встроенному стеку. Давайте импортируем наш класс и применим его.

```python
from collections import deque

d = deque()
for i in range(100): 
    d.append(i)
print(d)
print(d.pop())
```
Это может работать и как очередь:
```python
print(d.popleft())
print(d)
```
### PriorityQueue
В Python присутствует очередь с приоритетом, но адаптированная для многопоточной работы. В зависимости от ваших целей она может либо замедлить, либо ускорить работу вашей программы.
```python
from queue import PriorityQueue

q = PriorityQueue()
for i in ['привет', 'мир', '!']: 
    q.put(i)

while not q.empty():
   print(q.get())
```