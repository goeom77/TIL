# 20220906

복습: No
작성일시: 2022년 9월 6일 오전 9:05

# Django Form

### 개요

- 사용자로부터 데이터를 받는 방법
    - HTML form
    - input
    - → 이것들은 요청을 모두 수용하고 있다. → 유효성 검증이 필요하다. → 개발 생산성을 늦춘다. → fram work를 사용하자 → Django Form
- 특징
    - 렌더링을 위한 데이터 준비 및 재구성
    - 데이터에 대한 HYML forms 생성
    - 클라이언트로부터 받은 데이터 수신 및 처리

## Django form class

- 특징
    - 주요 유효성 검사도구
    - 공격 및 데이터 손상에 대한 중요한 방어수단
    - 유효성 검사에 대해 개발자에게 강력한 편의를 제공
- class 선언
    - model 선언과 유사하다.
    - 상속을 통해 선언
    
    ```jsx
    # articles/forms.py 헤깔리지 않게 하기 위해서
    from django import forms
    
    class ArticleForm(forms.Form):
        title = forms.CharField(max_length=10)
        # textfield가 존재하지 않는다.
        content = forms.CharField()
    ```
    
    - 쓰던 방식
    
    ```jsx
    {% extends 'base.html' %}
    
    {% block content %}
      <h1>NEW</h1>
      <form action="{% url 'articles:create' %}" method="POST">
        {% csrf_token %}
        <label for="title">Title: </label>
        <input type="text" name="title" id="title"><br>
        <label for="content">Content: </label>
        <textarea name="content" id="content"><br>
        <input type="submit">
      </form>
      <hr>
      <a href="{% url 'articles:index' %}">뒤로가기</a>
    {% endblock content %}
    ```
    
    - 개선 방식
    
    ```jsx
    # view
    from .forms import ArticleForm
    def new(request):
        form = ArticleForm()
        context = {
            'form':form,
        }
        return render(request, 'articles/new.html', context)
    ```
    
    ```jsx
    {% extends 'base.html' %}
    
    {% block content %}
      <h1>NEW</h1>
      <form action="{% url 'articles:create' %}" method="POST">
        {% csrf_token %}
        {{form}}
      </form>
      <hr>
      <a href="{% url 'articles:index' %}">뒤로가기</a>
    {% endblock content %}
    ```
    
    - method `{{form.as_p}}`
    
    ```jsx
    1. as_p() 각 필드가 단락(<p>태그)으로 감싸져서 렌더링
    2. as_ul() 각 필드가 (<li>테그)로 감싸져서 렌더링 -> ul태그는 직접 작성해야한다.
    3. as_table() 각 필드가 테이블(<tr>태그)로 감싸져서 렌더링
    -> 특별한 사항 아니면 1번만 사용할 것 
    ```
    
    - widgets → 텍스트 방식을 바꾸기 위해 → form필드에서 바꿔야한다.
    
    ```jsx
    # articles/forms.py 헤깔리지 않게 하기 위해서
    from django import forms
    
    class ArticleForm(forms.Form):
        title = forms.CharField(max_length=10)
        # textfield가 존재하지 않는다.
        content = forms.CharField(widget=forms.Textarea)
    ```
    
    - widget 종류
    `https://docs.djangoproject.com/ko/3.2/ref/forms/widgets/#built-in-widgets`
    
    ```jsx
    class ArticleForm(forms.Form):
        # django의 스타일 가이드 권장 사항
    		# 아래와 같이 항목을 작성해 줘야 한다.
        NATION_A = 'kr'
        NATION_B = 'ch'
        NATION_C = 'jp'
        NATIONS_CHOICES = [
            (NATION_A,'한국'),
            (NATION_B,'중국'),
            (NATION_C,'일본'),
            ]
        title = forms.CharField(max_length=10)
        # textfield가 존재하지 않는다.
        content = forms.CharField(widget=forms.Textarea)
        nation = forms.ChoiceField(choices=NATIONS_CHOICES,widget=forms.RadioSelect)
    ```
    

## Django Model Form

- 비교
    - model과 forms가 유사한 부분이 많았다.
    - 사용자로부터 입력 받는 수가 많아진다면 두군데 다 많이 써야한다.
    - 만약 모델과 폼이 동일한 자료를 작성한다면 모델을 기반으로 작성하게 만들자
    - 모델에 대한 기본정보를 들고가기 때문에 재정의 할 필요가 없다.
- helper class
    
    ```jsx
    from .models import Article
    class ArticleForm(forms.ModelForm):
    
        class Meta:
            model = # 어떤 모델을 기반으로 할지
            fields = # 어떤 모델 필드 중 어떤것을 출력할지
    									('title','content')
    									'__all__'
    ```
    
    ```jsx
    class ArticleForm(forms.ModelForm):
    # title만 빼고 나머지 다 받을 때는 exclude함수 사용한다.
        class Meta:
            model = Article
            # fields = '__all__'
            exclude = ('title')
    ```
    
- Meta data
    
    데이터를 표현하기 위한 데이터
    
