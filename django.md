- [django](#django)
  - [migrations](#migrations)
  - [django admin](#django-admin)
  - [create user](#create-user)
- [django rest framework](#django-rest-framework)
  - [install](#install)
  - [work with token](#work-with-token)
  - [cors](#cors)

# django

- install:`pip install Django`
- create project: `django-admin startproject [name] .`
- run project: `python3 manage.py runserver`
- create app: `django-admin startapp [name]`

## migrations

- migrate: `python3 manage.py migrate`
- add the app on **installed_apps** inside of settings.py

```python
python3 manage.py makemigrations
python3 manage.py migrate
```

## django admin

- go to <http://127.0.0.1:8000/admin/login/?next=/admin/>

## create user

- run: `python3 manage.py createsuperuser`

# django rest framework

## install

1. run `pip install djangorestframework`
2. add '**rest_framework**' on **installed_apps** inside of _settings.py_
3. do the migrations

## work with token

1. add '**rest_framework.authtoken**' on **installed_apps** inside of settings.py
2. migrate: `python3 manage.py migrate`
3. go to _admin_ module and generate tokens
4. optional, add on settings.py:

```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': (
        'rest_framework.permissions.IsAuthenticated',
    )
}
```

## cors

- install: `pip install django-cors-headers`
