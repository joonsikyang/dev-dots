# 브라우저의 렌더링 과정
### :: Index
- [브라우저의 렌더링 과정](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98-%EB%A0%8C%EB%8D%94%EB%A7%81-%EA%B3%BC%EC%A0%95)
- [요청과 응답](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EC%9A%94%EC%B2%AD%EA%B3%BC-%EC%9D%91%EB%8B%B5)
- [HTTP 1.1과 HTTP 2.0](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-http-11%EA%B3%BC-http-20)
- [HTML 파싱과 DOM 생성](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-html-%ED%8C%8C%EC%8B%B1%EA%B3%BC-dom-%EC%83%9D%EC%84%B1)
- [CSS 파싱과 CSSOM 생성](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-css-%ED%8C%8C%EC%8B%B1%EA%B3%BC-cssom-%EC%83%9D%EC%84%B1)
- [렌더 트리 생성](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EB%A0%8C%EB%8D%94-%ED%8A%B8%EB%A6%AC-%EC%83%9D%EC%84%B1)
- [자바스크립트 파싱과 실행](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8C%8C%EC%8B%B1%EA%B3%BC-%EC%8B%A4%ED%96%89)
- [리플로우와 리페인트](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EB%A6%AC%ED%94%8C%EB%A1%9C%EC%9A%B0%EC%99%80-%EB%A6%AC%ED%8E%98%EC%9D%B8%ED%8A%B8)
- [자바스크립트 파싱에 의한 HTML 파싱 중단](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8C%8C%EC%8B%B1%EC%97%90-%EC%9D%98%ED%95%9C-html-%ED%8C%8C%EC%8B%B1-%EC%A4%91%EB%8B%A8)
- [script 태그의 async/defer attribute](https://github.com/joonsikyang/dev-dots/blob/main/WEB/browser_rendering.md#-script-%ED%83%9C%EA%B7%B8%EC%9D%98-asyncdefer-attribute)

<br />

### :: 브라우저의 렌더링 과정
- 브라우저가 HTML, CSS, JavaScript 로 작성된 텍스트 문서를 어떻게 파싱(해석)하여 브라우저에 렌더링 하는지 살펴보자.

- `파싱(parsing)`
    
    - 파싱(구문 분석 syntax analysis)은 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서를 읽어 들여 실행하기 위해 텍스트 문서의 문자열을 토큰(token)으로 분해(어휘 분석 lexical analysis)하고,
    
    - 토큰에 문법적 의미와 구조를 반영하여 트리 구조의 자료구조인 파스 트리(parse tree / syntax tree)를 생성하는 일련의 과정을 말한다.
    
    - 일반적으로 파싱이 완료된 이후에는 파스 트리를 기반으로 중간 언어(intermediate code)인 바이트코드(bytecode)를 생성하고 실행한다.

- `렌더링(rendering)`
    
    - 렌더링은 HTML, CSS, JavaScript 로 작성된 문서를 파싱하여 브라우저에 시각적으로 출력하는 것을 의미한다.

- `브라우저의 렌더링 과정 (critical rendering path)`    
    - 1. 브라우저는 HTML, CSS, 자바스크립트, 이미지, 폰트 파일 등 렌더링에 필요한 리소스를 요청하고 서버로부터 응답받는다.
    
    - 2. 브라우저의 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하고 이들을 결합하여 렌더 트리를 생성한다.
    
    - 3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱하여 AST(Abstract Syntax Tree)를 생성하고 바이트코드로 변환하여 실행한다. 이때 자바스크립트는 DOM API를 통해 DOM이나 CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
    
    - 4. 렌더 트리를 기반으로 HTML 요소의 레이아웃(위치와 크기)을 계산하고 브라우저 화면에 HTML 요소를 페인팅한다.

    ![client-server](https://user-images.githubusercontent.com/43266792/127882129-420a17ed-d8d4-4f88-9783-21f42d53ec26.png)

<br />

### :: 요청과 응답
- 1) 브라우저와 서버의 통신
    - 브라우저의 핵심 기능은 필요한 리소스(HTML, CSS, 자바스크립트, 이미지, 폰트 등의 정적 파일 또는 서버가 동적으로 생성한 데이터)를 서버에 요청(request)하고 서버로부터 응답(response) 받아 브라우저에 시각적으로 렌더링하는 것
    
    - 즉, 렌더링에 필요한 리소스는 모두 서버에 존재하므로 필요한 리소스를 서버에 요청하고 서버가 응답한 리소스를 파싱하여 렌더링하는 것
    
    - 서버에 요청을 전송하기 위해 브라우저는 주소창을 제공한다.
    
    - 브라우저의 주소창에 URL을 입력하고 엔터를 누르면 URL의 호스트 이름이 DNS를 통해 IP주로소 변환되고 이 IP 주소를 갖는 서버에게 요청을 전송한다.
    
    - URI(Uniform Resource Identifier)
        ![uri](https://user-images.githubusercontent.com/43266792/128028965-aa9419de-9b2d-49c6-94af-9d0060e49f0c.png)

- 2) 브라우저의 주소창에 `https://poiemaweb.com` 을 입력하고 엔터 키를 누르면
    - 루트 요청 (index.html)
        
        - 루트 요청(`/`, 스킴(`scheme`)과 호스트(`host`)만으로 구성된 URI에 의한 요청)이 `poiemaweb.com` 서버로 전송된다.
        
        - 루트 요청에는 명확히 리소스를 요청하는 내용이 없지만 일반적으로 서버는 루트 요청에 대해 암묵적으로 `index.html` 을 응답하도록 기본 설정되어 있다.
        
        - 즉, `https://poiemaweb.com` 은 `https://poiemaweb.com/index.html` 과 같은 요청이다.
        
        - 따라서 서버는 루트 요청에 대해 서버의 루트 폴더에 존재하는 정적 파일 `index.html` 을 클라이언트(브라우저)로 응답한다.
    
    - 정적 파일 요청
        
        - 만약 index.html 이 아닌 다른 정적 파일을 서버에 요청하려면 브라우저의 주소창에 `https://poiemaweb.com/assets/data/data.json` 과 같이 요청할 정적 파일의 경로(서버의 루트 폴더 기준)와 파일 이름을 URI의 호스트 뒤의 패스(`path`)에 기술하여 서버에 요청한다.
        
        - 그러면 서버는 루트 폴더의 `assets/data` 폴더 내에 있는 정적 파일 `data.json` 을 응답할 것이다.
    
    - 동적으로 서버에 정적/동적 데이터 요청
        
        - 반드시 브라우저의 주소창을 통해 서버에게 정적 파일만 요청할 수 있는 것은 아니다.
        
        - 자바스크립트를 통해 동적으로 서버에 정적/동적 데이터를 요청할 수도 있다.
        
        - cf) `Ajax`, `REST API`

