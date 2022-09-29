---
layout: post
title: Django - Todo list 만들기
date: 2022-09-29 19:10:00 +0900
image:django.jpg
tags: django
categories: django
---

## Django 환경설정부터 Todo list 구현까지

<br>

## 요구사항

### 모델 Model

모델은 아래 조건을 만족해야 합니다.

다만, 기능 추가를 위해 필드를 추가해도 됩니다.

- 모델 이름 : Todo

- 모델 필드 및 속성

  | 필드 이름  | 역할       | 필드    | 속성              |
  | ---------- | ---------- | ------- | ----------------- |
  | content    | 할 일 내용 | Char    | max_length=80     |
  | completed  | 완료 여부  | Boolean | default=False     |
  | priority   | 우선순위   | Integer | default=3         |
  | created_at | 생성 날짜  | Date    | auto_now_add=True |
  | deadline   | 마감 기한  | Date    | null=True         |

### 기능 View

아래 기능을 구현합니다.

- 할 일 추가하기 Create
  - 힌트
    1. create() 메소드를 활용합니다.
    2. 아래 데이터를 사용자에게 입력받아서 데이터를 생성합니다.
       - 내용 / 우선 순위 / 마감 기한
    3. 할 일 목록 페이지로 redirect 합니다.
- 할 일 목록 보기 Read
  - 힌트
    1. 모든 데이터를 id를 기준으로 오름차순으로 정렬해서 불러옵니다.
    2. 불러온 데이터를 템플릿에서 반복문을 사용해 1개씩 화면에 표시합니다.
- 할 일 완료(completed) 여부(True / False) 변경하기 Update
  - 힌트
    1. 삭제할 할 일의 id가 필요합니다.
    2. get() 메소드를 사용하여 변경할 데이터를 불러옵니다.
    3. 불러온 데이터의 상태를 변경 후 저장합니다.
    4. 할 일 목록 페이지로 redirect 합니다.
- 할 일 삭제하기 Delete
  - 힌트
    1. 삭제할 할 일의 id가 필요합니다.
    2. get() 메소드를 사용하여 변경할 데이터를 불러옵니다.
    3. 불러온 데이터를 삭제합니다.
    4. 할 일 목록 페이지로 redirect 합니다.

### 화면 Template

- 할 일 추가 폼 <form>

  - 할 일
    - <input type = “text”> 태그를 활용합니다.
    - 최대 입력 길이는 80입니다.
  - 우선 순위
    - <select> <option> 태그를 활용합니다.
    - 참고 자료 : https://thrillfighter.tistory.com/572
  - 마감 기한
    - <input type="date"> 태그를 활용합니다.
  - 할 일 추가 버튼
    - <input type=”submit”> 태그를 활용합니다.

  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72153a58-09b6-4827-af5d-4250235981fe/Untitled.png)

  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0d52e188-dfe3-45f4-ac24-316044b7594d/Untitled.png)

- 할 일 목록 테이블 <table>

  - <thead>
    - 우선 순위 / 할 일 내용 / 생성 날짜 / 마감 기한 / 진행 상태 / 상태 변경 / 삭제 를 테이블 헤더로 사용합니다.
  - <tbody>
    - id를 기준으로 오름차순으로 정렬한 모든 데이터를 화면에 표시합니다.
  - 변경
    - 버튼을 누르면 해당 할 일의 상태(True / False)가 수정됩니다.
  - 삭제
    - 버튼을 누르면 해당 할 일이 삭제됩니다

<br>

## 가상환경 생성 및 프로젝트 생성

#### 작업 폴더 생성 및 이동

``` terminal
> mkdir todos
> cd todos
```

<br>

#### 가상 환경 생성

``` terminal
> python -m venv [가상환경 이름]
> python -m venv todos-venv
```

<br>

#### 가상 환경 실행

``` terminal
> source todos-venv/bin/activate # mac
```

<br>

#### pip 버전 확인

``` terminal
> pip list

Package    Version
---------- -------
pip        22.0.4
setuptools 58.1.0
WARNING: You are using pip version 22.0.4; however, version 22.2.2 is available.
You should consider upgrading via the '/Users/mac/Desktop/20220928/todos/todos-venv/bin/python -m pip install --upgrade pip' command.
```

<br>

#### pip 업데이트

``` terminal
python -m pip install --upgrade pip
```

<br>

#### Django 프로젝트 폴더 생성

