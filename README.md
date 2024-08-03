# study_buddy

# Steps to initiate django:
1. go to the projects directory in your local system and then RUN the command `ls` in your git bash terminal it will show you all the files in that directory.
2. Run the command `cd Document` to safe all the files in that folder.
3. Run the command `ls` to show the all the lists of the files.
4. Run the command `mkdir data` to make a folder named as data and again run the `ls` command to show all the list of the files.
5. Run the `cd data` command to change the directory and again run the `ls` command to show the list of files.
6. Run the command `git clone https://github.com/Ayeshashabbir01/study_buddy.git` and paste the url of our project to clone the repository.
7. Run the command `ls` to show the repository.
8. Run the command `cd study_buddy/` to go to the study_buddy .
9. Run the command `code .` to open in the visual studio code.
10. Run the command `python -m venv myenv` to create the virtual environment in the name of myenv.
11. Run the command `source myenv/Scripts/activate` to activate the envionment.
12. Run the command `python -m django version` to check the version of the django .
13. Run the command `pip install django` to install the django in the environment and again check the version of django.
14. Run the command ` django-admin startproject core ` and create name core project in the studdy_buddy repository.
15. Run the command `cd core` to go to the core and also run the ls command to show the all files in the core folder.
16. Run the command `python manage.py startapp base` to create the new application in the django project.
17. Run the command `python manage.py runserver` to run the server application.
18. Run the command `cd../` to one back to the folder.And run the `ls -a ` command to show all the files including the .gitignore.
19. Run the command `git add .`to add all changes in the current directories. And `git commit`to commit the message "Steps to initiate django".
20. Run the command `git push` to push to the github.

# `API:`
>1. we will send a GET request to the django View the View will which will send a request to the database, our database will send that data back to the view, the view will serialize that data and send it back to the client.

>2. when we are sending the data, we will send the form data from the frontEnd.

`Virtual Environment`

```py
pip install virtualenv
virtualenv venv
source env/Scripts/activate
```
To activate the virtual environment.

` Building base app`
```py
 python manage.py runserver
 python manage.py startapp base
 ```
configure your base app in the settings.py.

```py 
# settings.py
INSTALLED_APPS = [
 # ......
     'base.apps.BaseConfig',
]
```

2. Go to the app and create the urls file to handle all the route just for these app.
 
```py
 3.#// studybud/base/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name="home"),
    path('room/', views.room, name="room"),
]
```
so we have two views and two urls.

6. 
```py
# /studybud/urls.py
urlpatterns = [
    # .....
    path('', include('base.urls')),
]
```

# Templates:
1.create templates,and update the django that we have a templates .
```py 
 #settings.py
 TEMPLATES = [
    BASE_DIR / 'templates'
 ],
 ```
2. create four files in these templates `home.html`,`room.html`,`main.html`, `navbar.html`.

```py
# home.html
{% extends "main.html" %}

 {% block content  %} 

 <h1>Home Template</h1>

<div>
    <div>
        {% for room in rooms %}
            <div>
                <h5>{{room.id}} -- <a href="{% url 'room' room.id %}">{{room.name}}</a></h5>
            </div>
            
        {% endfor %}
    </div>
    
</div>

 {% endblock content %}
 ```
```py
# room.html
{% include 'navbar.html' %}

{% block content %}

<h1>{{room.name}}</h1>

{% endblock content %}
```

```py 
# navbar.html
<a href="/">
    <h1>LOGO</h1>
</a>

<hr>
```

```py
#main.html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <title>StudyBud</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!--link rel='stylesheet' type='text/css' media='screen' href='main.css'-->
    
</head>
<body>
    {% include "navbar.html" %}
    
    {% block content %}
    
    {% endblock content %}
</body>
</html>
```


    
