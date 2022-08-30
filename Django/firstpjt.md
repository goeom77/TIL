# 20220830

복습: No
유형: janggo
작성일시: 2022년 8월 29일 오전 5:33

## 🎨 Django

### ✨Intro

- webservice : server(온라인 쇼핑몰) , client(고객),
    1. 접속했을 때 보이는 페이지 : index 페이지
    2. 환영인사, login → submit → (ascending info → DB) → 양방향의 정보 → 새 페이지 return
- Flask, Django → 상업적으로 장고를 더 많이 사용한다. (규약이 많고, 보안이 좋기 때문)
ex) 인스타그램
- 웹페이지
    - 정적 웹 페이지(Static Web page) : 있는 그래도 제공하는 것(ex : 나무위키)
    - 동적 웹 페이지(Dynamic Web page) : 사용자의 요청에 따라 웹 페이지에 추가적인 수정이 되어 클라이언트에게 전달되는 웹 페이지 → 수정을 해주는 주체 : 서버 → 사용자 요청을 받아 적절한 응답을 만들어 주는 프로그램을 쉽게 만드는 프레임워크 : Django

### ✨장고 구조(MTV)

- 자주 사용하게 되는 구조와 해결책이 있다.
- MTV패턴은 MVC 디자인 패턴을 기반으로 변형된 패턴이다.

- MVC 패턴
    - Model : 데이터와 관련된 로직을 관리
    - View : 레이아웃과 화면을 처리
    - Controller : 명령을 mode과 view 부분으로 연결
    - 각 부분을 독립적으로 개발할 수 있어, 하나를 수정하고 싶을 때 모두 건들지 않아도 된다.
        
        
        | MVC | MTV |
        | --- | --- |
        | Model | Model |
        | View | Template |
        | Controller | View |

![캡처.PNG](20220830%20595849cddc634ac7839b103c03051733/%25EC%25BA%25A1%25EC%25B2%2598.png)

1. URLS : 어떤 페이지를 보낼지 경로를 결정
2. template : 새로운 html 만들어주기
3. view : 만든 html을 내보내기

### ✨장고 설치

- Django, Exel viewer을 vs코드 확장자에 열기(Server가 없는 경우)
- 설정 코드 작성

```python
// settings.json

{
  ... 생략 ...,

  // Django
  **"files.associations": {
    "**/*.html": "html",
	    "**/templates/**/*.html": "django-html",
    "**/templates/**/*": "django-txt",
    "**/requirements{/**,*}.{txt,in}": "pip-requirements"
  },
  "emmet.includeLanguages": {
    "django-html": "html"
  }**
}
```

- 가상환경 실무에서는 : 장고용 가상환경, 플라스크용 가상환경, 이런식으로 설정
- but 연습하기 위해서 프로젝트 단위로 가상환경을 설치할 것
- 가상환경 제작방법

```python
python -m venv {가상환경 이름}              # 새로운 가상환경 생성(디렉터리)
source {가상환경 이름}/Scripts/activate     # 가상환경 들어가기
deativate                                  # 가상환경에서 나가기

cd {가상환경 이름}                          # 가상환경 들어가기 2
source Scripts/activate

pip install django                         # 이대로 누르면 django 4.1버전이 깔린다.
pip install django==3.2.15                 # LTSversion 사용

pip list                                   # 버전을 확인할 수 있다.
pip freeze > requirements.txt              # 패키지 목록 생성
pip install -r requirements.txt            # 버전에 맞는 패키지 한번에 설치해준다.

# 멕킨더시에서는 Scripts가 아니라 bin파일이 열린다.
```

- version 중 관리를 계속 해주는 것 : LTS 버전

```python
django-admin startproject firstpjt .       # project 이름에는 -사용불가
# .을 붙이지 않은 경우 현재 디렉토리에 프로젝트 디렉토리를 새로 생성

python manage.py runserver                 # 서버 실행
ctrl + c                                   # 서버 종료
```

🍟프로젝트

