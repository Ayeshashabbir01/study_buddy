# study_buddy

# `Steps to initiate django:`
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

 Go to the app and create the urls file to handle all the route just for these app.
 
```py
 #// studybud/base/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name="home"),
    path('room/', views.room, name="room"),
]
```
so we have two views and two urls.


```py
# /studybud/urls.py
urlpatterns = [
    # .....
    path('', include('base.urls')),
]
```

# `Templates:`
1. create templates,and update the django that we have a templates .
```py 
 # studybud/settings.py/TEMPLATES
 TEMPLATES = [
    BASE_DIR / 'templates'
 ],
 ```
2. create four files in these templates folder `home.html`,`room.html`,`main.html`, `navbar.html`.

```py
#// studybud/templates/home.html
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
# //studybud/templates/room.html
{% include 'navbar.html' %}

{% block content %}

<h1>{{room.name}}</h1>

{% endblock content %}
```
In navbar.html, we can use different tags to create different styles.
```py 
# // studybud/templates/navbar.html
<a href="/">
    <h1>LOGO</h1>
</a>

<hr>
```
In main.html, we can encapsulates all the templates in our projects.

```py
# // studybud/templates/main.html
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
To organize our project, create a `templates` folder inside the `ourapp` directory. Inside `templates`, create a `base` subfolder. Move `home.html` and `room.html` into the `base` subfolder. This structure separates specific templates from those used throughout the app.

```py
#// studybud/base/views.py
from django.shortcuts import render
rooms = [
    {'id': 1, 'name': 'lets learn python!'},
    {'id': 2, 'name': 'Design with me.'},
    {'id': 3, 'name': 'Frontend developer.'},
]

def home(request):
    context = {'rooms': rooms}
    return render(request, 'base/home.html', context)

def room(request,pk):
    room = None
    for i in rooms:
        if i['id'] == int(pk):
            room = i
    context = {'room': room}
    return render(request, 'base/room.html', context)
```

```py
# // studybud/base/urls.py
urlpatterns = [
    path('', views.home, name="home"),
    path('room/<str:pk>/', views.room, name="room"),
]
```
In home.html we can add the link here. to show the room id and its name.
```py 
# studybud/templates/main.html
{% extends "main.html" %}

 {% block content  %} 

 <h1>Home Template</h1>

<div>
    <div>
        {% for room in rooms %}
            <div>
             # adding the link here,
  <h5>{{room.id}} -- <a href="{% url 'room' room.id %}">{{room.name}}</a></h5>
               
            </div>
            
        {% endfor %}
    </div>
    
</div>

 {% endblock content %}
```
```py 
#//  studybud/base/views.py
def room(request, pk):
    room = None
    for i in rooms:
        if i['id'] == int(pk):
            room = i
    context = {'room': room}
    return render(request, 'base/room.html', context)
```

```py
# //studybud/templates/base/room.html
{% include 'navbar.html' %}

{% block content %}

<h1>{{room.name}}</h1>

{% endblock content %}

```
# `Database And Admin Panel:`
```py 
# Steps to create database:
1. python manage.py  make migrations
2. python manage.py migrate
3. python manage.py createsuperuser
4. python manage.py runserver
```
go to the admin panel.


# `Modelling`
In modelling , defining the structure of our database tables using Python classes. Each class represents a database table, and each attribute of the class represents a column in that table. This allows you to interact with your database using Python code .
so, we will model our data in `models.py`.
```py 
# create room in the model.py
from django.db import models

# Create your models here.
class Room(models.Model):
    # host 
    # topic 
    name = models.CharField(max_length=200)
    description = models.TextField(null=True,blank=True)
    # participants 
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)

    def _str_(self):
        return self.name 
```
now we have to migrate our database and Register that room model to the admin.py.
```py
python manage.py migrate
python manage.py runserver
```
```py 
# register the model in admin.py
from django.contrib import admin
# Register your models here.
from .models import Room
admin.site.register(Room)
```
`Now add a room from admin panel`

```py
Steps:
1. Make a model
2. Register the model in the admin.py
3. migrate the database
4. run the server
5. add room in the room model from admin panel.
```
# `Now Adding more Models`
  Each model represents different data, like users, posts, or comments. so, we can add more models to make the code easier to maintain and update easily.
```py
# models.py
from django.db import models
from django.contrib.auth.models import User

# Create your models here.

