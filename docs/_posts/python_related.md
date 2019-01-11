---
title: Python Related
---

`pip`
======

<br>

Basics
------

<br>

+ Checking `pip` version
```bash
pip --version
pip3 --version
```

+ Upgrade using tsinghua.edu source
```bash
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ -U pip
```

<br>

Common Error Handling
------

<br>


### ImportError after pip upgrade

+ Error log
```
Traceback (most recent call last):
  File "/usr/bin/pip3", line 9, in <module>
    from pip import main
ImportError: cannot import name 'main'
```

+ Find which pip you are calling

```
which pip
# Or pip3
which pip3
```

+ Edit the pip file
```
sudo vim /usr/bin/pip
# Or if you are using pip3
sudo vim /usr/bin/pip3
```

+ Change the following lines
```python
import sys
from pip import __main__
if __name__ == '__main__':
     sys.exit(__main__._main())
```