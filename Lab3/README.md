# **Лабораторна робота №3**
---
## Послідовність виконання лабораторної роботи:
#### 1. Створив папку ***Lab3*** у власному репозиторію. Перейшовши у папку проініціалізував середовище pipenv та встановив необхідні пакети за допомогою команд:
```text
sudo pipenv --python 3.8
sudo pipenv install django
```
#### 2. За допомогою `Django Framework` створив заготовку (template) власного проекту `my_site`. Використовуючи команду `sudo pipenv run django-admin startproject my_site`. 
Для зручності виніс всі створені файли на один рівень вище щоб структура проекту була такою як показано нижче:
```text
Lab3/
├── my_site/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py
```
За допомогою команд:
```sh
sudo mv my_site/my_site/* my_site/
sudo mv my_site/manage.py ./
sudo rmdir my_site/my_site
```
#### 3. Запускаю `Django` сервер. За допомогою команди `sudo pipenv run python manage.py runserver` та перейшов за посиланням яке вивелось у консолі.
Виконання команди в консолі:
```text
23:23:50 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run python manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
November 05, 2021 - 21:24:03
Django version 3.2.9, using settings 'my_site.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```
#### 4. Після того як все запустилось успішно і стартова сторінка `Django` відображається коректно, зупинив сервер виконавши переривання `Ctrl+C`. Створив коміт із базовим темплейтом сайту. А також ознайомився із функціоналом `Django Framework`.

#### 5. Далі створив темплейт свого додатку у якому буде описано всі web сторінки мого сайту `main`. За допомогою команди `sudo pipenv run python manage.py startapp main`. Також створив коміт із новоствореними файлами темплейту додатка.

#### 6. Cтворbd папку `main/templates/`, а також у даній папці файл `main.html`. Також у папці додатку створив ще один файл `main/urls.py`. Зробив коміт із даними файлами.

#### 7. Після створення додатку вказав `Django frameworks` його назву та де шукати веб сторінки. Це здійснюється у файлі `my_site/settings.py` у змінній `INSTALLED_APPS`, а також вніс зміни у файл `my_site/urls.py`.
Доданий вміст до файлу `my_site/settings.py`:
```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'main'
]
```
Доданий вміст до файлу `my_site/urls.py`:
```python
"""my_site URL Configuration

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/3.2/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),
]
```
#### 8. Далі переходжу до мого додатку та буду виконувати дії над WEB сторінками. Для цього: створив сторінки двох типів - перша буде зчитуватись з .html темплейта. друга сторінка буде просто повертати відповідь у форматі JSON.
Вміст файла `main/views.py`:
```py
from django.shortcuts import render
from django.http import JsonResponse
import os
from datetime import datetime

def main(request):
    return render(request, 'main.html', {'parameter': "test"})

def health(request):
    response = {'date': 'test1', 'current_page': "test2", 'server_info': "test3", 'client_info': "test4"}
    return JsonResponse(response)
```
#### 9. Щоб поєднати функції із реальними URL шляхами за якими будуть доступні наші веб сторінки заповнив файл `main/urls.py` згідно зразка. Як можна зрозуміти з коду є два URL посидання:
* головна сторінка яка буде опрацьовуватись функцією main;
* сторінка health/ яка буде опрацьована функцією health;

Доданий вміст до файлу `main/urls.py`:
```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.main, name='main'),
    path('health/', views.health, name='health')
]
```

#### 10. Запустив сервер та переконався що сторінки доступні. Виконайте коміт робочого `Django` сайту.
Виконання команди:
```text
01:00:36 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run python manage.py runserver
[sudo] password for pavlovulchak: 
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
November 05, 2021 - 23:18:35
Django version 3.2.9, using settings 'my_site.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
[05/Nov/2021 23:18:46] "GET / HTTP/1.1" 200 158
Not Found: /favicon.ico
^C01:19:14 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ 
```

#### 11. Роль моніторингу буде здійснювати файл `monitoring.py` який за допомогою бібліотеки `requests` буде опитувати сторінку `health`. Встановив дану бібліотеку командою `sudo pipenv install requests`

#### 12. Як видно із заготовленої функції health() відповідь формується як Пайтон словник і далі обробляється функцією JsonResponse(). У даній заготовці вже є сформована відповідь що містить декілька полів, наприклад date та current_page. Відкрити сторінку /health у браузері і плогін JSON коректно відобразить дані.