class Topic(models.Model):
    name = models.CharField(max_length=200)

    def __str__(self):
        return self.name 

class Room(models.Model):
    host  = models.ForeignKey(User, on_delete=models.SET_NULL,null=True)
    topic = models.ForeignKey(Topic, on_delete=models.SET_NULL,null=True)
    name = models.CharField(max_length=200)
    description = models.TextField(null=True,blank=True)
    # participants 
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name 
    

class Message(models.Model):
    user = models.ForeignKey(User,on_delete=models.CASCADE)
    room = models.ForeignKey(Room, on_delete=models.CASCADE)
    body = models.TextField()
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.body[0:50]
```
now we have to migrate our database and Register that model to the admin.py,
```py
 python manage.py makemigrations
 python manage.py migrate
```
when we can registering our model,this makes it easy to add, edit, and delete data directly from the admin panel.
```py
# admin.py
from django.contrib import admin

# Register your models here.

from .models import Room ,Topic , Message

admin.site.register(Room)

admin.site.register(Topic)

admin.site.register(Message)
```
# `CRUD`

CRUD stands for Create, Read, Update, and Delete, which are the four basic operations for managing data in a database.
1. we can create the `room_form.html` file inside the base app firstly we can input to the `submit button` and create a room using function in views.py.
```py
# studybud/base/room_forms.html
{% extends 'main.html' %}

{% block content %}
  <div>
    <form method="POST" action="">
      {% csrf_token %}
      {{form.as_p}}
      <input type="submit" value="Submit" />
    </form>
  </div>
{% endblock content %}
```

2. create python file `forms.py` ,import model Room and access all the fileds of that model.
```py
#studybud/base/forms.py
from django.forms import ModelForm
from .models import Room

class RoomForm(ModelForm):
    class Meta:
        model = Room
        fields = '__all__'

```
```py
#studybud/base/delete.html
{% extends 'main.html' %}

{% block content %}
    <form method="POST" action="">
        {% csrf_token %}
        <p>Are you sure you want to delete "{{ obj }}"?</p>
        <a href="{{ request.META.HTTP_REFERER }}">Go Back</a>
        <input type="submit" value="Confirm" />
    </form>
{% endblock content %}
```
3. In views.py we can create ,update and delete the room.
```py
#studybud/base/views.py
from django.shortcuts import render,redirect
from .models import Room,Topic
from .forms import RoomForm
from django.db.models import Q
#rooms = [
#    {'id': 1, 'name': 'lets learn python!'},
#    {'id': 2, 'name': 'Design with me.'},
#    {'id': 3, 'name': 'Frontend developer.'},
#]

def home(request):
    q = request.GET.get('q') if request.GET.get('q') is not None else ''

    rooms = Room.objects.filter(
        Q(topic__name__icontains=q) |
        Q(name__icontains=q)|
        Q(description__icontains=q)
        )
    topics= Topic.objects.all()
    room_count = rooms.count()
    context = {'rooms': rooms,'topics':topics ,'room_count':room_count}
    return render(request, 'base/home.html', context)

def room(request,pk):
    room = Room.objects.get(id=pk)
    context = {'room': room}
    return render(request, 'base/room.html', context)

def createRoom(request):
    form=RoomForm()
    if request.method == 'POST': 
        form = RoomForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('home')  
    context = {"form":form}
    return render(request, 'base/room_form.html', context)


def updateRoom (request, pk):
    room =Room.objects.get(id=pk)
    form = RoomForm(instance=room)

    if request.method == 'POST':
        form = RoomForm(request.POST,instance=room)
        if form.is_valid():
            form.save()
            return redirect('home') 
        
    context = {'form': form}
    return render(request, 'base/room_form.html', context)
     

def deleteRoom(request, pk):
     room =Room.objects.get(id=pk)
     if request.method == 'POST':
        room.delete()
        return redirect('home')
     return render(request, 'base/delete.html', {'obj': room})
```
```py
#studybud/base/url.py
from django.urls import path
from.import views
urlpatterns = [
    
    
    path("",views.home, name="home"),
    path('room/<str:pk>/',views.room,name="room"),
    path('create-room/', views.createRoom, name='create-room'),
    path('update-room/<str:pk>', views.updateRoom, name='update-room'),
    path('delete-room/<str:pk>', views.deleteRoom, name='delete-room'),


]
```
Each model in models.py represents a different entity in our application. For example:
Topic represents a discussion topic.
Room represents a chat room or discussion room.
Message represents a message posted in a room.
Thats why we create different models for different purpose.

```py
# studybud/base/models.py
from django.db import models
from django.contrib.auth.models import User

