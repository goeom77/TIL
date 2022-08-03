## markdown

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
        - 취소:’~~글자~~’
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
        - ![깃로고 이미지 가져오기]([http://git-scm.com/images/logo@2x.png](http://git-scm.com/images/logo@2x.png))
    - 인용(Blockquate) → “토글이었다.”
        - 주석이나 인용문구를 표현
        - >를 사용함. 갯수에 따라 중첩이 가능
        - >>>는 중첩된 상태로 시작할 경우
    - 표(table) → 노션에서는 안되는 듯
        - 테이블 양쪽 끝의 파이프(|)는 생략가능함
        - 타이포라에서는 ctrl + T를 활용하여 쉽게 표 생성
        - `파이프(|)`과 `하이픈(-)`를 이용해서 행고 열을 구분
        - 행을 늘릴때는 ctrl +enter를 누름
        
        [제목 없음](https://www.notion.so/28561f62fff241eaac5cc13acff8df56)
        
    - 수평선(Horizontal Rule)
        - 구분선 생성
        - -*_를 3번이상 연속으로 작성(노션은 -)
        - 작성법
        
        ---