- 3) Network 패널을 활용한 요청과 응답 확인
    
    - 요청과 응답은 개발자 도구의 Network 패널에서 확인할 수 있다.
    
    - 개발자 도구의 Network 패널을 활성화하기 이전에 브라우저가 이미 응답 받은 경우 응답된 리소스가 표시되지 않는다. 따라서 Network 패널에 아무런 리소스가 표시되지 않았다면 페이지를 새로고침 해야 한다.
    
    - 브라우저의 주소창을 통해 요청한 `index.html` 외에 CSS, 자바스크립트, 이미지, 폰트 파일들도 응답되는 이유는?
    
    - 이는 브라우저의 렌더링 엔진이 HTML(index.html)을 파싱하는 도중에 외부 리소스를 로드하는 태그, 즉 CSS 파일을 로드하는 `link` 태그, 이미지 파일을 로드하는 `img` 태그, 자바스크립트를 로드하는 `script` 태그 등을 만나면 HTML의 파싱을 일시 중단하고 해당 리소스 파일을 서버로 요청하기 때문이다.

<br />

### :: HTTP 1.1과 HTTP 2.0
- `HTTP (HyperText Transfer Protocol)` : 웹에서 브라우저와 서버가 통신하기 위한 프로토콜(규약)

- HTTP의 역사와 발전
    - 1989년 - HTML, URL과 함께 팀 버너스리가 고안
    
    - 1991년 - 최초로 문서화
    
    - 1996년 - `HTTP / 1.0.`
    
    - 1999년 - `HTTP / 1.1.`
    
    - 2015년 - `HTTP / 2.0.`

