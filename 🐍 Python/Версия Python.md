___
### Как узнать версию [[Python]] 🐍
Перед началом полезно убедиться, что у нас установлена актуальная версия Python.
###### Способ 1: через модуль [[sys]]
```python
import sys
print(sys.version)
```
```console black:1
3.13.2 | packaged by Anaconda, Inc. | (main, Feb  6 2025, 18:56:02) [GCC 11.2.0]
```
###### Способ 2: через модуль [[platform]]
```python
from platform import python_version
print(python_version())
```
```console black:1
3.13.2
```
###### Python имеет встроенный "манифест" - набор принципов, описывающих идеологию языка. Этот манифест можно вывести с помощью модуля `this`.
```python
import this
```
```console black:1-21
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```