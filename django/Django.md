# Django

## 1. 시작하기

1. 프로젝트 시작하기

  ``` bash
  $ django-admin startproject (프로젝트이름)
  ```

  아래와 같이 프로젝트 구조가 만들어진다.

  ``` text
  django_intro/ (프로젝트 이름이 django_intro임)
  ├── django_intro/
  │	  ├── __init__.py
  │	  ├── settings.py
  │	  ├── urls.py
  │	  └── wsgi.py
  ├── db.sqlite3
  └── manage.py
  ```

  지금부터 pwd는 `~/workspace/django_intro` 이다.



2. 서버 실행하기

   * `settings.py`

   	``` python
   	ALLOWED_HOST = ['*']
   	# c9에서는 host - 0.0.0.0, port - 8080만 활용할 수 있기 때문에 위와 같이 설정한다.
   	```

   

   ``` bash
   ~/workspace/django_intro $ python manage.py runserver 0.0.0.0:8080
   ```

   앞으로 모든 장고 명령어는 프로젝트를 만들 때를 제외하고 `python manage.py`를 활용한다. 따라서, 반드시 `pwd` 와 `ls`를 통해 현재 bash 위치를 확인하자!!



## 2. hello, Django

> Django 프로젝트는 여러가지 app의 집합이다.
>
> 각각의 app은 MTV 패턴으로 구성되어 있다.
>
> M(Model): 어플리케이션의 핵심 로직의 동작을 수행한다.
>
> T(Template): 사용자에게 결과물을 보여준다.
>
> V(View): 모델과 템플릿의 동작을 제어한다. (모델의 상태를 변경하거나 값을 가져오고, 템플릿에 값을 전달하기 등)
>
> **일반적으로 MVC패턴으로 더 많이 사용된다.**

``` bash
/django_intro $ django-admin startapp <app 이름>
```



### 1. 기본 로직

앞으로 우리는 1. 요청 url 설정(`urls.py`) 2. 처리 할 view 설정(`views.py`) 3. 결과 보여줄 template 설정(`templates/`)으로 작성할 것이다.

1. url 설정

   ``` python
   # django_intro/urls.py
   
   from django.contrib import admin
   from django.urls import path
   # home 폴더 내에 있는 views.py를 불러온다.
   from home import views
   
   urlpatterns = [
       path('admin/', admin.site.urls),
       #  요청이 home/으로 오면, view의 index 함수를 실행시킨다.
       path('home/', views.index)
   ]
   ```

   

2. view 설정

   ``` python
   # home/views.py
   from django.shortcuts import render, HttpResponse
   
   # Create your views here.
   def index(request):
       return HttpResponse('hello, django!')
   ```

   * 주의할 점은 선언된 함수에서 `request`를 매개변수로 받아야 한다.
     * request는 사용자(클라이언트)의 요청 정보와 서버에 대한 정보가 담겨 있다.
     * Django 내부에서 해당 함수를 호출하면서 정보를 넘겨주기 떄문에 반드시 명시해줘야한다.

## 3. Template(MTV - T)

   > Django에서 활용되는 Template은 DTL(Django Template Language)이다.
   >
   > jinja2와 문법이 유사하다.

   1. 요청 url 설정

   ``` python
   # urls.py
   urlpatterns = [
       ...
       path('home/dinner/', views.dinner)
   ]
   ```

   2. view 설정

   ``` python
   # home/views.py
   
   ....
   
   def dinner(request):
       box = ['치킨', '치킨', '치킨', '와퍼']
       pick = random.choice(box)
       
       return render(request, 'dinner.html', {'dinner': pick})
     
   ```

   * Template을 리턴하려면, `render`를 사용하여야 한다.
     * `request`(필수)
     * `template 파일 이름`(필수)
     * `template 변수`(선택): `dictionary` 타입으로 구성해야 한다.

3. Template 설정

   ``` bash
   $ mkdir home/templates
   $ touch home/templates/dinner.html
   ```

   ``` html
   <!-- home/templates/dinner.html -->
   <h1> {{ dinner }} </h1>
   ```




## 4. Variable Routing

1. url 설정

   ``` python
   path('home/you/<name>', views.you),
   path('home/cube/<int:num>', views.cube),
   ```

2. view 파일 설정

   ``` python
   def you(request, name):
       return render(request, 'you.html', {'name': name})
   def cube(request, num):
       return render(request, 'cube.html', {'num': num**3})
   ```

3. 템플릿 파일 설정

   ``` django
   <h1>{{ name }}, 안녕!!</h1>
   ```
   ``` django
   <h1>{{ num }}</h1>
   ```


## 5. Form data

* url 과 view는 위와 같이 설정한다.
* POST의 경우 경로설정 시 반드시 '/'를 붙여야 한다!!

1. url 설정

