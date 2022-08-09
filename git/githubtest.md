Git 사용 요령
Repository clone하기

바탕화면을 우클릭하여 Git Bash Here 클릭!
터미널에 명령어 git clone https://github.com/al-mong/algorithm_study.git 입력!
레포지터리에 push하기

algorithm_study 폴더에서 우클릭하여 Git Bash Here 클릭!

터미널에 명령어 git pull 입력!

충돌 방지

터미널에 명령어 git status를 입력 후 변경사항 확인!

본인 폴더 외에 변경사항 있으면 안돼요~~

터미널에 명령어 git add . or git add <filename> 입력!

터미널에 명령어 git commit -m "류승태 220726" 커밋 메세지는 이름, 날짜 순으로 입력!

터미널에 명령어 git push origin main 으로 푸쉬 끝!

폴더 작성 법
바탕화면에 생성된 algorithm_study 폴더 열기

본인 영문 이름으로 새 폴더 생성하기 ex) seungtae

본인 폴더 안에 월별 폴더 생성하기 ex) 22_07

월별 폴더 안에 코딩테스트 사이트별 폴더 생성

ex) BOJ, SWEA, programmers 등등... 대/소문자 양식 꼭 맞춰주세요!

각 사이트별 폴더 안에서 문제 번호 당 python파일 작성하기!

# 내가 백준 문제 2822번을 풀 때 폴더 경로

# algorithm_study/seungtae/22_07/BOJ/2822.py
사용 유의사항
다른 스터디원의 폴더를 열면 안 된다!

다른 스터디원의 코드를 참고하고 싶다면 알몽 알고리즘 스터디 Repository를 접속하여 코드 보기!

알몽 레포지터리 링크

본인 작업 후 git status를 입력했을 때 다른사람 폴더의 변경사항이 있다면?

해결법
본인 작업물을 새폴더에 백업한 후 algorithm-study 폴더 삭제 및 다시 clone하기
다른 사람 폴더는 add 하지말고 본인 폴더만 add 하기
잡답 노트
[220727] pull, add, commit, push는 항상 .git이 있는 폴더에서 하는겁니다!