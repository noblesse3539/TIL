# Django



## 프로젝트 생성

``` powershell
$ django-admin startproject 프로젝트명 
$ ./manage.py startapp community //앱명
$ ./manage.py migrate // 장고에서 필요한 DB 테이블 생성
$ python manage.py createsuperuser // 슈퍼유저 생성. 깃배쉬에서 그냥은 생성이 안되므로 파이썬을 통해 생성
```



## 서버 구동

``` powershell
$ ./manage.py runserver // 주의! 깃배쉬에서 이 명령어 쓰니까 서버를 끌 수가 없어. ctrl + c가 안먹힘
$ python manage.py runserver // 이런식으로 하면 잘 먹힘
$ python manage.py runserver 8080 // 뒤에 포트를 적어서 열 수도 있음, 디폴트는 8000
```



## 앱 등록

``` python
#settings.py

INSTALLED_APPS = (
	'community' # 추가해야 앱이름(지금은 community)으로 만들어진 디렉터리에 있는 파일들을 코딩해서 쓸 수 있음
)
```



## 간단한 게시판 만들기

### 1. models.py에 모델 생성하기

   ``` python
   # modles.py
   
   class Article(models.Model):
       name = models.CharField(max_length =50)
       title = models.CharField(max_length=50)
       contents = models.TextField()
       url = models.URLField()
       email = models.EmailField()
       cdate = models.DateTimeField(auto_now_add=True)
   ```

### 2.  앱 변화 확인 및 모델 생성

   ``` powershell
   $ ./manage.py makemigrations community // 아직 데이터베이스에 적용은 안된 상태임
   $ ./manage.py migrate // 테이블을 생성함
   
   ```

### 3.  url 경로 설정

   ``` python
   #urls.py
   from community import views
   
   urlpatterns = [
       path('write/', views.write, name='write'),
   ]
   ```

### 4.  views 작성

   ``` python
   # views.py
   
   def write(request):
       return render(request, 'write.html')
   ```

### 5. 템플릿 작성 (html)

앱 디렉터리(여기선 community)에 templates 폴더 생성후, 이곳에 html문서 작성

   ```html
   <!-- write.html -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>write</title>
</head>
<body>
    <form action="", method="POST">
        <!-- {% comment %}
            {{ form.as_table }} 
            {{ form.as_p }}
            {{ form.as_ul }}
        {% endcomment %} -->
        {{ form.as_p }}
        {% csrf_token %}
        <button type="submit", class = "btnbtn-primary">저장</button>
    </form>
</body>
</html>
   ```

### 6. Forms.py

``` python
from django.forms import ModelForm
from community.models import *

class Form(ModelForm):
    class Meta:
        model = Article
        fields = ['name', 'title', 'contents', 'url', 'email'] # models.py에 작성한 필드들
        
# 이곳에 생성한 폼을 view에서 사용 가능
```