# Create your models here.

class Topic(models.Model):
    name = models.CharField(max_length=200)

    def __str__(self):
        return self.name


class Room(models.Model):
    host = models.ForeignKey(User, on_delete=models.SET_NULL, null=True)
    topic = models.ForeignKey(Topic, on_delete=models.SET_NULL, null=True)
    name = models.CharField(max_length=200)
    description = models.TextField(null=True, blank=True)
    # participants 
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['-updated', '-created']

    def __str__(self):
        return self.name  


class Message(models.Model):
    user = models.ForeignKey(User, on_delete=models.CASCADE)
    room = models.ForeignKey(Room, on_delete=models.CASCADE)
    body = models.TextField()
    updated = models.DateTimeField(auto_now=True)
    created = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.body[0:50]
```
# `Search`
A search form has a text box and a submit button. When we enter our search words and press the button, the website processes our request and displays the results.
In search we can search the room manually by its author name, text, name of topic. 
```py
# studybud/templates/base/home.html
{% extends "main.html" %}
 {% block content  %} 

 <style>
    .home-container {
        display: grid;
        grid-template-columns: 1fr 3fr;
    }
 </style>
    

<div class='home-container'>
    <div>
        <h3>Browse Topics</h3>
        <hr>
        <div>
            <a href="{% url 'home'%}">All</a>
        </div>

        {% for topic in topics %}
        <div>
            <a href="{% url 'home' %}?q={{topic.name}}">{{topic.name}}</a>
        </div>
        {% endfor %}
    </div>
    <div>
        <h5>{{room_count}} rooms available</h5>
        <a href="{% url 'create-room' %}">Create Room</a>

    <div>
        {% for room in rooms %}
            <div>
                <a href="{% url 'update-room' room.id %}">Edit</a>
                <a href="{% url 'delete-room' room.id %}">Delete</a>
                <span>@{{room.host.username}}</span>
                <h5> -- <a href="{% url 'room' room.id %}">{{ room.name }}</a></h5>
           <small>{{room.topic.name}}</small>
                <hr>
            </div>
        {% endfor %}
    </div>
    </div>
    
    
</div>

 {% endblock content %}
 ```

 Users can manage discussion rooms by searching for rooms based on topics, names, or descriptions, as well as creating, updating, and deleting rooms. 
 ```py
 # studybud/base/views.py
 from django.shortcuts import render,redirect
from .models import Room,Topic
from .forms import RoomForm
from django.db.models import Q
#rooms = [
#    {'id': 1, 'name': 'lets learn python!'},
#    {'id': 2, 'name': 'Design with me.'},
#    {'id': 3, 'name': 'Frontend developer.'},
#]

def home(request):
    q = request.GET.get('q') if request.GET.get('q') is not None else ''

    rooms = Room.objects.filter(
        Q(topic__name__icontains=q) |
        Q(name__icontains=q)|
        Q(description__icontains=q)
        )
    topics= Topic.objects.all()
    room_count = rooms.count()
    context = {'rooms': rooms,'topics':topics ,'room_count':room_count}
    return render(request, 'base/home.html', context)

def room(request,pk):
    room = Room.objects.get(id=pk)
    context = {'room': room}
    return render(request, 'base/room.html', context)

def createRoom(request):
    form=RoomForm()
    if request.method == 'POST': 
        form = RoomForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('home')  
    context = {"form":form}
    return render(request, 'base/room_form.html', context)


def updateRoom (request, pk):
    room =Room.objects.get(id=pk)
    form = RoomForm(instance=room)

    if request.method == 'POST':
        form = RoomForm(request.POST,instance=room)
        if form.is_valid():
            form.save()
            return redirect('home') 
        
    context = {'form': form}
    return render(request, 'base/room_form.html', context)
     

def deleteRoom(request, pk):
     room =Room.objects.get(id=pk)
     if request.method == 'POST':
        room.delete()
        return redirect('home')
     return render(request, 'base/delete.html', {'obj': room})
```
we can search  and count the  numbers of rooms by using GET method.
```py
# studybud/templates/navbar.html
<a href="/">
    <h1>LOGO</h1>
</a>
<form method="GET" action="{% url 'home' %}">
    <input type="text" name="q" placeholder="Search Rooms..." />
    <button type="submit">Search</button>