``` terminal
> django-admin startproject [폴더명]
> django-admin startproject todospjt
```

<br>

#### 애플리케이션 폴더 생성

* manage.py 가 있는 경로에서 실행해야함

``` terminal
> python manage.py startapp [폴더명]
> python manage.py startapp todo
```

<br>

#### 애플리케이션 실행

``` terminal
> python manage.py runserver
```

* 실행 후 나오는 주소를 입력해서 동작하는지 확인할 것

<br>

## 프로젝트 설정하기

#### django 프로젝트 폴더(todospjt) > settings.py

``` python
INSTALLED_APPS = [
  	# 생성한 애플리케이션 폴더(todo) 등록
  	'todo',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

<br>

#### 애플리케이션 폴더(todo) > models.py

* 주어진 내용에 맞게 models 작성

``` python
from django.db import models

# Create your models here.
class Todo(models.Model):
    # django에서 pk는 자동으로 만들어준다.
    content = models.CharField(max_length = 80)     # 할 일 내용 
    completed = models.BooleanField(default=False)  # 완료 여부
    priority = models.IntegerField(default=3)       # 우선순위
    created_at = models.DateField(auto_now_add=True)# 생성 날짜
    """
    default 
    데이터를 생성할 때 값을 안넣으면 
    자동으로 값을 채워서 데이터를 생성하겠다.
    """
    deadline = models.DateField(null=True)          # 마감 기한
```

<br>

#### 마이그레이션 파일 생성

* models.py 에서 만든 설계도를 데이터베이스에 '이주' 시키는 것

  ``` terminal
  > python manage.py makemigrations
  
  # 실행 결과
  Migrations for 'todo':
    todo/migrations/0001_initial.py
      - Create model Todo
  
  ```

<br>

#### 마이그레이트

``` terminal
 > python manage.py migrate
```

<br>

## URL 분리 및 프로젝트 실행하기

* 전체 프로젝트 URL에서 개별 애플리케이션의 URL을 분리해서 관리

#### 애플리케이션 폴더(todo) > urls.py 를 새로 생성

#### 프로젝트 폴더(todospjt) > urls.py

* 전체 프로젝트 파일에서 개별 애플리케이션 URL을 '포함' 시키기 위해 **django.urls에 include를 추가**

``` python
from django.contrib import admin
# include를 추가
from django.urls import path, include 

urlpatterns = [
    path('admin/', admin.site.urls),
  	# todo(애플리케이션 폴더)에 있는 urls를 가져온다
    path('', include('todo.urls')),
]
```

<br>

#### 애플리케이션 폴더(todo) > urls.py

* index url 생성 
* namespace 생성

``` python
from django.urls import path
from . import views # .은 현재경로 라는 뜻, 현재경로의 views를 가져온다. 

# url namespace
# url을 이름으로 분류하는 기능

app_name = 'todo' 

urlpatterns = {
    path('', views.index, name='index'),

}
```

<br>

#### 애플리케이션 폴더(todo) > views.py

* urls.py에서 작성한 index에 대한 정보를 views.py 에서 정의

``` python
from django.shortcuts import render

# Create your views here.
def index(request):

    return render(request, 'todo/index.html')
```

<br>

#### 애플리케이션 폴더(todo) > template 폴더 생성 > template 폴더 내 todo 폴더 생성 > index.html 파일 생성

<br>

#### templates > base.html

``` html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <!-- CSS only -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/css/bootstrap.min.css" rel="stylesheet"
    integrity="sha384-iYQeCzEYFbKjA/T2uDLTpkwGzCiq6soy8tYaI1GyVh/UjpbCx/TYkiZhlZB6+fzT" crossorigin="anonymous">
  <!-- JavaScript Bundle with Popper -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.1/dist/js/bootstrap.bundle.min.js"
    integrity="sha384-u1OknCvxWvY5kfmNBILK2hRnQC3Pr17a+RTT6rIHI7NnikvbZlHgTPOOmMi466C8"
    crossorigin="anonymous"></script>
</head>

<body>
  {% block content %}
  {% endblock content %}
</body>

</html>
```

<br>

#### templates > todo > index.html

``` html
{% extends 'base.html' %}

