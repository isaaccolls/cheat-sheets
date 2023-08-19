- [zen](#zen)
- [simple http server](#simple-http-server)
- [install](#install)
  - [upgrade](#upgrade)
- [pip](#pip)
- [virtual environment](#virtual-environment)
- [list](#list)

# zen

- show: `import this`

# simple http server

- python 2: `python -m SimpleHTTPServer 8000`
- python 3: `python3 -m http.server 8000`

# install

## upgrade

1. `sudo apt update -y`
2. `sudo apt install python3.8`
3. `sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1`
4. `sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 2`
5. `sudo update-alternatives --config python3`

# pip

- install: `sudo apt install python3-venv python3-pip`
- use: `pip3 install simplejson`
- installed packages: `pip3 freeze`
- create _requirements.txt_: `pip3 freeze > requirements.txt`
- install from _requirements.txt_: `pip3 install -r requirements.txt`
- uninstall: `pip3 uninstall [package-name]`
- version`pip3 --version`

# virtual environment

- install: `pip3 install virtualenv`
- Create Virtual Environment:
  - Find the Python 3 binary file location using which command: `which python3`
- create virtual environment: `python3 -m venv [420]` or `virtualenv -p /usr/bin/python3 [420]`
- activate: `source 420/bin/activate`
  - Check the correct Python version with: `python -V`
- Any package that you install using pip is now placed in the virtual environments project folder: `pip3 install <module>`
- Deactivate virtualenv Environment: `deactivate`

# list

- create a new list

```python
xs = [1,"x",3.1415]
ys = list(xs)
```

- indexing

```python
xs = [1,2,3]
xs[0] #1
xs[1] #2
xs[-1] #3
xs[-2] #2
```

- lenght of list

```python
xs = [1,2,1,2]
lenght = len(xs)
# lentgth = 4
```

- assignment

```python
xs = [1,1,1]
xs[-1] = 2
xs[0] = 2
# xs=[2,1,2]
```

- append

```python
xs = [1,1]
ys = [3,3]
xs.append(2)
# xs = [1,1,2]
xs.append(ys)
# xs = [1,1,2,[3,3]]
```

- extend

```python
xs = [1,2]
ys = [3,4]
xs.extend(ys)
# xs = [1,2,3,4]
```

- insert

```python
xs = [1,3]
xs.insert(1,2)
# xs = [1,2,3]
```

- remove

```python
xs = [1,2,3]
xs.remove(2)
# xs = [1,3]
```

- slicing

```python
start = 5
stop = 15
step = 2
xs = list(range(20))
print(xs[start:stop:step])
# [5,7,9,11,13]
```

- min/max

```python
xs = [1,2,3]
m = max(xs)
# m = 3
```

- sum

```python
xs = [1,1,-2]
s = sum(xs)
# s = 0
```

- sort

```python
xs = [3,1,4,2]
xs.sort()
# xs = [1,2,3,4]
```