#### 13. Здача/захист лабораторної:
1. ##### Модифікував функцію health так щоб у відповіді були: згенерована на сервері дата, URL сторінки моніторингу, інформація про сервер на якому запущений сайт та інформація про клієнта який робить запит до сервера.
    
    Вміст функції `health()` з файлика `main/views.py`:  
    ```python
    def health(request):
        response = {
        'date': datetime.now().strftime("Time: %H:%M:%S   Data: %Y/%M/%D"),
        'current_page': request.get_host() + request.get_full_path(),
        'server_info': "Name_OS: " + os.uname().sysname + ";   " +
                       "Name_Node: " + os.uname().nodename + ";   " +
                       "Release: " + os.uname().release + ";   " +
                       "Version: " + os.uname().version + ";   " +
                       "Indentificator:" + os.uname().machine,
        'client_info': "Browser: " + request.META['HTTP_USER_AGENT'] + ";   " + "IP: " + request.META['REMOTE_ADDR']
        }
        return JsonResponse(response)
    ```
2. ##### Дописав функціонал який буде виводити повідомлення про недоступність сайту у випадку якщо WEB сторінка недоступна.
    Вміст створеного файлика `monitoring.py`: 
    ```python
    import requests
    import json
    import logging
    
    logging.basicConfig(
        filename="server.log",
        filemode='a',
        level=logging.INFO,
        format='{levelname} {asctime} {name} : {message}',
        style='{'
    )
    log = logging.getLogger(__name__)
    
    
    def main(url):
        try:
        	r = requests.get(url)
        except Exception as x:
        	logging.error("Сервер недоступний.")
        else:
        	data = json.loads(r.content)
        	logging.info("Сервер доступний. Час на сервері: %s", data['date'])
        	logging.info("Запитувана сторінка: : %s", data['current_page'])
        	logging.info("Відповідь сервера місти наступні поля:")
        	for key in data.keys():
        	    logging.info("Ключ: %s, Значення: %s", key, data[key])

    if __name__ == '__main__':
        main("http://localhost:8000/health")
    ```
    Запуск в консолі:
    ```text
    23:35:51 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run python monitoring.py
    [sudo] password for pavlovulchak: 
    23:36:28 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    ERROR 2021-11-06 23:35:02,349 root : Сервер недоступний.
    INFO 2021-11-06 23:36:28,253 root : Сервер доступний. Час на сервері: Time: 21:36:28   Data: 2021/36/11/06/21
    INFO 2021-11-06 23:36:28,253 root : Запитувана сторінка: : localhost:8000/health/
    INFO 2021-11-06 23:36:28,253 root : Відповідь сервера місти наступні поля:
    INFO 2021-11-06 23:36:28,253 root : Ключ: date, Значення: Time: 21:36:28   Data: 2021/36/11/06/21
    INFO 2021-11-06 23:36:28,253 root : Ключ: current_page, Значення: localhost:8000/health/
    INFO 2021-11-06 23:36:28,253 root : Ключ: server_info, Значення: Name_OS: Linux;   Name_Node: pavlovulchak-vbox;   Release: 5.11.0-38-generic;   Version: #42~20.04.1-Ubuntu SMP Tue Sep 28 20:41:07 UTC 2021;   Indentificator:x86_64
    INFO 2021-11-06 23:36:28,253 root : Ключ: client_info, Значення: Browser: python-requests/2.26.0;   IP: 127.0.0.1
    23:40:39 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ 
    ```
3. ##### Після запуску моніторингу запит йде лише один раз після чого програма закінчується я  зробив так щоб дана програма запускалась раз в хвилину та працювала в бекграунді.
   Додані елементи до файлика `monitoring.py`: 
    ```python
    if __name__ == '__main__':
        while(True):
            main("http://localhost:8000/health")
            time.sleep(60)
    ```
    Запуск в терміналі:
    ```text
    23:52:36 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    cat: server.log: No such file or directory
    23:53:34 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run python monitoring.py &
    [1] 5194
    23:53:50 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    ERROR 2021-11-06 23:53:51,422 root : Сервер недоступний.
    23:54:01 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run python manage.py runserver
    Watching for file changes with StatReloader
    Performing system checks...
    
    System check identified no issues (0 silenced).
    
    You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.
    November 06, 2021 - 21:54:54
    Django version 3.2.9, using settings 'my_site.settings'
    Starting development server at http://127.0.0.1:8000/
    Quit the server with CONTROL-C.
    [06/Nov/2021 21:55:51] "GET /health HTTP/1.1" 301 0
    [06/Nov/2021 21:55:51] "GET /health/ HTTP/1.1" 200 344
    23:56:11 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    ERROR 2021-11-06 23:53:51,422 root : Сервер недоступний.
    ERROR 2021-11-06 23:54:51,482 root : Сервер недоступний.
    INFO 2021-11-06 23:55:51,559 root : Сервер доступний. Час на сервері: Time: 21:55:51   Data: 2021/55/11/06/21
    INFO 2021-11-06 23:55:51,560 root : Запитувана сторінка: : localhost:8000/health/
    INFO 2021-11-06 23:55:51,561 root : Відповідь сервера місти наступні поля:
    INFO 2021-11-06 23:55:51,561 root : Ключ: date, Значення: Time: 21:55:51   Data: 2021/55/11/06/21
    INFO 2021-11-06 23:55:51,561 root : Ключ: current_page, Значення: localhost:8000/health/
    INFO 2021-11-06 23:55:51,561 root : Ключ: server_info, Значення: Name_OS: Linux;   Name_Node: pavlovulchak-vbox;   Release: 5.11.0-38-generic;   Version: #42~20.04.1-Ubuntu SMP Tue Sep 28 20:41:07 UTC 2021;   Indentificator:x86_64
    INFO 2021-11-06 23:55:51,561 root : Ключ: client_info, Значення: Browser: python-requests/2.26.0;   IP: 127.0.0.1
    23:56:14 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs
    [1]+  Running                 sudo pipenv run python monitoring.py &
    23:56:36 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs -p
    5194
    23:57:52 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo kill 5194
    [1]+  Terminated              sudo pipenv run python monitoring.py
    23:57:57 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs -p
    23:58:02 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ 
    ```