{% block content %}
  <h1>index.html</h1>
{% endblock %}
```

<br>

#### 프로젝트 실행 후 작동 확인(manage.py 경로에서 실행 해야함)

``` terminal
> python manage.py runserver
```

<br>

## 본격적인 프로젝트 내용 작성

* 아래의 내용부터는 프로젝트의 내용에 대해서 다루므로, 내용이 많습니다. 프로젝트의 생성과 실행만 참고한다면 보지 않아도 상관없어요.

## 1. 할 일 추가하기(Create)

#### templates > todo > index.html

* 요구사항에 맞게 form 및 input 작성
* input 값에 maxlength="80" 옵션을 주어 model에서 작성한 값의 유효성 검사를 함.
* form의 action에 create 라는 이름을 가진 주소를 요청
* 주소를 요청할때는 app_name을 지정했으므로 `app_name:요청페이지` 형태로 요청
* input에 입력한 text 값을 `content_` 라는 이름으로 식별해준다. (임의 지정)

``` html
{% extends 'base.html' %}

{% block content %}
  <h1>index.html</h1>
  <!-- 사용자에게 정보를 입력받을 때 form 태그를 사용해야한다. -->
  <!-- action : 어떤 url을 요청할지 -->
  <!-- create 라는 이름을 가진 주소를 요청 -->
  <form action="{% url ' todo:create' %}">
    <!-- input에 입력한 text 값을 content_ 로 식별해준다 -->
    <input type="text" name="content_" id="" maxlength="80">
    <input type="submit" value="할 일 추가">
{% endblock %}
```

<br>

#### 애플리케이션 폴더(todo) > urls.py

* 요청할 create 에 대한 url 정의 

``` python
from django.urls import path
from . import views # .은 현재경로 라는 뜻, 현재경로의 views를 가져온다. 

# url namespace
# url을 이름으로 분류하는 기능

app_name = "todo"

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),

]
```

<br>

#### 애플리케이션 폴더(todo) > views.py

* url.py 에서 정의한 create를 views.py에서 정의

``` python
from django.shortcuts import render
from .models import Todo

# Create your views here.
def index(request):

    return render(request, 'todo/index.html')

def create(request):
  	# input
    content = request.GET.get("content_")
    Todo.objects.create(content=content)
    return  render(request, 'todo/index.html')
```

<br>

## 2. 할 일 목록 보기(Read)

#### 애플리케이션 폴더(todo) > views.py 

* redirect 사용을 위해  django.shortcuts에 redirect import
* 조회를 위해 index에 models에서 정의한 Todo의 모든 정보를 가져와서 _todos에 저장
* context에 _todos의 정보를 담아서 반환하게함
* create에 반환을 redirect로 하여 변경된 값을 바로 반영해서 보여주게함

``` python
# redirect 사용을 위해 import
from django.shortcuts import render, redirect
# db에 저장하기 위해 model을 import
from .models import Todo

# Create your views here.
def index(request):
    # models에서 정의한 Todo의 모든 정보를 가져와서 _todos에 저장 
    _todos = Todo.objects.all()
    # _todos의 정보를 context에 담아서 반환하게함
    context = {
        "todos" : _todos,
    }
    return render(request, 'todo/index.html', context)

def create(request):
    # input에서 입력받은 값을 content에 저장 
    content = request.GET.get("content_")
    # db에 저장, create(필드, 값) 
    Todo.objects.create(content=content)

    _todos = Todo.objects.all()
    context = {
        "todos" : _todos,
    }

    return redirect('todo:index')
```

<br>

#### templates > todo > index.html

* DTL for문을 사용하여 views.py에서 정의된 todos를 반복문을 돌면서 뿌려줌

``` python
{% extends 'base.html' %}

{% block content %}
  <h1>index.html</h1>
  <!-- 사용자에게 정보를 입력받을 때 form 태그를 사용해야한다. -->
  <!-- action : 어떤 url을 요청할지 -->
  <!-- create 라는 이름을 가진 주소를 요청 -->
  <form action="{% url 'todo:create' %}">
    <!-- input에 입력한 text 값을 content_ 로 식별해준다 -->
    <input type="text" name="content_" id="" maxlength="80">
    <input type="submit" value="할 일 추가">
  </form>

  <!-- DTL for문 사용법 -->
  <ul>
  	# todos요소를 돌면서 
    {% for todo in todos %}
    # todos의 id, content, completed를 뿌려줌
    <li>{{ todo.id }} - {{ todo.content }} - {{ todo.completed }}</li>
    {% endfor %}
  </ul>
{% endblock %}
```

<br>

## 3. 할 일 완료(completed) 여부 (True/False) 변경하기(Update)

#### templates > todo > index.html

``` html
{% extends 'base.html' %}