- `HTTP 1.1`
    - HTTP / 1.1 은 기본적으로 커넥션(connection)당 하나의 요청과 응답만 처리
    
    - 즉, 여러 개의 요청을 한 번에 전송할 수 없고 응답 또한 마찬가지
    
    - 따라서 HTML 문서 내에 포함된 여러 개의 리소스 요청, 즉 CSS 파일을 로드하는 link 태그, 이미지 파일을 로드하는 img 태그, 자바스크립트를 로드하는 script 태그 등에 의한 리소스 요청이 개별적으로 전송되고 응답 또한 개별적으로 전송된다.
    
    - 이처럼 HTTP / 1.1 은 리소스의 동시 전송이 불가능한 구조이므로 요청할 리소스의 개수에 비례하여 응답 시간도 증가하는 단점이 있다.

- `HTTP 2.0`
    - HTTP / 2 는 커넥션당 여러 개의 요청과 응답, 즉 다중 요청/응답이 가능하다.
    
    - 따라서 HTTP / 2 는 여러 리소스의 동시 전송이 가능하므로 HTTP / 1.1. 에 비해 페이지 로드 속도가 약 50% 정도 빠르다고 알려져 있다.

- `HTTP 1.1` vs. `HTTP 2.0`
    ![http](https://user-images.githubusercontent.com/43266792/128028518-8712e499-bc3f-49b3-ade7-70c6940681c9.png)


<br />

### :: HTML 파싱과 DOM 생성
- 브라우저의 요청에 의해 서버가 응답한 HTML 문서는 문자열로 이루어진 순수한 텍스트다.

- 순수한 텍스트인 HTML 문서를 브라우저에 시각적인 픽셀로 렌더링하려면 HTML 문서를 브라우저가 이해할 수 있는 자료구조(객체)로 변환하여 메모리에 저장해야 한다.

- 브라우저 렌더링 엔진은 응답받은 HTML 문서를 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM(Document Object Model) 을 생성한다.

- 즉, DOM은 HTML 문서를 파싱한 결과물이다.

- DOM 생성 과정

    ![full-process](https://user-images.githubusercontent.com/43266792/128587778-d14a2530-4540-4d8e-879d-c289b5cc1633.png)

    - `바이트` : 서버에 존재하던 HTML 파일이 브라우저의 요청에 의해 응답된다. 이때 서버는 브라우저가 요청한 HTML 파일을 읽어 들여 메모리에 저장한 다음 메모리에 저장된 바이트(2진수)를 인터넷을 경유하여 응답한다. 브라우저는 서버가 응답한 HTML 문서를 바이트(2진수)형태로 응답받는다.
    
    - `문자` : 응답된 바이트 형태의 HTML 문서는 `meta` 태그의 `charset` 어트리뷰트에 의해 지정된 인코딩 방식(예: `UTF-8`)을 기준으로 문자열로 반환된다. 참고로 `meta` 태그의 `charset` 어트리뷰트에 선언된 인코딩 방식(예: `UTF-8`)은 `content-type: text/html; charset=utf-8` 과 같이 응답 헤더(response header)에 담겨 응답된다. 브라우저는 이를 확인하고 문자열로 반환한다.
    
    - `토큰` : 문자열로 반환된 HTML 문서를 읽어 들여 문법적 의미를 갖는 코드의 최소 단위인 토큰(token)으로 분해한다.
    
    - `노드` : 각 토큰들은 객체로 변환하여 노드(node)들을 생성한다. 토큰의 내용에 따라 문서 노드, 요소 노드, 어트리뷰트 노드, 텍스트 노드가 생성된다. 노드는 이후 DOM 을 구성하는 기본 요소가 된다.
    
    - `DOM` : HTML 문서는 HTML 요소들의 집합으로 이루어지며 HTML 요소는 중첩 관계를 갖는다. 즉, HTML 요소의 콘텐츠 영역(시작 태그와 종료 태그 사이)에는 텍스트뿐만 아니라 다른 HTML 요소도 포함될 수 있다. 이때 HTML 요소 간에는 중첩 관계에 의해 부자 관계가 형성된다. 이러한 HTML 요소 간의 부자 관계를 반영하여 모든 노드들을 트리 자료구조로 구성한다. 이 노드들로 구성된 트리 자료구조를 DOM(Document Object Model) 이라 부른다.

<br />

### :: CSS 파싱과 CSSOM 생성
- 렌더링 엔진은 HTML 을 한줄씩 순차적으로 파싱하여 DOM을 생성해 나가다가 CSS 를 로드하는 `link` 태그나 `style` 태그를 만나면 DOM 생성을 일시 중단한다.

- 그리고 `link` 태그의 `href` 어트리뷰트에 지정된 CSS 파일을 서버에 요청하여 로드한 CSS 파일이나 style 태그 내의 CSS를 HTML과 동일한 파싱 과정(바이트 → 문자 → 토큰 → 노드 → CSSOM)을 거치며 해석하여 CSSOM(CSS Object Model)을 생성한다.
    ![cssom-construction](https://user-images.githubusercontent.com/43266792/128587805-094129c2-57c3-4629-bb43-599911a173df.png)

- 이후 CSS 파싱을 완료하면 HTML 파싱이 중단된 지점부터 다시 HTML을 파싱하기 시작하여 DOM 생성을 재개한다.

- CSSOM은 CSS의 상속을 반영하여 생성된다.

<br />

### :: 렌더 트리 생성
![render-tree-construction](https://user-images.githubusercontent.com/43266792/128172712-f4aabd98-022a-472b-bad8-c86cdd9d55c3.png)

- 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 각각 DOM과 CSSOM을 생성한다.

- 그리고 DOM과 CSSOM은 렌더링을 위해 렌더 트리(render tree)로 결합된다.

- 렌더 트리는 렌더링을 위한 트리 구조의 자료구조다.

- 렌더 트리는 브라우저 화면에 렌더링되는 노드만으로 구성된다.

- 화면에 렌더링되지 않는 노드(ex. `<meta>`, `<script>`) 와 CSS에 의해 비표시(ex. `display : none`)되는 노드들은 포함되지 않는다.

- 완성된 렌더 트리는 각 HTML 요소의 `레이아웃`(위치와 크기)을 계산하는 데 사용되며 브라우저 화면에 픽셀을 렌더링하는 페인팅(`painting`) 처리에 입력된다.

- (`HTML` → `DOM tree`) + (`CSS` → `CSSOM`) → `Render Tree` → `Layout` → `Paint`

- 브라우저의 렌더링 과정은 반복해서 실행될 수 있다.

- 다음과 같은 경우 반복해서 `레이아웃 계산`과 `페인팅`이 재차 실행된다.
    
    - 자바스크립트에 의한 노드 추가 또는 삭제
    
    - 브라우저 창의 리사이징에 의한 뷰포트(viewport) 크기 변경
    
    - HTML 요소의 레이아웃(위치, 크기)에 변경을 발생시키는 width, height, margin, padding, border, display, position, top/right/bottom/left 등의 스타일 변경

- 레이아웃 계산과 페인팅을 다시 실행하는 리렌더링은 비용이 많이 드는, 즉 성능에 악영향을 주는 작업이다. 따라서 가급적 리렌더링이 빈번하게 발생하지 않도록 주의할 필요가 있다. (cf. 성능 최적화)

<br />

### :: 자바스크립트 파싱과 실행
- HTML 문서를 파싱한 결과물로서 생성된 DOM은 HTML 문서의 구조와 정보뿐만 아니라 HTML 요소와 스타일 등을 변경할 수 있는 프로그래밍 인터페이스로서 DOM API 를 제공한다.

- 즉, 자바스크립트 코드에서 DOM API를 사용하면 이미 생성된 DOM을 동적으로 조작할 수 있다.

- CSS 파싱 과정과 마찬가지로 `렌더링 엔진`은 HTML을 한 줄씩 순차적으로 파싱하며 DOM을 생성해 나가다가 자바스크립트 파일을 로드하는 `script` 태그나 자바스크립트 코드를 콘텐츠로 담은 `script` 태그를 만나면 DOM 생성을 일시 중단한다.

- 그리고 script 태그의 src 어트리뷰트에 정의된 자바스크립트 파일을 서버에 요청하여 로드한 자바스크립트 파일이나 script 태그 내의 자바스크립트 코드를 파싱하기 위해 `자바스크립트 엔진`에 제어권을 넘긴다.

- 이후 자바스크립트 파싱과 실행이 종료되면 렌저링 엔진으로 다시 제어권을 넘겨 HTML 파싱이 중단된 지점부터 다시 HTML 파싱을 시작하여 DOM 생성을 재개한다.

- 자바스크립트 파싱과 실행은 브라우저의 렌더링 엔진이 아닌 자바스크립트 엔진이 처리한다.

- 자바스크립트 엔진은 자바스크립트 코드를 파싱하여 CPU가 이해할 수 있는 저수준 언어(low-level language)로 변환하고 실행하는 역할을 한다.

- 자바스크립트 엔진은 구글 크롬과 Node.js의 V8, 파이어폭스의 SpiderMonkey, 사파리의 JavaScriptCore 등 다양한 종류가 있으며, 모든 자바스크립트 엔진은 ECMAScript 사양을 준수한다.

- 렌더링 엔진으로부터 제어권을 넘겨받은 자바스크립트 엔진은 자바스크립트 코드를 파싱하기 시작한다.

- 렌더링 엔진이 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하듯이 자바스크립트 엔진은 자바스크립트를 해석하여 `AST(Abstract Syntax Tree 추상적 구문 트리)`를 생성한다.

- 그리고 AST를 기반으로 인터프리터가 실행할 수 있는 `중간 코드(intermediate code)`인 `바이트코드`를 생성하여 실행한다.

1. `토크나이징(tokenizing)`
    - 단순한 문자열인 자바스크립트 소스코드를 어휘 분석(lexical analysis)하여 문법적 의미를 갖는 코드의 최소 단위인 토큰(token)들로 분해한다.
    - 이 과정을 렉싱(lexing)이라 부리기도 하지만 토크나이징과 미묘한 차이가 있다.

2. `파싱`
    - 토큰들의 집합을 구문 분석(syntactic analysis)하여 `AST(Abstract Syntax Tree 추상적 구문 트리)` 를 생성한다.
    - AST는 토큰에 문법적 의미와 구조를 반영한 트리 구조의 자료구조다.
    - AST는 인터프리터나 컴파일러만이 사용하는 것은 아니다.
    - AST를 사용하면 Typescript, Babel, Prettier 같은 트랜스파일러(transpilir)를 구현할 수도 있다.

3. `바이트코드 생성과 실행`
    - 파싱의 결과물로서 생성된 AST는 인터프리터가 실행할 수 있는 중간 코드인 바이트코드로 변환되고 인터프리터에 의해 실행된다.
    - 참고로 V8 엔진의 경우 자주 사용되는 코드는 터보팬(TurboFan)이라 불리는 컴파일러에 의해 최적화된 머신 코드(optimized machine code)로 컴파일되어 성능을 최적화한다.
    - 만약 코드의 사용 빈도가 적어지면 다시 디옵티마이징(deoptimizing)하기도 한다.

<br />

### :: 리플로우와 리페인트
- 만약 자바스크립트 코드에 DOM이나 CSSOM을 변경하는 DOM API 가 사용된 경우 DOM이나 CSSOM이 변경된다.

- 이때 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합되고 변경된 렌더 트리를 기반으로 레이아웃과 페인트 과정을 거쳐 브라우저의 화면에 다시 렌더링한다.

- 이를 리플로우(reflow), 리페인트(repaint)라 한다.

- (그림 38-12 참고)

- 리플로우(reflow)
    - 레이아웃 계산을 다시 하는 것
    - 노드 추가/삭제, 요소의 크기/위치 변경, 윈도우 리사이징 등 레이아웃에 영향을 주는 변경이 발생한 경우에 한하여 실행

- 리페인트(repaint)
    - 재결합된 렌더 트리를 기반으로 다시 페인트를 하는 것

- 리플로우와 리페인트가 반드시 순차적으로 동시에 실행되는 것은 아니다. 레이아웃에 영향이 없는 변경은 리플로우 없이 리페인트만 실행된다.

- cf. 성능 최적화

<br />

### :: 자바스크립트 파싱에 의한 HTML 파싱 중단
- 렌더링 엔진과 자바스크립트 엔진은 병렬적으로 파싱을 실행하지 않고 직렬적으로 파싱을 수행한다.

    ```html
    <!-- HTML 파싱 -->
    <!DOCTYPE html> 
    <html>
    	<head>
    		<meta charset="UTF-89">
    		<!-- HTML 파싱 중단 -->
    		<!-- CSS 파싱 -->
    		<link rel="stylesheet" href="style.css">
    		<!-- JavaScript 파싱/실행 -->
    		<script src="app.js"></script>
    	<!-- HTML 파싱 -->
    	</head>
    	<body>
    		<h1>JavaScript</h1>
    	</body>
    </html>
    ```

- 이처럼 브라우저는 동기적(`synchronous`)으로, 즉 위에서 아래 방향으로 순차적으로 HTML, CSS, 자바스크립트를 파싱하고 실행한다.

- 이것은 script 태그의 위치에 따라 HTML 파싱이 블로킹 되어 DOM 생성이 지연될 수 있다는 것을 의미한다. 따라서 script 태그의 위치는 중요한 의미를 갖는다.

- 위의 경우 app.js의 파싱과 실행 이전까지는 DOM 생성이 일시 중단된다.

- 이때 자바스크립트 코드(app.js)에서 DOM이나 CSSOM을 변경하는 DOM API를 사용하는 경우 DOM이나 CSSOM이 이미 생성되어 있어야 한다.

- 만약 DOM을 변경하는 DOM API를 사용할 때 DOM의 생성이 완료되지 않은 상태라면 문제가 발생할 수 있다.

- 이러한 문제를 회피하기 위해 body 요소의 가장 아래에 자바스크립트를 위치시키는 것이 좋은 아이디어다. 그 이유는 다음과 같다.
    
    1. DOM이 완성되지 않은 상태에서 자바스크립트가 DOM을 조작하면 에러가 발생할 수 있다.
    
    2. 자바스크립트 로딩/파싱/실행으로 인해 HTML 요소들의 렌더링에 지장받는 일이 발생하지 않아 페이지 로딩 시간이 단축된다.

<br />

### :: script 태그의 async/defer attribute
- 자바스크립트 파싱에 의한 DOM 생성이 중단(blocking)되는 문제를 근본적으로 해결하기 위해 HTML5 부터 `script` 태그에 `async` 와 `defer` 어트리뷰트가 추가되었다.

- `async` 와 `defer` 속성은 `src` 속성을 통해 외부 자바스크립트 파일을 로드하는 경우에만 사용할 수 있다. 즉, `src` 속성이 없는 인라인 자바스크립트에는 사용할 수 없다.

    ```html
    <script async src="extern.js"></script>
    <script defer src="extern.js"></script>
    ```

- `async` 와 `defer` 속성을 사용하면 HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적(`asynchronous`)으로 동시에 진행된다. 하지만 자바스크립트의 실행 시점에 차이가 있다.

- `async`
    - HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다.
    
    - 단, 자바스크립트 파싱과 실행은 자바스크립트 파일의 로드가 완료된 직후 진행되며, 이때 HTML 파싱이 중단된다.
    
    - 여러 개의 `script` 태그에 `async` 속성을 지정하면 script 태그의 순서와 상관없이 로드가 완료된 자바스크립트부터 먼저 실행되므로 순서가 보장되지 않는다.
    
    - 따라서 순서 보장이 필요한 `script` 태그에는 `async` 속성을 지정하지 않아야 한다.
    
    - `async` 속성은 IE10 이상에서 지원된다.

- `defer`
    - `async` 속성과 마찬가지로 HTML 파싱과 외부 자바스크립트 파일의 로드가 비동기적으로 동시에 진행된다.
    
    - 단, 자바스크립트 파싱과 실행은 HTML 파싱이 완료된 직수, 즉, DOM 생성이 완료된 직후(이때 `DOMContentLoaded` 이벤트가 발생한다.) 진행된다.
    
    - 따라서 DOM 생성이 완료된 이후 실행되어야 할 자바스크립트에 유용하다.
    
    - `defer` 속성은 IE10 이상에서 지원된다.