</form>


<hr>
```
# `User Login/logout`

`Login`
A form where users enter their username and password to access the website.
`Logout`
A button that users click to end their session and log out of the website.

 we can create the file `login_register.html` and register the user.
 ```py
# studybud/templates/base/login_register.html
{% extends 'main.html' %}
{% block content %}
<div>
<form method="POST" action="">
{% csrf_token %}
<label>Username: </label>
<input type="text" name="username" placeholder="Enter Username" />
<br>
<label>Password: </label>
<input type="password" name="password" placeholder="Enter Password" />
<br>
<input type="submit" value="Login" />
</form>
</div>
{% endblock content %}
```
now create view for this login page.

```py
#studybud/base/views.py
def loginPage(request):
    context = {}
    return render(request, 'base/login_register.html', context)
```
```py
#studybud/base/urls.py
urlpatterns = [
    path('login/',views.loginPage, name="login"),
]
```
we can create the loginpage , users can login the page and access the website and  user can also logout ,update and delete the room.
```py
# studybud/base/views.py

from django.shortcuts import render,redirect
from django.contrib.auth.models import User
from django.contrib.auth import authenticate , login,logout
from django.contrib import messages
from .models import Room,Topic
from .forms import RoomForm
from django.db.models import Q
#rooms = [
#    {'id': 1, 'name': 'lets learn python!'},
#    {'id': 2, 'name': 'Design with me.'},
#    {'id': 3, 'name': 'Frontend developer.'},
#]