{% block content %}
<h1>index.html</h1>
<!-- 사용자에게 정보를 입력받을 때 form 태그를 사용해야한다. -->
<!-- action : 어떤 url을 요청할지 -->
<!-- create 라는 이름을 가진 주소를 요청 -->
<form action="{% url 'todo:create' %}">
  <!-- input에 입력한 text 값을 content_ 로 식별해준다 -->
  <input type="text" name="content_" id="" maxlength="80">
  <input type="submit" value="할 일 추가">
</form>

<!-- DTL for문 사용법 -->
<ul>
  {% for todo in todos %}
  <li>{{ todo.id }} - {{ todo.content }} - {{ todo.completed }}
    <!-- 수정 버튼 생성 -->
    <a href="{% url 'todo:update' todo.pk %}">변경</a>
  </li>
  {% endfor %}
</ul>
{% endblock %}
```

<br>

#### 애플리케이션 폴더(todo) > urls.py

* urlpatterns에 update를 정의, 수정할 항목을 구분하기 위해 pk값을 이용

``` python
from django.urls import path
from . import views # .은 현재경로 라는 뜻, 현재경로의 views를 가져온다. 

# url namespace
# url을 이름으로 분류하는 기능

app_name = "todo"

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),
    path('update/<int:pk>', views.update, name='update'),
]
```

<br>

#### 애플리케이션 폴더(todo) > views.py 

* todo에 pk값을 가져와 저장 
* pk_를 사용해 update할 특정 데이터를 불러온다
* 불러온 완료 여부의 값을 내가 수정한 값으로 변경
* 수정 후 index로 리다이렉트시켜 바로 반영된 정보를 보여주게함

``` python
# redirect 사용을 위해 import
from django.shortcuts import render, redirect
# db에 저장하기 위해 model을 import
from .models import Todo

# Create your views here.
def index(request):
    # models에서 정의한 Todo의 모든 정보를 가져와서 _todos에 저장 
    _todos = Todo.objects.all()
    # _todos의 정보를 context에 담아서 반환하게함
    context = {
        "todos" : _todos,
    }
    return render(request, 'todo/index.html', context)

def create(request):
    # input에서 입력받은 값을 content에 저장 
    content = request.GET.get("content_")
    # db에 저장, create(필드, 값) 
    Todo.objects.create(content=content)

    _todos = Todo.objects.all()
    context = {
        "todos" : _todos,
    }

    return redirect('todo:index')

def update(request, pk):
    # update할 특정 데이터를 불러온다 -> pk_를 사용
    todo = Todo.objects.get(pk = pk)
    # True로 변경
    completed_ = True
    # 불러온 완료 여부의 값을 내가 수정한 값으로 변경
    todo.completed = completed_
    # 데이터를 수정한 것을 반영
    todo.save()
    return redirect('todo:index')
```

<br>

## 4. 할 일 삭제하기(Delete)

#### templates > todo > index.html

* li 태그 내에 삭제 버튼 생성

``` html
{% extends 'base.html' %}

{% block content %}
<h1>index.html</h1>
<!-- 사용자에게 정보를 입력받을 때 form 태그를 사용해야한다. -->
<!-- action : 어떤 url을 요청할지 -->
<!-- create 라는 이름을 가진 주소를 요청 -->
<form action="{% url 'todo:create' %}">
  <!-- input에 입력한 text 값을 content_ 로 식별해준다 -->
  <input type="text" name="content_" id="" maxlength="80">
  <input type="submit" value="할 일 추가">
</form>

<!-- DTL for문 사용법 -->
<ul>
  {% for todo in todos %}
  <li>{{ todo.id }} - {{ todo.content }} - {{ todo.completed }}
    <!-- 수정 버튼 생성 -->
    <a href="{% url 'todo:update' todo.pk %}">변경</a>
    <!-- 삭제 버튼 생성 -->
    <a href="{% url 'todo:delete' todo.pk %}">삭제</a>
  </li>
  {% endfor %}
</ul>
{% endblock %}
```

<br>

#### 애플리케이션 폴더(todo) > urls.py

* urlpatterns 에 delete를 정의

``` python
from django.urls import path
from . import views # .은 현재경로 라는 뜻, 현재경로의 views를 가져온다. 

# url namespace
# url을 이름으로 분류하는 기능

