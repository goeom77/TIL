# Web

복습: No
작성일시: 2022년 8월 5일 오후 4:55

## 🎈단축키

```html
art + shift + 화살표 : 복사
ctrl + b : 왼쪽 창 삭제
ctrl + art + 화살표 : 적는 커서 추가
Lorem : 아무글자 배열
div#id명 : id 생성
div.클래스명 : 클래스 생성
art + 마우스 클릭 : 커서 병렬 수행
art + z : 자동 줄 바꾸기
shift + 스크롤 : 화면 좌우로 움직이기
```

## ✨Web

- 구조 : HTML(구조), CSS(표현), JAVASCRIPT(동작)
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598.png)
    
- 참고 사이트
    - can i use : 사용할 수 있는 것 확인
    - MDN web docs : https://developer.mozilla.org/ko/
    - 개발자 도구 활용법 : https://developer.chrome.com/docs/devtools/css/
    - Emmet : HTML과 CSS 작성시 빠른 마크업용

## ✨HTML

: Hyper Text Markup Language(비 선형적인 텍스트)

```html
Hyper Text :  참조(하이퍼링크)를 통해 사용자가 한 문서에서 
							다른 문서로 즉시 접근할 수 있는 텍스트
Markup Language : 태그 등을 이용하여 문서나 데이터의 구조를
									명시하는 언어 (ex: HTML, Mark Down)
```

- 기본 구조 : Head , Body
    - Head : 문서 레벨 메타 데이터 요소<meta>, 문서 제목<title>, 스크립트요소<script>, 외부파일 로딩<link>,css<style>
    
    ```html
    title: 브라우저 상단 타이틀
    meta : 문서 레벨 메타데이터 요소
    link : 외부 리소스 연결 요소(css파일, favicon 등)
    script : 스크립트 요소(JavaScript 파일/코드)
    style : CSS직접 작성
    ```
    
    - Body : 실제 화면 구성과 관련 내용
- 태그
    - 내용이 없는 태그 : br, hr, img, input, link, meta
    - 사이트 검사를 통해 1회성으로 고칠 수 있다.
- 속성
    - 사용할 때 띄어쓰기 사용 x, “”쌍따움표 사용
    
    ```html
    id : 문서 전체에서 유일한 고유 식별자 지정 -> css에서 사용
    class : 공백으로 구성된 해당 요소의 클래스 목록
    data-* : 페이지에 개인 사용자 정의 데이터를 저장하는 위해 사용
    style : 
    
    주석 : <!-- -->
    ```
    
- 시맨틱 태그 : 의미적 가치를 가지는 것(공간도 가진다) → 공간이 자동 배열되지는 X
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%201.png)
    
    사용 이유 
    
    - 개발자 및 ㅏㅅ용자 뿐만 아니라 검색엔진 등에 의미 있는 정보의 그룹을 태그로 표현
    - 단순히 구역을 나누는 것 뿐만 아니라 의미를 가지는 태그들을 활용하기 위해
    - 요소의 의미가 명확해지기 때문에 코드의 가독성을 높이고 유지보수 쉽게함
    - 검색 엔진 최적화(SEO)를 위해서 메타태그, 시맨틱 태그를 통한 마크업 효과적 활용
- 렌더링 : 웹사이트를 그림체로 보여주는 과정
    - Dom(Document Object Model)트리
- HTML 요소
    - 인라인 요소 : 글자처럼 취급
    - 블록 요소 : 한 줄 모두 사용
        - 텍스트 요소
            
            ```python
            <a> : href 속성을 활용하여 다른 URL로 연결
            <b> : 굵은 글씨요소
            <strong> : 중요 강조하고자 하는 요소(굵은 글씨)
            <i> : 기울임 글씨요소
            <em> : 중요 강조하고자 하는 요소(기울임 글씨)
            <br> : 줄바꿈
            <img> : src속성 활용 이미지 표현
            <span> : 의미 없는 인라인 컨테이너
            <p> 하나의 문단(paragraph)
            <hr> : 문단 레벨 요소에서 주제의 의미하며 수평선으로 표현
            <ol> : 순서가 있는 리스트 -> 1. # 자식 -> li 사용
            <ul> : 순서 없는 리스트 -> 점 # 자식 -> li 사용
            <pre> : Html 작성한 내용을 그대로 표현
            <blockqueote> : 텍스트가 긴 인용문, 주로 들여쓰기 표현
            <div> : 의미 없는 블록 레벨 컨테이너
            ```
            