4. ##### Cпростив роботу з пайтон середовищем через швидкий виклик довгих команд, для цього звернув увагу на секцію `scripts` у `Pipfile`. Таксамо як викладач додав аліас на запуск сервера який тепер буде стартувати за командою `pipenv run server`. Зрообив аліас на запус моніторингу командою `pipenv run monitoring`.
    Секція `script` в файлику `Pipfile`:
    ```text
    [scripts]
    server = "python manage.py runserver 0.0.0.0:8000"
    monitoring = "python monitoring.py"
    ```
    Запуск в терміналі:
    ```text
    00:13:35 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run monitoring &
    [1] 5534
    00:13:37 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs
    [1]+  Running                 sudo pipenv run monitoring &
    00:13:55 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    ERROR 2021-11-07 00:13:38,851 root : Сервер недоступний.
    00:14:09 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo pipenv run server
    Watching for file changes with StatReloader
    Performing system checks...
    
    System check identified no issues (0 silenced).
    
    You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
    Run 'python manage.py migrate' to apply them.
    November 06, 2021 - 22:14:18
    Django version 3.2.9, using settings 'my_site.settings'
    Starting development server at http://0.0.0.0:8000/
    Quit the server with CONTROL-C.
    [06/Nov/2021 22:14:38] "GET /health HTTP/1.1" 301 0
    [06/Nov/2021 22:14:38] "GET /health/ HTTP/1.1" 200 344
    00:14:43 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ cat server.log
    ERROR 2021-11-07 00:13:38,851 root : Сервер недоступний.
    INFO 2021-11-07 00:14:38,918 root : Сервер доступний. Час на сервері: Time: 22:14:38   Data: 2021/14/11/06/21
    INFO 2021-11-07 00:14:38,919 root : Запитувана сторінка: : localhost:8000/health/
    INFO 2021-11-07 00:14:38,919 root : Відповідь сервера місти наступні поля:
    INFO 2021-11-07 00:14:38,919 root : Ключ: date, Значення: Time: 22:14:38   Data: 2021/14/11/06/21
    INFO 2021-11-07 00:14:38,919 root : Ключ: current_page, Значення: localhost:8000/health/
    INFO 2021-11-07 00:14:38,919 root : Ключ: server_info, Значення: Name_OS: Linux;   Name_Node: pavlovulchak-vbox;   Release: 5.11.0-38-generic;   Version: #42~20.04.1-Ubuntu SMP Tue Sep 28 20:41:07 UTC 2021;   Indentificator:x86_64
    INFO 2021-11-07 00:14:38,919 root : Ключ: client_info, Значення: Browser: python-requests/2.26.0;   IP: 127.0.0.1
    00:14:47 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs -p
    5534
    00:14:57 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ sudo kill 5534
    [1]+  Terminated              sudo pipenv run monitoring
    00:15:08 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ jobs -p
    00:15:12 pavlovulchak ~/TPIS/Pavlo_Vulchak_IK_31/Lab3 (master) $ 
    ```
#### 14. Запустив сервер та переконався що головна сторінка відображається. Перейшов у інше вікно консолі та запустив програму моніторингу. Закомітив файл логів server.logs до репозиторію.
![task_14](https://github.com/PavloVulchak/Pavlo_Vulchak_IK_31/blob/master/Lab3/picture/task_14.png) 

#### 15. Після успішного виконання роботи відредагував свій персональний `README.md` у цьому репозиторію. Додав в таблицю яка ставить у відповідність номер лабораторної роботи та URL посилання на папку з виконаною роботою у моєму персональному репозиторію. Створив пул-реквест до основного репозиторію.
