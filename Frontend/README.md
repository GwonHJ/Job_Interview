1. 프론트엔드를 구성하는 세가지 기술 언어
    - HTML : 웹 페이지 문서 담당 (구조)
    - CSS : 웹 페이지 디자인 담당 (표현)
    - JS(Java Script) : 웹 페이지 이벤트 담당 (동작)
2. CSS 포지셔닝, Display 이해
    - width, height
        - length(길이 값) : px, pt, cm, mm, in등의 길이단위 사용
        - 백분율(%) : 상위 block에 대한 백분율 단위로 상위 block의 크기가 바뀌면 자신의 크기도 자동으로 변경
        - auto (width의 경우) : 100%, 자신의 상위 block이 허용하는 width크기만큼 채운다.
        - auto (height의 경우) : 0%, 이 경우 height를 결정하는 요인은 block box속의 내용물의 크기가 된다.
    - position
        - static  : 기본(default)값으로 일반적인 내용물의 흐름. 상단(top)과 좌측(left)에서의 거리를 지정할 수 없다.
        - relative : HTML 문서에서의 일반적인 내용물의 흐름을 말하지만 top, left 거리를 지정
        - absolute : 자신의 상위 box속에서의 top, left, right, bottom 등의 절대적인 위치를 지정
        - fixed : 스크롤(scroll)이 일어나도 항상 화면상의 지정된 위치에 있다
    - top, left, bottom, right
        - top, left, bottom, right 속성은 엘리먼트의 위치를 지정하기 위해 사용
        - 자신이 포함되어 있는 박스 속에서의 top, left, bottom, right에서의 거리를 지정하는 속성
        - 사용법은 "E{ top : 길이 값(length:px, cm) | 백분율(%) | auto }"이다.
        - 각 <div> 엘리먼트의 position 속성이 absolute로 설정이 되어있기 때문에 절대적인 위치 지정 가능
    - overflow
        - overflow 속성은 상위 엘리먼트에 속한 내용이 엘리먼트의 크기보다 클 경우 어떻게 처리할 것인지 설정
        - 속성값을 visible로 설정하면 box속의 내용을 모두 표시. 내용의 크기에 따라 box의 가로, 세로 폭이 늘어남
        - 속성값을 hidden으로 설정하면 box의 width, height를 지정했을 경우, 지정된 범위를 넘치는 내용은 보이지 않는다.
        - 속성값을 auto로 설정하면 지정된 범위를 넘치는 내용은 스크롤바를 이용하여 표시
    - float
        - float 속성은 박스가 화면의 어느 위치에 배치할 것인지를 설정하기 위해 사용
        - 속성값을 left로 설정하면 그림이나 박스가 왼쪽에 배치되고, 글씨는 박스의 오른쪽으로 흐른다.
        - 속성값을 right로 설정하면 그림이나 박스가 오른쪽에 배치되고, 글씨는 박스 왼쪽으로 흐른다.
        - 속성값을 none으로 설정하면 그림이나 박스가 왼쪽에 배치되고, 글씨는 첫 줄만 박스의 오른쪽으로 흐른다.
    - clear
        - clear속성은 float속성이 가지고 있는 값을 초기화 하기 위해 사용
        - 속성값을 left, right로 설정하여 왼쪽 또는 오른쪽 float 속성값을 취소할 수 있다.
        - 속성값을 both로 설정하여 양쪽 모두의 float속성값을 취소할 수 있다.
        - 속성값을 none으로 설정하면 clear를 설정하지 않는 것과 같다.
    - clip
        - clip 속성은 이미지 사이즈가 클 경우 이미지를 일부 가려서 표시하기 위해 사용
        - 속성값으로 rect()에 명시된 사각형 크기만큼 가려서 화면에 표시
        - rect(top, right, bottom, left)순으로 픽셀 값을 설정
        - auto로 설정하면 이미지를 가리지 않고 모두 보여줌
    - visibility
        - visiblity 속성은 엘리먼트를 화면에 보이거나 숨기기 위해서 사용
        - 속성값 visible로 설정하면 화면에 표시하고 hidden으로 설정하면 화면에서 숨김
        - hidden으로 설정된 엘리먼트는 화면에 표시되지는 않지만 면적은 차지하고 있음
        - 화면에서 숨기고 면적도 차지하지 않도록 하기 위해선 display속성을 사용
    - z-index
        - z-index 속성은 여러 개의 엘리먼트를 화면에 쌓아서 표시하기 위해 사용
        - 사용법은 "E { z-index:정수 값(양수, 음수 가능)) }"
        - z-index 값이 큰 엘리먼트를 위에 표시
        - z-index 값을 auto로 설정하면 부모 엘리먼트의 레벨과 같은 값으로 설정되며 이 값이 기본값이다
    
