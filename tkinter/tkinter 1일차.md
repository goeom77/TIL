# 20220813

복습: No
유형: tkinter
작성일시: 2022년 8월 13일 오후 11:27
참고: https://076923.github.io/posts/Python-tkinter-4/1/

### 🍓tkinter 사용(css의 적용과 비슷한느낌)

Gui 모듈 : import tkinter

- 사용 방법 : tkinter.*

```python
import tkinter
window=tkinter.Tk()  # 가장 상위 레벨의 윈도우 창을 생성
~  # 이 사이에 위젯을 생성하고 적용한다.
window.mainloop()  # 윈도우 이름의 윈도우 창을 윈도우가 종료될 때 까지 실행시킨다.
```

- 응용

```python
import tkinter
window = tkinter.Tk()

wimdow.title("EOM HYUNG GYU")        # 윈도우 제목을 설정
window.geometry("640x400+100+100")   # 너비x높이 + x좌표 + y좌표 -> 윈도우 너비와 높이
																		 # 초기 화면 위치의 x좌표와 y 좌표 설정
window.resizable(False,False)        # (상하,좌우) 창크기 조절 가능 여부
                                     # True인경우 윈도우 창의 크기를 조절 할수 있다.
                                     # Tip resizeable()적용시 True=1,False=0적용 가능
window.mainloop()
```

- 위젯 배치

```python
import tkinter
window = tkinter.Tk()
wimdow.title("EOM HYUNG GYU")
window.geometry("640x400+100+100")
window.resizable(False,False)
label=tkinter.Label(window, text="안녕하세요.")    #윈도우 창에 label설정
label.pack()                                       # 위젯을 배치
```

- 라벨 사용

```python
label = tkinter.Label(window,text="파이썬",width=10,height=5,fg="red",relief="solid")
label.pack()
```

- 라벨 문자열 설정
    
    ![1.PNG](20220813%20af38c58fee2b4b0d8fb7dff44ce5fe9b/1.png)
    
- 라벨 형태 설정
    
    ![2.PNG](20220813%20af38c58fee2b4b0d8fb7dff44ce5fe9b/2.png)
    

### tkinter - Label

- 라벨 형식 설정
    
    ![3.PNG](20220813%20af38c58fee2b4b0d8fb7dff44ce5fe9b/3.png)
    
- 라벨 상태 설정
    
    ![4.PNG](20220813%20af38c58fee2b4b0d8fb7dff44ce5fe9b/4.png)
    
- 라벨 하이라이트 설정
    
    ![5.PNG](20220813%20af38c58fee2b4b0d8fb7dff44ce5fe9b/5.png)
    

### tkinter - Button

- 버튼을 이용하여 메서드 또는 함수 등을 실행시키기 위한 단추를 생성할 수 있다.

```python
import tkinter

window=tkinter.Tk()
window.title("EOM HYUNG GYU")
window.geometry('640*400+100+100")
window.resizable(False,False)

count =0
def countUP():   # 사용자 정의 함수
	global count
	count += 1
	label.config(text=str(count))

label = tkinter.Label(window, text="0")
label.pack()
																															↓함수 쓸때 사용
button = tkinter.Button(window, overrelief="solid",width=15, command=countUP,
repeatdelay=1000, repeatinterval=100)
# tkinet.Button(윈도우창, 매개변수1,매개변수2,...)을 사용해 윈도우 창에 버튼의 속성설정
# 매개변수에 command사용해 사용자 정의 함수:countUP등을 실행할 수 있다.
button.pack()

window.mainloop()
```

button method

```python
invoke() : 버튼의 실행 # 버튼을 클릭할때와 동일한 실행
flash() : 깜빡임 # 상태 배경 색상과 active 상태 배경 색상 사이에서 깜빡인다.
```

** 버튼은 라벨의 형식, 상태, 하이라이트의 설정을 따라간다.

### Entry(기입창)

: `Entry`을 이용하여 텍스트를 입력받거나 추력하기 위한 기입창을 생성할 수 있다.

```python
import tkinter
from math import *

window = tkinter.Tk()
window.tiltle("EOM HYUNG GYU")
window.geometry("640x480+100+100")
window.resizable(False,False)

def calc(event):
	label.config(text="결과="+str(ecal(entry.get()))

entry=tkinter.Entry(window)
#tkinter.Entry(윈도우창,매개변수1,매개변수2..)를 사용해 윈도우창에 표시할 기입창의 속성 설정
entry.bind("<Return>",calc)
#entry.bind()를 이용해 key나 mouse등의 event를 처리해 메서드나 함수 실행
entry.pack()

window.mainloop()
```