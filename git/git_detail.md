# markdown

- TIL 만들어 보기

  markdown 기능을 이용하면 가독성 up

  - 제목 만들기

    ‘#blank’ 제목

    ‘##blank’ 중제목

    ‘###blank’ 소제목

    *6개까지, ctrl 1~3 이용해서 제목 설정도 가능

  - 목록 만들기

    - 순서가 있는 목록

      ‘1.’space를 이용 → 끝에는 shift tab으로 끝내기

    - 순서가 없는 목록

      ‘-’,*,+space를 사용 → 끝에는 shift tab으로 끝내기

      목록 속의 목록은  tab 이용

  - 강조

    - 기울임: ‘*글자*’
    - 굵게: ‘**글자**’
    - 취소:’글자’
    - 그대로 표시하고 싶은경우 : 1옆의 `사용

  - 코드

    - 인라인 코드

      백틱을 통해 코드를 감싸준다

      - 파이썬에서 출력하려면 print()를 사용한다.

    - 블록 코드

      백틱을 3번 입력한 후 코드의 종류를 작성

      ```python
      print('백틱 + python')
      import random
      numbers = range(1,46)
      lucky = random.sample(numbers, 6)
      ```

  - 링크

    - 클릭하면 해당 주소로 이동
    - [표시할 글자](이동할 주소) 형태로 작성

  - 이미지

    - 절대경로

      - 지정 시 리눅스 등 다른 os사용할 경우 적용안됨

        C:/users/~~→ 다른 os에 없는 경우가 있음

    - 상대경로

      - ./${filename}.assets

        .→현재 파일이 포함된 경로

  - 깃로고

    - ![깃로고 이미지 가져오기](%5B%3Chttp://git-scm.com/images/logo@2x.png%3E%5D(%3Chttp://git-scm.com/images/logo@2x.png%3E))

  - 인용(Blockquate) → “토글이었다.”

    - 주석이나 인용문구를 표현

    - > 를 사용함. 갯수에 따라 중첩이 가능

    - > > > 는 중첩된 상태로 시작할 경우

  - 표(table) → 노션에서는 안되는 듯

    - 테이블 양쪽 끝의 파이프(|)는 생략가능함
    - 타이포라에서는 ctrl + T를 활용하여 쉽게 표 생성
    - `파이프(|)`과 `하이픈(-)`를 이용해서 행고 열을 구분
    - 행을 늘릴때는 ctrl +enter를 누름

  - 수평선(Horizontal Rule)

    - 구분선 생성
    - -*_를 3번이상 연속으로 작성(노션은 -)
    - 작성법

    ------

# git

- lab.ssafy

- 생성 동기

  - 맨 나중 파일만 온전히 유지하고 수정된 파일은 수정과정만 남긴다.

    → 데이터 효율을 위해

- 종류

  - 중앙 집중식 버전 관리
  - 분산 버전 관리

GUI, CLI

- gui : Graphic user interface 그래픽으로
- cli : command line interface
- CSI → CLI,GUI 이용상의 편의를 위해
- 빌게이츠(DOS) → 스티븐잡스(멕킨독스) → 윈도우
- SSAFY@DESKTOP-KVCQHCD MINGW64 ~→ 사용자의 홈 드라이브
- 폴더 > 디랙터리(거의 유사)
- 상대 경로 : 현재 작업 중인 디렉토리 기준으로 계산한 상대적 위치(./이 기준)(../상위 폴더[부호폴더])
- 절대 경로 : 모든 경로

CLI명령어

```python
touch a.txt : 현재 폴더에 a.txt 생성
touch b.txt c.txt : 현재 폴더에 b.txt, c.txt 생성
start .: 현재 파일 켜기
mkdir ‘folder a’ : 현재 폴더에 folder a 폴더 생성
cd .. : 상위폴더로 올라가기
  
cd test : test 파일로 들어가기
    
pwd : 현재 위치
ls : 현재 폴더의 파일 검색
   
ls -ㅣ(L.lower) : 현재 폴더 파일 검색 자세하게
    
mv s.txt ../test : s.txt 를 test파일로 옮기기
rm q.txt : q.txt 파일을 제거
```

## git 기본

- Working Directory - untracked file

  > ^git add(U→C) | git rm(commit→ untracked file)

  ```
  * clone : local에 아무것도 없을 때
  ```

- Staging Area -

- Repository

### git 명령어

```python
git config --global user.name {name}
git config --global user.email {email}
# 내부 파일이 untracted 되어서 git에 의해 관리되어진다.
git add test.txt
# working directory -> staging Area : 어느정도 완성되어서 저장하고 싶을때
git commit -m "1st commit"
# commit: 계약하다 // 이때까지 만든것을 버전1으로 지정하겠다.
# -m : message
git log
# commit된 git 내용 확인
git log --oneline
# commit된 번호 요약해서 안내
git status
# 현재상태
git init
# 현재장소를 저장장소로 지정
clear
# 터미널 clear
local  ———-push——→ Github
     ←—pull / clone—
1. clone : local에 아무것도 없을 때 하는거
2. pull : clone 이후로는 다 pull
git remote add origin <https://github.com/goeom77/test.git>
# git -> local 로 이어지는 다리를 만들어주는 것
git push -u origin master
# 
git push -v
```