def loginPage(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        try:
            user = User.objects.get(username=username)
          
        except User.DoesNotExist:
            messages.error(request, 'User does not exist')
        user=authenticate(request,username=username,password=password)
        if user is not None:
            login(request,user)
            return redirect('home')
        else:
            messages.error(request,'Username or Password does not  exist')

    context = {}
    return render(request, 'base/login_register.html', context)
 
def logoutUser(request):
    logout(request)
    return redirect('home')


def home(request):
    q = request.GET.get('q') if request.GET.get('q') is not None else ''

    rooms = Room.objects.filter(
        Q(topic__name__icontains=q) |
        Q(name__icontains=q)|
        Q(description__icontains=q)
        )
    topics= Topic.objects.all()
    room_count = rooms.count()
    context = {'rooms': rooms,'topics':topics ,'room_count':room_count}
    return render(request, 'base/home.html', context)

def room(request,pk):
    room = Room.objects.get(id=pk)
    context = {'room': room}
    return render(request, 'base/room.html', context)

def createRoom(request):
    form=RoomForm()
    if request.method == 'POST': 
        form = RoomForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('home')  
    context = {"form":form}
    return render(request, 'base/room_form.html', context)


def updateRoom (request, pk):
    room =Room.objects.get(id=pk)
    form = RoomForm(instance=room)

    if request.method == 'POST':
        form = RoomForm(request.POST,instance=room)
        if form.is_valid():
            form.save()
            return redirect('home') 
        
    context = {'form': form}
    return render(request, 'base/room_form.html', context)
     

def deleteRoom(request, pk):
     room =Room.objects.get(id=pk)
     if request.method == 'POST':
        room.delete()
        return redirect('home')
     return render(request, 'base/delete.html', {'obj': room})
``` 
and then give the urls of our views  functions to access the different pages in our website.
```py
# studybud/base/urls.py
from django.urls import path
from.import views
urlpatterns = [
    path('login/',views.loginPage, name="login"),
    path('logout/',views.logoutUser, name="logout"),
    
    path("",views.home, name="home"),
    path('room/<str:pk>/',views.room,name="room"),
    path('create-room/', views.createRoom, name='create-room'),
    path('update-room/<str:pk>', views.updateRoom, name='update-room'),
    path('delete-room/<str:pk>', views.deleteRoom, name='delete-room'),


]
```

```py
# base/templates/main.html
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
    
    {% if messages %}
<ul class="messages">
    {% for message in messages %}
    <li></li>{{ message }}</li>
    {% endfor %}
</ul>
{% endif %}

    {% block content %}
    
    {% endblock content %}
</body>
</html>
```
we can set a frame to search different rooms by its author name ,text, name of topic etc and also check the user authenticatons through  login and logout.
```py
# base/navbar.html
<a href="/">
    <h1>LOGO</h1>
</a>
<form method="GET" action="{% url 'home' %}">
    <input type="text" name="q" placeholder="Search Rooms..." />
    <button type="submit">Search</button>
</form>
{% if request.user.is_authenticated %}
<a href="{% url 'logout' %}">Logout</a>
{% else %}
<a href="{% url 'login'%}">Login</a>
{% endif %}

<hr>
```

# `User Registeration`
In user Registeration we can manage user login and registration. It provides forms for users to log in or sign up, handles the authentication process, and allows new users to create accounts and log in automatically.

```py
# studybud/template/base/login_register.html
{% extends 'main.html' %}
{% block content %}


{% if page == 'login' %}

<div>
<form method="POST" action="">
{% csrf_token %}
<label>Username: </label>
<input type="text" name="username" placeholder="Enter Username" />
<br>
<label>Password: </label>
<input type="password" name="password" placeholder="Enter Password" />
<br>
<input type="submit" value="Login" />
</form>

<p>havent signed up yet?</p>

<a href="{% url 'register' %}">Sign up</a>

</div>
{% else %}
<div>
    <form method="POST" action="">
        {% csrf_token %}
        {{form.as_p}}
    <input type="submit" value="Register"/>
    </form>
    <p>Already signed up yet?</p>
    <a href="{% url 'login' %}">Login</a>
</div>

{% endif %}

{% endblock content %}
```


```py
# studybud/base/views

from django.shortcuts import render,redirect
from django.contrib.auth.models import User
from django.http import HttpResponse
from django.contrib.auth.forms import UserCreationForm
from django.contrib.auth import authenticate , login,logout
from django.contrib.auth.decorators import login_required
from django.contrib import messages
from .models import Room,Topic
from .forms import RoomForm
from django.db.models import Q
#rooms = [
#    {'id': 1, 'name': 'lets learn python!'},
#    {'id': 2, 'name': 'Design with me.'},
#    {'id': 3, 'name': 'Frontend developer.'},
#]

def loginPage(request):
    page = 'login' 
    if request.user.is_authenticated:
         return redirect('home')


    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        try:
            user = User.objects.get(username=username)
          
        except User.DoesNotExist:
            messages.error(request, 'User does not exist')
        user=authenticate(request,username=username,password=password)
        if user is not None:
            login(request,user)
            return redirect('home')
        else:
            messages.error(request,'Username or Password does not  exist')

    context = { 'page': page}
    return render(request, 'base/login_register.html', context)
 
def logoutUser(request):
    logout(request)
    return redirect('home')

def registerPage(request):
    form = UserCreationForm()

    if request.method == 'Post':
        form = UserCreationForm(request.Post)
        if form.is_valid():
            user = form.save(commit=False)
            user.username = user.username.lower()
            user.save()
            login(request, user)
            return redirect('home')
        else:
            messages.error(request, 'An error occured during registerations')
            
    return render(request, 'base/login_register.html',{'form': form })


def home(request):
    q = request.GET.get('q') if request.GET.get('q') is not None else ''

    rooms = Room.objects.filter(
        Q(topic__name__icontains=q) |
        Q(name__icontains=q)|
        Q(description__icontains=q)
        )
    topics= Topic.objects.all()
    room_count = rooms.count()
    context = {'rooms': rooms,'topics':topics ,'room_count':room_count}
    return render(request, 'base/home.html', context)

def room(request,pk):
    room = Room.objects.get(id=pk)
    context = {'room': room}
    return render(request, 'base/room.html', context)

def createRoom(request):
    form=RoomForm()
    if request.method == 'POST': 
        form = RoomForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('home')  
    context = {"form":form}
    return render(request, 'base/room_form.html', context)

@login_required(login_url='login')
def updateRoom (request, pk):
    room =Room.objects.get(id=pk)
    form = RoomForm(instance=room)

    if request.user != room.host:
        return HttpResponse('you are not allowed here!!')
    

    if request.method == 'POST':
        form = RoomForm(request.POST,instance=room)
        if form.is_valid():
            form.save()
            return redirect('home') 
        
    context = {'form': form}
    return render(request, 'base/room_form.html', context)
     

def deleteRoom(request, pk):
     room =Room.objects.get(id=pk)

     if request.user != room.host:
        return HttpResponse('you are not allowed here!!')
     
     if request.method == 'POST':
        room.delete()
        return redirect('home')
     return render(request, 'base/delete.html', {'obj': room})
     ```