- `model = Article` 의미
    - 함수를 그대로 출력하면 → 함수의 `참조값` 출력
    - 호출을 하면 → 함수의 `반환값` 출력
    - 함수 자체를 그대로 전달해서 필요한 시점에 호출하는 경우 사용한다.
    - url 에서 path(’’, `views.index` ,name=’index’) → 필요한 시점에 호출하는 것

## ModelForm with view functions(view함수의 구조 변화)

- is_valid()
    - 데이터가 유효한지 여부를 boolean으로 반환
    
    ```jsx
    # views.py
    def create(request):
        form = ArticleForm(request.POST)
        # 검증을 하기 위해서 사용한다.
        if form.is_valid():
            article = form.save() # 인스턴스를 지정해서 pk값이 반환되도록 한다.
            return redirect('articles:index', article.pk)
        return redirect('articles:new')
    ```
    
- save()
    - form인스턴스에 바인딩 된 데이터를 통해 DB객체를 만들고 저장
    - modlefom의 하위 클래스는 instance여부를 통해 생성할지, 수정할지 결정한다.
- error
    
    ```jsx
    # create
    def create(request):
        form = ArticleForm(request.POST)
        # 검증을 하기 위해서 사용한다.
        if form.is_valid():
            article = form.save()
            return redirect('articles:index', article.pk)
        # form instance에 errors의 이유를 적어 보낸다.
        print(f'에러: {form.errors}')
        # 공백넣으면 에러가 뜬다.
        return redirect('articles:new')
    ```
    
    에러: <ul class="errorlist"><li>title<ul class="errorlist"><li>필수 항목입니다.</li></ul></li></ul>
    
    ```jsx
    def create(request):
        form = ArticleForm(request.POST)
        # 검증을 하기 위해서 사용한다.
        if form.is_valid():
            article = form.save()
            return redirect('articles:index', article.pk)
        # form instance에 errors의 이유를 적어 보낸다.
        print(f'에러: {form.errors}')
        # 공백넣으면 에러가 뜬다.
        context = {
            'form' : form
        }
        return redirect(request, 'articles/new.html', context)
    		# -> 필수항목이라고 li형식으로 에러메세지가 뜬다.
    ```
    
- 팝업창 넣는 방법
    - input태그에 required 넣어두면 아무것도 안넣었을 때 팝업이 뜨게 된다.
- update
    - model
    
    ```jsx
    def edit(request, pk):
        article = Article.objects.get(pk=pk)
        form = ArticleForm(instance=article)
        # 기존 객체를 넣어주는 것을 instance = article로 대체
        context = {
            'article': article,
        }
        return render(request, 'articles/edit.html', context)
    def update(request, pk):
        article = Article.objects.get(pk=pk)
        form = ArticleForm(requiest.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articleds:detail',article.pk)
        context = {
            'form':form,
        }
        return render(request,'articles/edit.html',context)
    ```
    
    - html
    
    ```jsx
    # edit
    <h1>EDIT</h1>
      <form action="{% url 'articles:update' article.pk %}" method="POST">
        {% csrf_token %}
        {{form.as_p}}
    	</form>
    ```
    
- form vs modelform
    - form : DB와 연관되어 있지 않은 경우
        - 로그인
    - modelform : 데이터를 DB와 연관되어 있는 경우에 사용
        - 회원가입
        - 데이터의 유효성 검사가 끝나면 데이터를 어떤 레코드에 맵핑 해야할지 이미 알기 때문에 곧바로 save()호출이 가능

## widget

- 첫번째 방법(이게 좋아)

```jsx
class ArticleForm(form.MoodelForm):
		class Meta:
				model = Article
				fields = '__all__'
				widgets = {
						'title' : forms.TextInput(attrs={
									
							}
```

- 두번째 방법

```jsx
ㅇㅇ
```

- 사용 예
    
    ```jsx
    class ArticleForm(forms.ModelForm):
        title = forms.CharField(
            label = '제목',
            widget = forms.TextInput(
                attrs={
                    # attributes
                    'class':'my-title',
                    
                    'placeholder':'Enter the title',
                    # 미리 빈칸에 넣어 둘값
                    'maxlength':10,
                    # 유효성 검사를 하지는 않는다. 다만 사용자가 입력하지 못하게 되어있다.
    
                }
            ),
        )
        content = forms.CharField(
            label = '내용',
            widget=forms.Textarea(
                attrs={
                    'class':'my-content',
                    'placeholder' : 'Enter the content',
                    'rows' : 5
                    'cols': 10
                }
            ),
            error_messagers={
                'required':'내용 입력하라고..',
            },
        )
    ```
    

## Handling HTTP requests

- 개요
    - HTTP requests 처리에 따른 view함수 구조 변화
    - new와 create가 합쳐진다.
    - edit와 update가 합쳐진다.
- create

```jsx
#url
path('create/', views.create, name='create'), # GET/POST
```