- `__**[init__**.py](http://init.py)` : python에게 이 디렉토리를 하나의 python패키지를 다루도록 지시(별도 추가 코드 x)
- [`asgi.py`](http://asgi.py) : *Asychronous Server Gateway Interface*, Django 애플리케이션이 비동기식 웹서버와 연결및 소통을 도움, 추후 배포시에 사용한다.
- [`setting.py`](http://setting.py) : Django 프로젝트 설정을 관리
- [`urls.py`](http://urls.py) : 사이트의 url과 적절한 view의 연결을 지정 ( 가장 많이 신경)
- [`wsgi.py`](http://wsgi.py) : Web Server Gateway Interfere, Django 애플리케이션이 웹서버와 연결 및 소통 도움
- [`manage.py`](http://manage.py) : Django 프로젝트와 다양한 방법으로 상호작용 하는 커맨드라인 유틸리티

```python
# manage.py Usage
python manage.py <command> [options]

#애플리케이션 생성
python manage.py startapp {애플리케이션 이름}
```

🍟애플리케이션

- `__**[init__**.py](http://init.py)` : python에게 이 디렉토리를 하나의 python패키지를 다루도록 지시(별도 추가 코드 x)
- [`admin.py`](http://admin.py) : 관리자용 페이지를 설정
- `[apps.py](http://apps.py)` : 앱의 정보가 작성된 곳, 별도의 추가 코드를 작성하지 않음
- `[models.py](http://models.py)` : 애플리케이션에서 사용하는 model을 정의하는 곳 MTV의 M에 해당
- `[test.py](http://test.py)` : 프로젝트의 테스트 코드를 작성하는 곳
- `[views.py](http://views.py)` : view 함수들이 정의 되는 곳,  MTV패턴의 V에 해당

app만든 후 프로젝트에서 setting의 33번째 installed_apps에 새로운 애플리케이션을 더해줘야 한다.
→ local apps, Third party apps, Django apps 순서로 하는 것을 권장.

### ✨요청과 응답

- URL → VIEW → TEMPLATE순의 작성 순서로 코드 작성
    
    ![캡처.PNG](20220830%20595849cddc634ac7839b103c03051733/%25EC%25BA%25A1%25EC%25B2%2598%201.png)
    
    - index → view.index (함수이름), view에 index라는 함수 사용 → url에 from app import views 가능해진다. → view에서 render에 ‘html이름’ 정의하고 그 이름으로 template에 html 만들기
- \URL → http:주소.port번호/경로/a.html(주로 index는 주소.port번호/index에서 한다.

```python
# urls.py
from django.contrib inport admin
from django.urls import path      # path 함수를 통해서
from articles import views        # app의 views를 import한다. -> views.py에 있어야됨

urlpatterns = [
	path('admin/', admin.site.urls),   # 장고는 경로뒤에 반드시 /를 붙인다.
	path('index/', views.index),       # 장고는 끝에 ,치는 것을 권장한다. 잘못하면 IndexError
]                                    # 매너이자 상대방에 대한 예의다. 위에 버릇!
```

```python
# articles/view.py
def index(request):                    # http request 객체안에 request를 받는데 다른것도 가능
	return render(request, 'index.html') # http요청을 수신하고 http응답을 반환하는 함수 작성
# view에 가면 import render가 있다. http를 장고로 만들어 주는 역할을 한다.
# 보통은 이름이 같은 'index.html'과 같이 만든다.
```

[참고] 추가 설정

- language code

```python
# setting.py
LANGUAGE_CODE = 'ko-kr'
TIME_ZONE = 'Asia/Seoul'
```

- Time_Zone
    - DB연결의 시간대를 나타내는 문자열을 지정
    - USE_TZ가 True이면 새로 설정한 인식 날짜, 시간이 반환되고 False이면 error발생

### ✨Template(DTL)

- 위치 app > template > html 만 Django가 관리한다.
- “데이터 표현을 제어하는 도구이자 표현에 관련된 로직”
- Django Template을 이용한 HTML 정적 부분과 동적 컨텐츠 삽입
- DTL Synytax
    - Variable
    
    ```python
    # {{variable}} -> 변수다 {{list이름.0(idx)}} 
    #articles/views.py
    
    def greeting(request):        # 변수명은 영어, 숫자와, 밑줄의 조합으로 구성될 수 있으나
    # 밀줄로는 시작할수 없다. 공백이나, 구두점 문자 또한 불가
    # .을 사용하여 변수 속성에 접근할 수 있음
    # render()의 세번째 인자로{'key':value}와 같이 딕셔너리 형태로 넘겨주며, 여기서 정의한 key에 해당하는 문자열이 template에서 사용 가능한 변수명이 됨
    		return render(request, 'greeting.html',{'name':'Alice'})
    ```
    
    - Filters
        
        `{{variable|lower}} -> 소문자`
        
    - Tags
        
        `{% %} : for if block 이용할 수 있다.`
        
    - Comments
        
        `{# #}` : 한 줄 주석
        
        `{% comment %}` : 여러 줄 주석  `{% endcomment %}`
        

### ✨상속

- `{% extends {부모템플릿} %}` : ‘자식 탬플릿’이 부모 템플릿을 확장한다는 것을 알림
**→ 반드시 템플릿 최상단에 작성 되어야 함**
- `{% block %}` ~ `{% endblock %}` : ~는 고유 코드를 넣는 영역이다. → 고유 코드와 상속 코드를 병행해서 사용할 수 있다. (Overriding 이라고 부른다.)
- `{% block Eom %}` , `{% block sky %}` 이런 방법으로 block을 여러개 사용할 수 있다.
- 상위의 다른 폴더에  templates를 상속받기 위해서 
setting → templates → ‘dirs’ : [BASE_DIR / ‘templates’], → 만들어진 템플릿을 이용하겠다.
* base.html은 최상위 파일에 templates안에 있어야 적용이 된다.
    
    ![https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-15-20-07-image.png](https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-15-20-07-image.png)
    

### **✨ Sending form data(Client)**

- **✨ HTML `<form>` element**
    - 데이터가 전송되는 방법을 정의
    - 웹에서 사용자 정보를 입력하는 여러 방식(text, button, submit 등)을 제공하고, 사용자로부터 할당된 데이터를 서버로 전송하는 역할을 담당
    - "데이터를 어디(action)로 어떤 방식(method)으로 보낼지"
    - 핵심 속성
        - action
        - method
- **✨ HTML form's attributes**
    1. action
        - 입력 데이터가 전송될 URL을 지정
        - 데이터를 어디로 보낼 것인지 지정하는 것이며 이 값은 반드시 유효한 URL이어야 함
        - 만약 이 속성을 지정하지 않으면 데이터는 현재 form이 있는 페이지의 URL로 보내짐
    
    2- method
    
    - 데이터를 어떻게 보낼 것인지 정의
    - 입력 데이터의 HTTP request methods를 지정
    - HTML form 데이터는 오직 2가지 방법으로만 전송 할 수 있는데 바로 GET 방식과 POST방식
- **✨ HTML `<input>` element**
    - 사용자로부터 데이터를 입력 받기 위해 사용
    - "type" 속성에 따라 동작 방식이 달라진다.
        - input 요소의 동작 방식은 type 특성에 따라 현격히 달라지므로 각각의 type은 별도로 MDN 문서에서 참고하여 사용하도록 함
        - type을 지정하지 않은 경우, 기본값은 "text"
    - 핵심 속성
        - name
- **✨ HTML input's attribute**
    - name
        - form을 통해 데이터를 제출(submit)했을 때 name 속성에 설정된 값을 서버로 전송하고, 서버는 name 속성에 설정된 값을 통해 사용자가 입력한 데이터 값에 접근할 수 있음
        - 주요 용도는 GET/POST 방식으로 서버에 전달하는 파라미터(name은 key, value는 value)로 매핑하는 것
            - GET 방식에서는 URL에서 `'?key=value&key=value/'` 형식으로 데이터를 전달

### **✨ Retrieving the data(server)**

- **✨ Retrieving the data(server)**
    - 데이터 가져오기(검색하기)
    - 서버는 클라이언트로 받은 key-value 쌍의 목록과 같은 데이터를 받게 됨
    - 이러한 목록에 접근하는 방법은 사용하는 특정 프레임워크에 따라 다름
    - 우리는 Django 프레임워크에서 어떻게 데이터를 가져올 수 있을지 알아볼 것
        - throw가 보낸 데이터를 catch에서 가져오기
- **✨ 데이터 가져오기**
    - catch 페이지가 잘 응답되어 출력됨을 확인
    - 그런데 throw 페이지의 form이 보낸 데이터는 어디에 들어 있는 걸까?
        - catch 페이지의 url 확인 `http://127.0.0.1:8000/catch/?message=데이터`
        - GET method로 보내고 있기 때문에 데이터를 서버로 전송할 때 Query String Parameters를 통해 전송
        - 즉, 데이터는 URL에 포함되어 서버로 보내짐
    - 그러면 우리가 작성해야 하는 view 함수에서는 해당 데이터에 어떻게 접근 가능할까?
        - 모든 요청 데이터는 view함수의 첫번째 인자 `request`에 들어있다.

## **6. Django URLs**

### **✨ App URL mapping**

- 앱이 많아졌을 때 urls.py를 각 app에 매핑하는 방법을 이해하기
- 두번째 app인 **pages**를 생성 및 등록 하고 진행
- app의 view함수가 많아지면서 사용하는 path() 또한 많아지고, app 또한 더 많이 작성되기 떄문에 프로젝트의 urls.py에서 모두 관리하는 것은 프로젝트 유지보수에 좋지 않음
- ~~각 앱의 view 함수를 다른 이름으로 import 할 수 있음 -> 안좋은 방법!!~~
- 하나의 프로젝트에 여러 앱이 존재한다면, 각각의 앱 안에 urls.py를 만들고 프로젝트 urls.py에서 각 앱의 urls.py 파일로 URL 매핑을 위탁할 수 있음
- **각각의 app 폴더 안에 urls.py를 작성**하고 다음과 같이 수정 진행
    
    ![https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-17-42-18-image.png](https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-17-42-18-image.png)
    

### **✨ Including other URLconfs (1/2)**

- urlpattern은 언제든지 다른 URLconf 모듈을 포함(include)할 수 있음
- include되는 앱의 url.py에 urlpatterns가 작성되어 있지 않다면 에러가 발생
    - 예를 들어, pages 앱의 urlpatterns가 빈 리스트라도 작성되어 있어야 함
- 이제 메인 페이지의 주소는 이렇게 바뀌었음
    - [http://127.0.0.1:8000/index/](http://127.0.0.1:8000/index/) -> [http://127.0.0.1:8000/articles/index/](http://127.0.0.1:8000/articles/index/)
- include()
    - 다른 URLconf(app1/urls.py)들을 참조할 수 있도록 돕는 함수
    - 함수 include()를 만나게 되면 URL의 그 시점까지 일치하는 부분을 잘라내고, 남은 문자열 부분을 후속 처리를 위해 include된 URLconf로 전달

### **✨ Naming URL patterns**

- 이제는 링크에 URL을 직접 작성하는 것이 아니라 path() 함수의 name 인자를 정의해서 사용
- DTL의 Tag중 하나인 URL 태그를 사용해서 path() 함수에 작성한 name을 사용할 수 있음
- 이를 통해 URL 설정에 정의된 특정한 경로들의 의존성을 제거할 수 있음
- Django는 URL에 이름을 지정하는 방법을 제공함으로써 view 함수와 템플릿에서 특정 주소를 쉽게 참조할 수 있도록 도움
    
    ![https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-17-58-53-image.png](https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-17-58-53-image.png)
    
- Built-in tag - "url"
    - `{% url '' %}`
    - 주어진 URL 패턴 이름 및 선택적 매개 변수와 일치하는 절대 경로 주소를 반환
    - 템플릿에 URL을 하드 코딩하지 않고도 DRY 원칙을 위반하지 않으면서 링크를 출력하는 방법
        
        ![https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-18-00-21-image.png](https://github.com/SeungtaeRyu/TIL/raw/master/Django/Django_01_assets/2022-08-30-18-00-21-image.png)