- Form
    
     : <form>은 정보를 서버에 제출하기 위해 사용하는 태그(ID/Pw)
    
    - 기본 속성
    - action : form 처리할 서버의 URL(데이터를 보낼 곳)
    - method : form을 제출할 때 사용할 HTTP 메소드(get 혹은 post)
    - enctype : method가 post인 경우 데이터의 유형
        - application/x=www-form-urlencoded : 기본값
        - multipart/form-data : 파일 전송시 (input type이 file 인경우)
- Select
    - 내부가 필수로 선택해야되면 required사용
    - 선택 사항을 만드는 것 Option사용
    
    ```html
    <div>
    	<label for="region">지역을 선택해주세요.</label><br>
    	<select name="region" id="region" required>
    		<option value="서울">서울</option>
    		<option value="강원"disabled>강원</option>
    	</select>
    </div>
    ```
    
- Input
    
     : 다양한 타입을 가지는 입력 데이터의 유형과 위젯이 제공됨
    
    - name: form control에 적용되는 이름(이름/값 페어로 전송)
    - value : form control에 적용되는 값(이름/ 값 페어로 전송)
    - required, readonly, autofocus, autocomplete,disabled 등
    
    ```html
    <form action="/search" method="GET">
    	<input type="text" name="q"> <!--http상에서 q="적은 내용"으로 저장되어 전송-->
    </form>
    ```
    
- Input label: label을 클릭하여 input자체에 초점을 맞추거나 활성화
    
    ```html
    <label for="agreement">개인정보 수집에 동의합니다.</label>
    <input type="checkbox" name="agreement" id="agreement" 
    place holder = "안에 적을것" value = "안에 적을것">
    # label
    # 아이디 __input__
    # for ID 대입
    # input 내에 글자 기입
    <input 못 쓰게 할때 뒤에 disabled>
    ```
    
    - text :일반 텍스트 입력
    - password: 입력 시 값이 보이지 않고 * 로 표현
    - email: 이메일 형식이 아닌 경우 form제출 불가
    - number : min,max,step속성을 활용하여 사용
    - file : 속성을 이용해서 사용
    - checkbox : 다중 선택 / radio button : 단일 선택
        
        ```html
        <p>checkbox</p>
        <input id="html" type= "checkbox" name="language" value = "html">
        ```
        
        ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%202.png)
        
    - color : color picker
    - date : date picker
    - hidden : 사용자에게 보이지 않는 input
        
        ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%203.png)
        
    
    input 공부 참조 : https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input
    
    >>html에서는 태그 + 클래스 등 = css에서 선택자라 부른다.
    

## ✨CSS

: Cascading Style Sheets(스타일을 지정하기 위한 언어)

- 구조

```html
h1{ #선택자(Selector)
	color: blue; #선언(Declaration)
	font-size: 15px; # 속성(property): 값(Value);
```

- 정의 방법:
    - 인라인(inline)
    
    ```python
    <h2 style="color:blueviolet; font-size: 100px";>
    ```
    
    - 내부 참조(embedding) → 처음에 사용하는 방법
    
    ```python
    <style>
    	h1{
    			color: red;
    			font-size: 40px
    	}
    </style>
    ```
    
    - 외부 참조 → 가장 많이 사용하는 방법
    
    ```python
    외부에 mystyle.css 생성 -> link로 연결
    p{
    	color: pink;
    	font-size: 16px;
    }
    
    내부에 link tab-> <link rel="stylesheet" href="mystyle.css">
    ```
    
- 선택자 : 원하는 개수를 특정하는 것, 넓은 것은 상속된다.
    - 요소(서울사람) → HTML 태그를 직접 선택
    
    ```python
    <style>
    	# 전체 선택자
    	*{
    		color: red;
    	}
    	# 요소 선택자
    	h2,h3{
    		color: orange;
    	}
    </style>
    ```
    
    - 클래스(최씨, 이씨) → 마침표(.)문자로 시작하며, 해당 클래스가 적용된 항목 선택
    
    ```python
    <style>
    	# 클래스 선택자
    	.green{
    	color: green;
    	}
    	# id 선택자
    	#purple {
    		color: purple;
    	}
    	# 자식 선택자
    	.box > p{
    		font-size: 30px;
    	}
    	# 자손 집합자
    	.box p{
    		color: blue;
    	}
    </style>
    <h1 class="green">SSAFY</h1>
    # 위에 선택자에 의해 자동적으로 green이 된다.
    <div class="green box">
    	box contents
    		<div>
    			<p> 지역 목록 </p>
    			<ul>
    				<li>서울</li>
    				<li id="purple">인천</li>
    			</ul>
    		</div>
    ```
    
    - id 선택자
        
         #문자로 시작하며, 해당 아이디가 적용된 항목을 선택
        
        일반적으로 하나의 문서에 1번만 사용
        
        여러번 사용해도 동작하지만, 단일 id를 사용하는 것을 권장
        