```jsx
def create(request):
    if request.method == 'POST':
        #create
        form = ArticleForm(request.POST)
        # 검증을 하기 위해서 사용한다.
        if form.is_valid():
            article = form.save()
            return redirect('articles:index', article.pk)
             # form instance에 errors의 이유를 적어 보낸다.
    else:
        #new
        form = ArticleForm()
    context = {
        'form':form,
    }
    return render(request, 'articles/create.html', context)
```

- update

```jsx
# url
path('<int:pk>/update/', views.update, name='update'),  # GET/POST
```

```jsx
def update(request, pk):
    article = Article.objects.get(pk=pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, instance=article)
        if form.is_valid():
            form.save()
            return redirect('articles:detail',article.pk)
    else:
        form = ArticleForm(instance=article)
    # 기존 객체를 넣어주는 것을 instance = article로 대체
    context = {
        'article': article,
        'form':form
    }
    return render(request, 'articles/update.html', context)
```

- delete

```jsx
def delete(request, pk):
    if request.method == 'POST':
        article = Article.objects.get(pk=pk)
        article.delete()
    return redirect('articles:index')
```

GET 형식은 조회에만 사용한다 왜냐하면 url에 다 보이니깐

C : post, R : get , U : put , D : delete 방법마다 다른 방법을 사용하게 할 예정

## View Decorator

- 데코레이터
    - 기존에 작성된 함수에 기능을 추가하고 싶을 때 해당함수를 수정하지 않고 기능을 추가해주는 함수
    
    ```jsx
    def hello(func):
    		def wrapper():
    				print('hihi')
    				func()
    				print('hihi')
    				return wrapper
    @hello
    def bye():
    		print('byebye')
    bye()
    #
    hihi
    byebye
    hihi
    ```
    
- 요청이 들어올 때 GET, POST신경 안쓴다.(모든 요청 받아들인다) → 실제로는 신경 써야한다.

### require_safe()

require_get() 별로 안좋아서 → safe로 사용

: GET요청만 받을것들

```jsx
from django.views.decorators.http import require_safe

@require_safe  # get으로 온것만 받아들여진다.
def index(request):
    # DB에 전체 데이터를 조회
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)
```

### require_http_methods()

: 받아들여지는 것이 2가지 이상일 때 → 생각할 때 없다고 생각하고 짠 뒤에 고려

```jsx
from django.views.decorators.http import require_http_methods

@require_http_methods(['GET','POST'])
def create(request):
    if request.method == 'POST':
        #create
        form = ArticleForm(request.POST)
        # 검증을 하기 위해서 사용한다.
        if form.is_valid():
            article = form.save()
            return redirect('articles:index', article.pk)
             # form instance에 errors의 이유를 적어 보낸다.
    else: # GET일때만 받아들여진다.
        #new
        form = ArticleForm()
    context = {
        'form':form,
    }
    return render(request, 'articles/create.html', context)
```

### require_POST()

```jsx
from django.views.decorators.http import require_http_methods, require_POST

@require_POST
def delete(request, pk):
    if request.method == 'POST':
        article = Article.objects.get(pk=pk)
        article.delete()
    return redirect('articles:index')
```

## Rendering Fields manually

[Working with forms | Django documentation | Django](https://docs.djangoproject.com/en/4.1/topics/forms/)

→ 수동으로 form을 만드는것

```jsx
<h2>수동으로 Form 작성</h2>
  <form action="#">
    <div>
      {{form.title.errors}}
      {{form.title.label_tag}}
      {{form.title}}
    </div>
    <div>
      {{form.content.errors}}
      {{form.content.label_tag}}
      {{form.content}}
    </div>
  </form>
```

### Looping over the form’s fields

반복하는것

```jsx
<h2>Looping</h2>
  <form action="#">
    {% for field in form %}
      {{form.errors}}
      {{form.label_tag}}
      {{form}}
    {% endfor %}
  </form>
```

꾸밀때 bootstrap , djangobootstrap v5 → 따로 설치 필요 pip

## Authentication System

### 개요

- buil-in에 이미 추가 되어있다.
- Authoentication(인증) → 이거에 대해 학습
    - 신원 확인
    - 사용자가 자신이 누구인지 확인
- Authorization(권한, 허가)
    - 권한 부여
    - 인증된 사용자가 수행할 수 있는 작업을 결정
- Django → admin, staff, 일반
- 인증의 app_name : accounts→안하면 추가 설정 필요 할수도?

### accounts

- build-in User model의 기본 인증 요구사항이 적절하지 않을 수 있음
    
    → 언젠가 필요할 수 있으므로 대체하고 시작할 것
    
    → user model을 수정해야하나 쉽지 않은 작업이기 때문
    
- 미리 빼놓고 쓰기! 어디에? accounts/models.py에
- 비록 기본 user모델이 충분하더라도 커스텀 user모델을 설정하는 것을 highly recommended
- 필요한 경우 나중에 맞춤 설정할 수 있기 때문
- 첫 migrate를 실행하기 전에 이 작업을 마쳐야 함!!
- 만약 migrate하고 db가 중요하지 않다면
    1. migrations폴더 및 init만 남기고 번호가 있는 migrations파일 삭제
    2. db.sqlite삭제
    3. makemigrate다시 시행