``` python
    path('home/ping/', views.ping),
    path('home/pong/', views.pong),
    path('home/user_new/', views.user_new),
    path('home/user_read/', views.user_read),
```



2. view 설정
  1. GET:

   ``` python
   def pong(request):
       msg = request.GET.get('message')
       return render(request, 'pong.html', {'msg' : msg})
   ```

   2. POST:

      * `csrf_token`은 보안을 위해 django에서 기본적으로 설정되어 있는 것이다.
      * POST는 장고에서 반드시 CSRF 토큰을 넘겨주어야 한다.
      * form을 통해 POST 요청을 보낸다는 것은 데이터베이스에 반영되는 경우가 대부분인데, 해당 요청을 우리가 만든 정해진 form에서 보내는지 검증하는 것.
      * 실제로 input type hidden으로 설정되어있다.
      * `settings.py`에 `MIDDLEWARE` 설정에 보면 csrf 관련된 내용이 설정된 것을 볼 수 있다.

      > CSRF 공격 : Cross Site Request Forgery

      

   ``` django
   <form action="/home/user_read/" method="POST">
           {% csrf_token %}
           <h2>ID: </ID><input type="text" name="user_id"/></h2>
           <h2>PASSWORD: <input type="password" name="user_password"/></h2>
           <input type="submit" value="Submit"/>
       </form>
   ```

   ``` python
   def user_read(request):
       user_id = request.POST.get('user_id')
       user_password = request.POST.get('user_password')
       return render(request, 'user_read.html', {'user_id' : user_id, 'user_password' : user_password}) 
   ```



## 6. static file 관리

> 정적 파일(images, css, js)을 서버 저장이 되어 있을 때, 이를 각각의 템플릿에 불러오는 방법

### 디렉토리 구조

디렉토리 구조는 `home/static/home/`으로 구성된다.

이 디렉토리 설정은 `settings.py`의 가장 하단에 `STATIC_URL` 변수를 통해 변경할 수 있다. (기본 `/static/`)

1. 파일 생성

   `home/static/home/images/1.jpg`

   `home/static/home/stylesheets/style.css`

2. 템플릿 활용

   ``` django
   {% extends 'base.html' %}
   {% load static %}
   {% block css %}
   	<link rel="stylesheets" type="text/css" href="{% static 'home/stylesheets/style.css'%}">
   {% endblock %}
   {% block body %}
   <img src="{% static 'home/images/1.jpg' %}">
   {% endblock%}
   ```





## 7. URL 설정 분리

> 지금과 같은 코드를 짜는 경우에, `django_intro/urls.py`에 모든 url 정보가 담기게 된다.
>
> 일반적으로 Django 어플리케이션에서 url을 설정하는 방법은 app 별로 `urls.py`를 구성하는 것이다.

1. `django_intro/urls.py`

   ``` python
   from django.contrrib import admin
   from django.urls import path, include
   
   urlpatters = [
       path('admin/', admin.site.urls),
       path('home/', include('home.urls')),
   ]
   ```

   * `include`를 통해 `app/urls.py`에 설정된 url을 포함한다.

2. `home/urls.py`

   ``` python
   from django.urls import path
   # views는 home/views.py
   urlpatters = [
       path('', views.index),
   ]
   ```

   * `home/views.py` 파일에서 `index`를 호출하는 url은 `http://<host>/`이 아니라, `http://<host>/home/`이다.



## 8. Template 폴더 설정

### 디렉토리 구조

디렉토리 구조는 `home/templates/home/`으로 구성된다.

디렉토리 설정은 `settings.py`의 `TEMPLATES`변수를 통해 변경할 수 있다.

``` python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'django_intro', 'templates'),],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

* `DIRS` : templates를 커스텀하여 경로를 설정할 수 있다.

  * 경로 설정

    ``` python
    os.path.join(BASE_DIR, 'django_intro', 'templates')
    #=> BASE_DIR(PROJECT1)/django_intro/templates/
    ```

* `APP_DIRS` : `INSTALLED_APPS`에 설정된 app의 디렉토리에 있는 `templates`를 템플릿으로 활용한다. (True)

1. 활용 예시

   ``` python
   # home/views.py
   def index(request):
       return render(request, 'home/index.html')
   ```

   ``` text
   ├── __init__.py
   ├── admin.py
   ├── apps.py
   ├── migrations
   ├── models.py
   ├── static
   │   └── home
   │       ├── images
   │       │   └── img_1.png
   │       └── stylesheets
   │           └── style.css
   ├── templates
   │   └── home
   │       ├── cube.html
   │       ├── dinner.html
   │       ├── index.html
   │       ├── ping.html
   │       ├── pong.html
   │       ├── static_example.html
   │       ├── template_example.html
   │       ├── user_new.html
   │       ├── user_read.html
   │       └── you.html
   ├── tests.py
   ├── urls.py
   └── views.py
   ```

   