app_name = "todo"

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),
    path('delete/<int:todo_pk>', views.delete, name='delete'),
      path('update/<int:pk>', views.update, name='update'),
]
```

<br>

#### 애플리케이션 폴더(todo) > views.py 

* todo에 pk값을 가져와 저장 
* todo를 삭제
* 삭제 후 index로 리다이렉트시켜 바로 반영된 정보를 보여주게함

``` python
# redirect 사용을 위해 import
from django.shortcuts import render, redirect
# db에 저장하기 위해 model을 import
from .models import Todo

# Create your views here.
def index(request):
    # models에서 정의한 Todo의 모든 정보를 가져와서 _todos에 저장 
    _todos = Todo.objects.all()
    # _todos의 정보를 context에 담아서 반환하게함
    context = {
        "todos" : _todos,
    }
    return render(request, 'todo/index.html', context)

def create(request):
    # input에서 입력받은 값을 content에 저장 
    content = request.GET.get("content_")
    # db에 저장, create(필드, 값) 
    Todo.objects.create(content=content)

    _todos = Todo.objects.all()
    context = {
        "todos" : _todos,
    }

    return redirect('todo:index')
  
def update(request, pk):
    # update할 특정 데이터를 불러온다 -> pk_를 사용
    todo = Todo.objects.get(pk = pk)
    # True로 변경
    completed_ = True
    # 불러온 완료 여부의 값을 내가 수정한 값으로 변경
    todo.completed = completed_
    # 데이터를 수정한 것을 반영
    todo.save()
    return redirect('todo:index')
  
def delete(request, todo_pk):
    todo = Todo.objects.get(pk = todo_pk)
    todo.delete()

    return redirect('todo:index')
```

<br>

## 디자인 및 기능 변경

* 여기서부터는 위의 작업과정을 거치고 난 후에 제 주관적인 생각으로 작성한 디자인과 기능이 포함되어 있습니다. 내용이 난잡하니 넘기셔도 상관없습니다.
* 내용이 많으므로 설명은 주석으로 하고 과정을 일일히 보여주지 않습니다.

#### index.html

``` html
{% extends 'base.html' %}

{% block content %}
<!-- 변경 버튼 클릭 시 취소선을 긋기 위한 스타일 정의 -->
<style>
  .checked {
    color: grey;
    text-decoration-line: line-through;
  }
</style>
<h1>Todo.list</h1>
<!-- 사용자에게 정보를 입력받을 때 form 태그를 사용해야한다. -->
<!-- action : 어떤 url을 요청할지 -->
<!-- create 라는 이름을 가진 주소를 요청 -->
<form action="{% url 'todo:create' %}">
  <!-- input에 입력한 text 값을 content_ 로 식별해준다 -->
  
  <!-- 할 일 -->
  <div class="input-group mb-3">
    <span class="input-group-text" id="inputGroup-sizing-default">할 일</span>
    <input type="text" class="form-control" name="content_" maxlength="80" aria-label="Sizing example input"
      aria-describedby="inputGroup-sizing-default">
  </div>
  
  <!-- 우선 순위 -->
  <div class="input-group mb-3">
    <label class="input-group-text" for="inputGroupSelect01">우선 순위</label>
    <select class="form-select" name="priority_" id="inputGroupSelect01">
      <option selected>클릭하여 선택</option>
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
      <option value="4">4</option>
      <option value="5">5</option>
    </select>
  </div>
  
  <!-- 마감기한 -->
  <div class="input-group date mb-3">
    <label class="input-group-text">마감 기한</label>
    <input type="text" class="form-control" name="deadline_" placeholder="YYYY-MM-DD">
    <span class="input-group-addon"><i class="glyphicon glyphicon-calendar"></i></span>
  </div>
  
  <!-- 할 일 추가 버튼 -->
  <button type="submit" class="btn btn-outline-primary col-12">할 일 추가</button>
</form>

