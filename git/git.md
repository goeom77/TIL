# git

- 생성 동기
    - 맨 나중 파일만 온전히 유지하고 수정된 파일은 수정과정만 남긴다.
        - 데이터 효율을 위해
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

CLI 명령어

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
    > 
    
      * clone : local에 아무것도 없을 때
    
- Staging Area -
- Repository

### git 명령어

```python
git config --global user.name goeom77
git config --global user.email 7eom14@gmail.com
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
```

```python
local  ———-push——→ Github
     ←—pull / clone—
1. clone : local에 아무것도 없을 때 하는거(내가 깃 쓰는 것 하나 위에 파일에)
2. pull : clone 이후로는 다 pull
git remote add origin https://github.com/goeom77/test.git
# git -> local 로 이어지는 다리를 만들어주는 것
git remote rm origin
# 기존 origin 제거
git push -u origin master
# master 로 파일 올리기
git clone https://github.com/goeom77/til.git
#해당 위치에 git저장

#깃 푸쉬된 내용 지우는 방법?
```

순서 : 처음할경우 init -> add -> remote -> commit-> push
두번째 add -> commit -> push

.git → 저장소 위치를 알림