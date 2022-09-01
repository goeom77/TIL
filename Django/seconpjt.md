# 20220901

django: django
복습: No
작성일시: 2022년 9월 1일 오전 9:21

## ✨Django Syntex

- http://local.8000/articles/app
→ {% url=’article:app’ %}
django
- >articles
    >templates ← 규약
        >app ← template name space
            -.html
- catch & get
    
    ```python
    <h1>NEW</h1>
      <form action="{% url 'articles:create' %}" method="GET">
        <label for="title">Title: </label>
        <input type="text" name="title" id="title"><br>
        <label for="content">Content: </label>
        <input type="text" name="content" id="content"><br>
        <input type="submit">
      </form>
    ```
    
- migration 만들기
    
    ```python
    # articles/models.py
    class Article(models.Model):
        title = models.CharField(max_length=10)
        content = models.TextField()
        created_at = models.DateTimeField(auto_now_add=True)
        updated_at = models.DateTimeField(auto_now=True)
    ```
    

### ✨CRUD

- models.Model 클래스
    - → 테이블 모양의 RDB(관계형 DB : 역사적으로 오래 사용해와서 그만큼 안정성이 있다.)
    - `python [manage.py](http://manage.py) makemigration`
    - `python [manage.py](http://manage.py) shell_plus`
        
        ```python
        created_at = models.DateTimeField(auto_now_add=True)
        # 1 → enter : default 값 부여 (설치시간 넣을때)
        updated_at = models.DateTimeField(auto_now=True)
        ```
        
    - get() : unique한 값에서만 사용 가능하다. → pk만 가능( 1개만 들고 오는 것)
        
        ```html
        In [18]: Article.objects.get(pk=1)
        Out[18]: <Article: Article object (1)>
        ```
        
    - filter : 걸러내기
        
        ```html
        In [20]: Article.objects.filter(content='django!')
        Out[20]: <QuerySet [<Article: Article object (1)>, <Article: Article object (2)>, <Article: Article object (3)>]>
        
        In [21]: Article.objects.filter(content='yeah')
        Out[21]: <QuerySet []>
        
        ~~In [22]: Article.objects.filter(pk=3)
        Out[22]: <QuerySet [<Article: Article object (3)>]>~~
        # 적합하지 않다. 
        
        추가) contains : 일부만 포함된것을 필터
        In [19]: Article.objects.filter(content__contains='dj')
        Out[19]: <QuerySet [<Article: Article object (1)>, <Article: Article object (2)>, <Article: Article object (3)>]>
        ```
        
    - 

### ✨DB 데이터 사용하기

```python
def index(request):
    # DB에 전체 데이터를 조회
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)
```

```python
<a href="{% url 'articles:new' %}">NEW</a>
  <hr>
  {% for article in articles %}
    <p>글 번호 : {{ article.pk }}</p>
    <p>제목 : {{ article.title }}</p>
    <p>내용 : {{ article.content }}</p>
    <hr>
```

### ✨web page 상에서 정보 넣기

```python
<h1>NEW</h1>
  <form action="{% url 'articles:create' %}" method="GET">
    <label for="title">Title: </label>
    <input type="text" name="title" id="title"><br>
    <label for="content">Content: </label>
    <input type="text" name="content" id="content"><br>
    <input type="submit">
  </form>
```

input 받기 위한 html 필요 → DB가기 위해 함수로 바꾼다. → 잘된 경우 잘되었다는 것을 알려주는 html 필요

```python
from django.urls import path
from . import views

app_name = 'articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'), # 여기서 name을 써줘야 url 'articles:create' 사용 가능
]
```

### ✨get

```python
def create(request):
    # 사용자의 데이터를 받아서
    title = request.GET.get('title')      # GET을 받아서 get으로 한개의 값을 넣어준다.
    content = request.GET.get('content')

    # DB에 저장
    # 1
    article = Article()
    article.title = title
    article.content = content
    article.save()

    # 2
    article = Article(title=title, content=content)  # 변수값에 할당 해준다.
    article.save()

    # 3
    Article.objects.create(title=title, content=content)

    return render(request, 'articles/create.html')
🍟# -> http://127.0.0.1:8000/articles/create/?title : create경로로 가게된다.
		# 새로운 요청을 하기 위해서 redirect를 사용한다.
		from django.shortcuts import render, redirect
		return redirect('articles:index')
🍟# -> "GET /articles/create/?title=~~~ HTTP/1.1" 302 0
		# 이후 경로는 안없애고 create.html은 없애도 된다. 
		# 경로는 사용해야 되므로~
```

### ✨ post방식(get처럼 log가 뜨지 않게 하기 위해서)

```python
{% csrf_token %}  # post 보낼때
```

- CSRF (Cross-Site-Request-Forgery 준말)
    - 사이트 간 요청 위조(2008년 옥션 개인정보 해킹 사건)
    
    ```python
    <h1>NEW</h1>
      <form action="{% url 'articles:create' %}" method="POST">
        {% csrf_token %} # -> 이 태그가 있을 때만 post시켜 주겠다.
        <label for="title">Title: </label>
        <input type="text" name="title" id="title"><br>
        <label for="content">Content: </label>
        <input type="text" name="content" id="content"><br>
        <input type="submit">
      </form>
    ```
    

### detail page

- 개별 게시글 상세 페이지 제작
- url → view → template

2개씩 설치하는 것 : update, create

- usl

```python
app_name = 'articles'
urlpatterns = [
    path('', views.index, name='index'),
    path('new/', views.new, name='new'),
    path('create/', views.create, name='create'),
    path('<int:pk>/', views.detail, name='detail'),
    path('<int:pk>/delete/', views.delete, name='delete'),   
    path('<int:pk>/edit/', views.edit, name='edit'),
    path('<int:pk>/update/', views.update, name='update'),
    ]
```

- view

```python
def create(request):
    # 사용자의 데이터를 받아서
    title = request.POST.get('title')
    content = request.POST.get('content')
    # print('서버 도착','title,content')
    # DB에 저장
    # 1
    # article = Article()
    # article.title = title
    # article.content = content
    # article.save()

    # 2
    article = Article(title=title, content=content)
    article.save()

    # 3
    # Article.objects.create(title=title, content=content)

    return redirect('articles:detail', article.pk)
    
def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')

def detail(request, pk):
    article = Article.objects.get(pk=pk)
    context ={
        'article':article,
    }
    return render(request, 'articles/detail.html', context)

def edit(request, pk):
    article = Article.objects.get(pk=pk)
    context = {
        'article':article,
    }
    return render(request, 'articles/edit.html', context)

def update(request, pk):
    article = Article.objects.get(pk=pk)
    article.title = request.POST.get('title')
    article.content = request.POST.get('content')
    article.save()
    return redirect('articles:detail',article.pk)
```

- admin 관리

`python [manage.py](http://manage.py/) createsuperuser`

아이디 , 이메일, 비번 등록