- 우선순위
    1. 중요도(importance) - 사용시 주의
        1. !important
    2. 우선순위
        1. important> 인라인(style) > id, 속성, pseudo-class>요소,pseudo-element>속성설정순서
- 상속
    - 상속되는 것 : Text관련 요소(font, color, text-align),opacity, visibility등
    - 상속 안되는 것: 박스모델 관련 요소: width, height, margin, padding, box-sizing, display,text-align
        
        position관련 요소 : position, top/right/bottom/left,z-index
        
- 크기 단위
    - class= “em” : 상속에 영향을 받음
    - class= “rem”: 상속에 영향을 받지 않음(최상위(html)의 사이즈를 기준)
        
        ```python
        <ul class="font-big"> #font-size: 16px(b)
                <li class="em">2em</li>  #font-size: 상속받아 16px(b)*2 
                <li class="rem">2rem</li> #font-size: 상속x 8px2
                <li>no class</li> #font-size: 36px(b)
            </ul>
        ```
        
    - no class
    - vw, vh, vmin, vmax: 창의 크기에 따라 크기가 변한다.

- 색상 단위
    - 대소문자 구분 x
    - 특정 색을 직접 글자로 나타냄
    - RGB : (background-color: rgb(0,255,0);)
    - HSL : (background-color: hsl(0,100%, 50%);) # 색상, 채도, 명도
    - 참고 : rgba, hsla → a:투명도 / obacity : 0.8 로 사용도 가능

차후 공부 :!! 잘 쓰이는 것 서체, 서체스타일, 자간, 단어간격, 행간, 컬러, 배경, 목록, 표

- 결합자(Combinators)
    - 자손결합자
        
        selectorA 하위의 모든 selectorB 요소
        
        ```python
        <div># 1 level 1,3사이 자손 div span{color:red;}
        	<span> 빨강입니다.</span> # 2 level 같은 레벨은 형제 결합자
        	<p>이건 빨강이 아닙니다.</p> # 2 level
        	<p>
        		<span> 빨강입니다.</span> # 3 level
        	</p>
        ```
        
    - 자식결합자(>)
        
        selectorA 바로 아래의 selectorB요소
        
        ```python
        <div> # div>span{color:red;}
        	<span> 이건 빨강입니다.</span>
        	<p> 이건 빨강 아닙니다.</p>
        	<P>
        		<span> 이건 빨강 아닙니다.</p>
        ```
        
    - 일반 형제 결합자(~)
        
        selectorA의 형제 요소 중 뒤에 위치하는 selectorB 요소를 모두 선택
        
        ```html
        <span> 빨강이 아닙니다.</span> # p~span{color:red;}
        <p> 문장 </p>
        <b> 코드 </b>
        <span> 빨강입니다.</span>
        <b></b>
        <span> 빨강입니다.</span>
        ```
        
    - 인접 형제 결합자(+)
        
        selectorA의 형제 요소 중 바로 뒤에 위치하는 selectorB 요소를 선택(뒤에것만 적용)
        
        ```html
        <span>빨강이 아닙니다.</span> # p+span{color:red;}
        <p></p>
        <span>빨강입니다.</span>
        <b></b>
        <span>빨강이 아닙니다.</span>
        ```
        
- Box Model
    
    :모든 요소는 네모(박스모델)이고, 위에서부터 아래로, 왼쪽에서 오른쪽으로 쌓인다!!
    
- box-sizing
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%204.png)
    
    - content-box
        
        : 실제로 contents영역만을 box로 지정
        
    - border-box
        
        : border까지의 너비를 100px 로 맞추는 것
        
