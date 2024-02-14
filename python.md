- [zen](#zen)
- [simple http server](#simple-http-server)
- [virtual environment](#virtual-environment)
- [list](#list)

# zen

- show: `import this`

# simple http server

- python 2: `python -m SimpleHTTPServer 8000`
- python 3: `python3 -m http.server 8000`

# virtual environment

- install: `sudo apt install python3-venv`
- manage project
  - create a directory project and access it: `mkdir my_project` and `cd my_project`
  - create a virtual environment: `python3 -m venv venv`
  - activate the virtual environment: `source venv/bin/activate`
  - run script with: `python hello_world.py`
  - exit the virtual environment: `deactivate`
- manage packages
  - install some package: `pip install colorama`
  - uninstall: `pip3 uninstall [package-name]`
  - show installed packages: `pip3 freeze`
  - create _requirements.txt_: `pip3 freeze > requirements.txt`
  - install from _requirements.txt_: `pip3 install -r requirements.txt`

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