3. 테이블 관련 태그와 속성
    
    ### 테이블 태그
    
    [테이블 속성](https://www.notion.so/90e835d6ce6f45eeb1e860559564c277)
    
4. 자바스크립트 연산자
    
    [제목 없음](https://www.notion.so/aa2b6ed08ecd4afb92050dc89ca23490)
    
5. FORM태그의 속성 및 이벤트
    - control요소
        - 사용자로부터 데이터를 입력 받아 서버에서 처리하기 위한 용도로 사용
        - 사용자의 요청에 따라 서버는 HTML form을 전달(회원가입 양식, 검색 양식 등)
        - 사용자는 HTML form에 적절한 데이터를 입력한 후 서버로 전송. 이를 submit이라 함
        - 서버는 사용자의 요청을 분석한 후 데이터를 등록하거나, 원하는 데이터를 조회하여 결과를 다시 반환
        - 사용자가 입력하기 위한 control 요소들은 모두 <form> tag 하위에 위치해야 서버로 전송됨
        - 각 control 요소마다 텍스트 입력, 버튼 클릭 등 다양한 형식으로 입력을 받는다.
    
    [control요소](https://www.notion.so/966dbcf62eb4488d8e913e6eba7d9c7b)
    
    - form
        - 사용자가 입력한 자료들을 어떤 방식으로 서버로 전달할 것인지 결정
        - 서버에서 어떤 프로그램을 이용해 처리할 것인지 결정
        - <form [속성 = "속성값}'> form control </form>
        - method : 사용자가 입력한 내용을 서버 쪽 프로그램으로 어떻게 넘겨줄지 지정
            - GET(속성값) : 주소 표시줄에 사용자가 입력한 내용이 표시. 256 ~ 2048bytes의 데이터만 서버로 전송
            - POST(속성값) : 사용자의 입력을 표준 입력으로 넘겨주기 때문에 입력 내용의 길이에 제한이 없다. 사용자가 입력한 내용이 표시되지 않는다
        - name : form의 이름을 지정. 한 문서 안에 여러 개의 <form> 태그가 있을 경우, 구분자로 사용
        - action : <form> 태그 안의 내용들을 처리해 줄 서버상의 프로그램 지정. (URL)
        - target : <action> 태그에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정
        - autocomplete : 자동완성기능. 기본값 on
    - label
        - form control에 레이블(텍스트)을 연결
        - 사용법
            - <label [속성="속성값"]> 레이블 <input ...></label>
            - <label for = "id이름"><input id = "id이름" [속성="속성값"]></label>
    - fieldset, legend
        - form요소를 그룹으로 묶음
    - 
6. A태그 속성 이해
    - Anchor
        - <a> tag를 사용하며, 하나의 문서에서 다른 문서로 연결하기 위해 사용
        - tag를 서로 중첩해서 사용할 수 없다
        - href 속성은 하이퍼링크를 클릭했을 때 이동할 문서의 URL이나 문서의 책갈피를 지정
        - target속성은 하이퍼링크를 클릭했을 때 현재 윈도우 또는 새로운 윈도우에서 이동할지를 지정
    
    [target](https://www.notion.so/de116dc190db47fdaf8f078c6ddce349)
    
    - #anchor
        - 같은 페이지 안에서 특정 요소를 클릭 시 그 위치로 한 번에 이동시킨다
    - map
        - 하나의 이미지에 여러 개의 link (Click위치에 따라 서로 다른 link)
        - <map name = "map name"><area><area>...</map>
        - 이미지에 영역을 표시할 때 <area>사용
        - shape의 값으로는 default, rect, circle, poly가 있다.
    - link
        - link tag를 사용하며 문서와 외부 자원을 연결하기 위해 사용
        - <head> 위치에 정의하며 여러 자원을 연결할 수 있다.
        - rel 속성은 현재 문서와 연결된 문서 사이의 연관 관계를 지정하기 위해 사용
        - href 속성은 연결된 문서의 위치를 지정하기 위해 사용
7. CSS 블록과 인라인의 이해
    1. 외부 스타일 시트 적용
        - <link>
            - <link>는 <head>안에 작성하며 rel, type, href 3가지 속성을 주로 사용
            - rel : HTML 페이지와 링크된 파일간의 관계
            - href : CSS file 경로를 의미
            - <link rel = "stylesheet" href="../css/style.css">
        - @import
            - @import는 스타일 시트 중 최상단에 위치해야함.
            - @import url("file path:); 또는 @import "file path";형태로 사용
            - <link>와 달리 <style>의 media 속성을 통해 보여지는 미디어 타입을 설정
    2. 내부 스타일 시트 적용
        - <style>을 사용하여 내부 스타일 시트를 적용
        - <style>tag 내부에 CSS규칙을 작성.
        - 외부 스타일 시트보다 우선 적용
        - <head> tag 내부에 작성
        - <head> tag 내부에 <style></style> tag를 정의하고 css를 정의
    3. 인라인 스타일 적용
        - 개별 element 마다 스타일을 지정하므로 유지보수에 용이하지 않다.
        - 스타일 적용 우선순위 "**인라인 스타일> 내부스타일 시트 > 외부스타일 시트**" 순
        - Style 속성을 사용하고 속성값으로 CSS규칙을 작성
8. CSS선택자
    
    [일반 선택자](https://www.notion.so/a98b5b05a5b44a0e80083cb83f190542)
    
    우선순위 : ID 선택자 > 클래스 선택자 > 타입선택자 > 전체 선택자
    
    [복합 선택자](https://www.notion.so/f4aab7f6cd064a39a8043ef5a1eb755e)
    
    그 외에도 가상 클래스 선택자, 가상 엘리먼트 선택자, 속성 선택자가 존재
    
    [가상 클래스](https://www.notion.so/0c075a480c1d4cdcbc15128f068ef308)
    
    [가상 엘리먼트](https://www.notion.so/b2c1fc4b09fa41be97ea31e50bcf1586)
    
    [속성 선택자](https://www.notion.so/fd2d04e66ff04b789af6537dab3e5a2c)
    
9. 부트스트랩 그리드 방식 이해
10. JQuery함수와 이벤트
    - 이벤트
11. localStorage방식 이해
12. 자바스크립트 문자열의 숫자 변화
    - "String"*1;
    - Number("String");
    - parseInt("String");
    - parseFloat("String");