- 내용과 보더 사이 공간 : padding이라고 한다.
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%205.png)
    
    margin> border> padding> 내용
    
    ```python
    margin-padding{
    	margin: 10px;
    	padding: 30px;
    } #상하좌우 모두 10px이다!
    margin:10px 20px; # 상하 좌우
    margin:10px 20px 30px # 상 좌우 하
    margin:10px 20px 30px 40px # 상 우 하 좌
    ```
    
    ```python
    #밖에서 설정
    .border{
    	border-width:2px;
    	border-style: dashed;
    	border-color: black;
    }
    #안에서 해주는것
    .box2 {
    	border: 2px solid black; # border-width,style,color
    }
    ```
    
    기본 사이즈 = content-box(외부 박스 100px ) vs border-box content (내부박스 100px)
    
- display
    - display: block(너무 커)
        - 줄바꿈이 일어나는 요소
        - 화면 크기 전체의 가로폭을 차지
        - 블록 레벨 요소 안에 인라인 레벨 요소가 들어갈 수 있음
        - 레벨 요소 : div/ul, ol/p/hr/form
        - 너비를 가질수 없다면 자동으로 지정
        - 기본 너비 : 가질수 있는 너비의 100%/ 가질수 없는 곳은 자동으로 margin처리
    - display: inline(작아)
        - 줄 바꿈이 일어나지 않는 행의 일부 요소
        - content 너비만큼 가로 폭을 차지한다.
        - width, height, margin-top, margin-bottom지정 못한다.
        - 상하여백은 line-height로 지정
        - 레벨 요소 : span/a/ing/input, label/b,em,i,strong등
        - inline의 기본 너비는 컨텐츠 영역만큼 (글자 크기만큼만)
    - margin-right: auto;   text-align: left;
    - margin-left: auto;    text-align: right;
    - margin-left : auto; margin-right : auto; / text-align : center
- Display
    - display: inline-block
        - block과 inline 레벨 요소를 모두 가짐
        - inline처럼 한줄에 표시할 수 있고, block처럼 width,height,margin속성을 지정 가능
    - dispaly: none
        - 해당 요소를 화면에 표시하지 않고, 공간조차 부여하지 않음
        - 유사한것 : {visibility : hidden}은 해당요소가 공간을 차지하나 화면에 표시만 안하는 것
        - None 숨겨져 있는것(보여줄일 없다.)
        - hidden 숨겨져 있는것(보여줄일 있다.)
- position
    - static : 모든 태그의 기본값
    - relative : 상대 위치
        - 자기 자신의 static 위치를 기준으로 이동(normal flow유지)
        - 브라우저를 기준 (있다고 가정하고 비워둔다) 위치를 차지
    - absolute : 절대 위치( 부모기준 static 아닌 것)
        - 위치를 차지하지 않음
        - static이 아닌 가장 가까이 있는 부모/조상 요소를 기준으로 이동
        - 위에 사항이 없는 경우 브라우저 화면 기준으로 이동
    - fixed : 고정 위치
        - 위치를 차지하지 않음
        - 스크롤 시에도 항상 같은 곳에 위치
    - sticky : 스크롤에 따라 static → fixed로 변경
        - 속성을 적용한 박스는 평소 문서 안에서는 static상태지만 스크롤이 임계점 위치에 이르면 fixed와 같이 박스를 화면 고정하는 속성
    - 종류별 기준
    
    ```html
    모든 요소의 기본은 좌측 상단에 배치
    display에 따라 크기와 배치가 달라진다.
    relative : 본인의 원래 위치
    absolute : 특정 부모의 위치
    fixed : 화면의 위치
    sticky: 본인의 원래 위치 -> 화면의 위치
    ```
    

head 안에 내부참조 넣는다. title은 위에 창에 뜨는 이름을 의미

서버까지 input 넣는 방법 : input, label ⇒ form ⇒ server

## ✨Layout

Display, Position, Float(1996), Flexbox(2012), Grid(2017)

- 구조(위에서 아래로, 왼쪽에서 오른쪽으로 쌓인다)
    - Inline Direction(글자처럼 인식) →
    - Block Direction(블록처럼 인식) ↓
- Float
    - 생성 배경 : 텍스트 포함 인라인 요소들이 주변을 wrapping하도록 함
    - 요소가 Normal Flow를 벗어나도록 함
    - None: 기본값, left : 요소를 왼쪽으로 띄움, right : 요소를 오른쪽으로 띄움