<!-- 테이블 영역 -->
<table class="table">
  <!-- 헤드 -->
  <thead class="table-light">
    <tr>
      <th scope="col">우선 순위</th>
      <th scope="col">할 일</th>
      <th scope="col">생성 날짜</th>
      <th scope="col">마감 기한</th>
      <th scope="col">진행 상태</th>
      <th scope="col">상태 변경</th>
      <th scope="col">삭 제</th>
    </tr>
  </thead>
  <!-- 바디 -->
  <tbody>
    {% for todo in todos %}
    <tr>
      {% if todo.completed %}

      <th><del>{{ todo.priority }}</del></th>
      <th><del>{{ todo.content }}</del></th>
      <th><del>{{ todo.created_at }}</del></th>
      <th><del>{{ todo.deadline }}</del></th>
      <th><del>{{ todo.completed }}</del></th>

      {% else %}
      <th>{{ todo.priority }}</th>
      <th>{{ todo.content }}</th>
      <th>{{ todo.created_at }}</th>
      <th>{{ todo.deadline }}</th>
      <th>{{ todo.completed }}</th>
      {% endif %}
      <th>
        <form action="{% url 'todo:update' todo.pk %}">
          <button type="submit" class="btn btn-primary mod">변경</button>
        </form>
      </th>
      <th>
        <form action="{% url 'todo:delete' todo.pk %}">
          <button type="submit" class="btn btn-danger">삭제</button>
        </form>
      </th>
    </tr>
    {% endfor %}
  </tbody>
</table>

<!-- datepicker 스크립트 -->
<script type='text/javascript' src='//code.jquery.com/jquery-1.8.3.js'></script>
<link rel="stylesheet"
  href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.5.0/css/bootstrap-datepicker3.min.css">
<script type='text/javascript'
  src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.5.0/js/bootstrap-datepicker.min.js"></script>
<script src="/js/bootstrap-datepicker.kr.js" charset="UTF-8"></script>
<script type='text/javascript'>
  $(function () { $('.input-group.date').datepicker({ calendarWeeks: false, todayHighlight: true, autoclose: true, format: "yyyy-mm-dd", language: "kr" }); });
</script>
<!-- datepicker function -->
<script>
  $(document).ready(function () {
    var date_input = $('input[name="date"]');
    var container = $('.bootstrap-iso form').length > 0 ? $('.bootstrap-iso form').parent() : "body";
    var options = {
      format: 'YYYY-MM-DD',
      container: container,
      todayHighlight: true,
      autoclose: true,
    };
    date_input.datepicker(options);
  })
</script>
{% endblock %}
```

<br>

#### urls.py

* 변경 사항이 없습니다.

``` python
from django.urls import path
from . import views # .은 현재경로 라는 뜻, 현재경로의 views를 가져온다. 

# url namespace
# url을 이름으로 분류하는 기능

app_name = "todo"

urlpatterns = [
    path('', views.index, name='index'),
    path('create/', views.create, name='create'),
    path('delete/<int:todo_pk>', views.delete, name='delete'),
    path('update/<int:pk>', views.update, name='update'),
]
```

<br>

#### views.py

* create 부분의 내용이 변경되었습니다.
* index.html 에서 출력되는 테이블에 맞게 내용을 출력하기 위해 변경되었습니다.

``` python
# redirect 사용을 위해 import
from django.shortcuts import render, redirect
# db에 저장하기 위해 model을 import
from .models import Todo

# Create your views here.
def index(request):
    # models에서 정의한 Todo의 모든 정보를 가져와서 _todos에 저장 
    _todos = Todo.objects.all()
    # _todos의 정보를 context에 담아서 반환하게함
    context = {
        "todos" : _todos,
    }
    return render(request, 'todo/index.html', context)

def create(request):
    # input에서 입력받은 값을 content에 저장 
    content = request.GET.get("content_")
    priority = request.GET.get("priority_")
    deadline = request.GET.get("deadline_")
    # db에 저장, create(필드, 값) 
    # create를 각각 하면 테이블이 생성될 때 바뀐 항목마다 개별적으로 생성되기 때문에 하나에 담아서 생성
    Todo.objects.create(content=content, priority=priority, deadline=deadline)

    _todos = Todo.objects.all()
    context = {
        "todos" : _todos,
    }

    return redirect('todo:index')

def delete(request, todo_pk):
    todo = Todo.objects.get(pk = todo_pk)
    todo.delete()

    return redirect('todo:index')

def update(request, pk):
    # update할 특정 데이터를 불러온다 -> pk_를 사용
    todo = Todo.objects.get(pk = pk)
    completed_ = True

    # 불러온 제목과 내용의 값을 내가 수정한 값으로 변경
    todo.completed = completed_

    # 데이터를 수정한 것을 반영
    todo.save()

    return redirect('todo:index')
```

<br>

## 시연하기

<video src="../images/과정.mp4"></video>
