# oswhich
This package allows for cross-platform implementations on-the-go with a very sugary decorator syntax. It works also for classes, its methods and properties. Although, development is still incipient so feel free to open an issue on the bug tracker.

## Examples
```python
from oswhich import linux, macosx, windows, solaris

@linux
def f(x):
    return 2 * x

@macosx
def f(x):
    return x ** 2

@windows
def f(x):
    return x + 2

>>> f(3) # in Linux
6
>>> f(3) # in MacOSx
9
>>> f(3) # in Windows
5
>>> f(3) # in Solaris
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: Sorry, function `f` was not implemented for your platform. 
```

## Advanced usage
You may define your own definition selector. Internally, ``OsWhich`` relies on ``platform.system()`` to select current platform. If ``OsWhich.__init__`` takes a string as parameter, it just compares it with ``platform.system()``'s output. If you pass a ``callable`` to the constructor, you are allowed to do whatever you want, as long as this function follows the signature ``foo(system: str) -> bool``.

```python
from oswhich import OsWhich

mysystem = OsWhich(foo)

@mysystem
def f(x):
    return -x
```