- Flexbox
    - 생각 흐름 : 주축의 방향설정 → 넘치는거 넘길지 → 어느 방향에 정렬할지
    
    ```html
    기본 속성 : None
    left : 왼쪽으로 띄움
    right : 오른쪽으로 띄움
    ```
    
    - display: flex;
    flex-direction: row-reverse(오른쪽에서 왼쪽으로), column-reverse(위로), row, column
        
        → 주축의 방향을 설정
        
        ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%206.png)
        
    - 축 관리(div 내 div할때 방향을 나누는 기준)
        - → main axis : justify로 정렬
        - ↓ cross axis : align으로 정렬
    - 요소
        - flex container(부모 요소) # 감싸는  div
        - flex items(자식 요소) #안쪽 div
    - 배치 설정(주의 : 역방향의 경우 HTML 선언 순서와 시각적으로 다르니 유의(웹접근성 영향)
        - flex-direction
            
            ex) row, row-reverse, column, column-reverse
            
        - flex-wrap
            
            ex) 컨테이너를 벗어나는 경우 밑의 줄로 가는 것
            
            ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%207.png)
            
            - nowrap:한줄에 배치
            - wrap : 넘치면 그다음줄로 배치
    - 공간 나누기
        - justify-content(메인축 정렬)
            
            ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%208.png)
            
        - align-content(교차축 정렬)
            
            ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%209.png)
            
            → space-around는 2등분하고 각각 간격 같게 : 1:2:1
            
        - align-items(style)
            
            ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2010.png)
            
        - align-self(self하나만 정렬하기) → align-items 것 다 사용
            
            ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2011.png)
            
    - 기타 속성
        - flex-grow : 남은 영역을 아이템에 분배
        - order : 배치 순서( 요소의 우선순위를 따진다) → 기본이 0 (개별요소에 순서 지정)
        
    
    **`flex-direction`**과 **`flex-wrap`**이 자주 같이 사용되기 때문에, **`flex-flow`**가 이를 대신할 수 있습니다. 이 속성은 공백문자를 이용하여 두 속성의 값들을 인자로 받습니다.
    
    예를 들어, 요소들을 가로선 상의 여러줄에 걸쳐 정렬하기 위해 **`flex-flow: row wrap`**을 사용할 수 있습니다.
    

## ✨CDN

- head: link, body: script넣기
- spacing(margin and padding)
    - {property}{sides}-{size}
    - <div class=”mt-3 ms-5”>bootstrap-spacing</div>
    - t:top, b:bottom, s:left, e:right, x:left+right, y:top+bottom
    - 0: 0px, 1: 4px, 2: 8px, 3: 16px, 4: 24px, 5: 48px
    - mx-auto:수평중앙정렬, py-0: padding위아래 0

## ✨사이즈마다 보이는 게 다른것

- d-sm: 작을때 보임
- d-md:

## ✨Bootstrap

- Spacing

```html
{property}{sides}-{size}
m(margin),p(padding)
```

![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2012.png)

- property
    - m(margin)
    - p(padding)
- sides
    - t(top)
    - b(bottom)
    - s(start)
    - e(end)
    - x( left+right)
    - y(top + bottom
- size
    - 0 -  0
    - 1 - spacer * 0.25
    - 2 - spacer * 0.5
    - 3 - spacer
    - 4 - spacer * 1.5
    - 5 - spacer * 3
    - auto   ex) 가운데 정렬 = mx-auto
- Grid  system

```html
반드시 기억할 것
1. 12개의 column
2. 6개의 grid break points
```

- Column : 실제 컨텐츠를 포함하는 부분
- Gutter : 칼럼과 칼럼 사이의 공간
- Container : Column들을 담고 있는 공간

목록 검색 → nav bar

사진 넘기는거 → carousel

경고나 창 띄우는거 → modal → top lebel에 넣을 것! → 작동 안할수 있으므로

grid system → 일정 크기 이하 될때까지 크기가 맞춤으로 작아지다가 개수를 줄이는 것(반응형)

→ 반드시 기억 : 12개의 column, 6개의 grid break points(화면 크기를 조정하는 포인트가 6개다)

column : 실제 컨탠츠 포함하는 부분 , gutter: 칼럼과 칼럼 사이 공간, container: 칼럼 담고있는 공간

offset :앞에 공간을 비워두고 싶은경우

- col 쓸 때 유의점 container 안에 row 안에 col 사용할 것
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2013.png)
    
- 사진이 매우 큰 상태인 경우
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2014.png)
    
- 크기조절
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2015.png)
    
- nav 바 만들 때
    
    ![캡처.PNG](Web%2039b571e1d71d4e9d9a6b5d139b36950a/%25EC%25BA%25A1%25EC%25B2%2598%2016.png)