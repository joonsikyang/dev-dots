# 브라우저의 렌더링 과정

### :: 브라우저의 렌더링 과정
- 브라우저가 HTML, CSS, JavaScript 로 작성된 텍스트 문서를 어떻게 파싱(해석)하여 브라우저에 렌더링 하는지 살펴보자.
- `파싱(parsing)`
    - 파싱(구문 분석 syntax analysis)은 프로그래밍 언어의 문법에 맞게 작성된 텍스트 문서를 읽어 들여 실행하기 위해 텍스트 문서의 문자열을 토큰(token)으로 분해(어휘 분석 lexical analysis)하고,
    - 토큰에 문법적 의미와 구조를 반영하여 트리 구조의 자료구조인 파스 트리(parse tree / syntax tree)를 생성하는 일련의 과정을 말한다.
    - 일반적으로 파싱이 완료된 이후에는 파스 트리를 기반으로 중간 언어(intermediate code)인 바이트코드(bytecode)를 생성하고 실행한다.
- `렌더링(rendering)`
    - 렌더링은 HTML, CSS, JavaScript 로 작성된 문서를 파싱하여 브라우저에 시각적으로 출력하는 것을 의미한다.
- `브라우저의 렌더링 과정 (critical rendering path)`

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/faf4e2b8-96a2-436b-b1f5-ecceb1feeb58/client-server.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/faf4e2b8-96a2-436b-b1f5-ecceb1feeb58/client-server.png)

    1. 브라우저는 HTML, CSS, 자바스크립트, 이미지, 폰트 파일 등 렌더링에 필요한 리소스를 요청하고 서버로부터 응답받는다.
    2. 브라우저의 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하고 이들을 결합하여 렌더 트리를 생성한다.
    3. 브라우저의 자바스크립트 엔진은 서버로부터 응답된 자바스크립트를 파싱하여 AST(Abstract Syntax Tree)를 생성하고 바이트코드로 변환하여 실행한다. 이때 자바스크립트는 DOM API를 통해 DOM이나 CSSOM을 변경할 수 있다. 변경된 DOM과 CSSOM은 다시 렌더 트리로 결합된다.
    4. 렌더 트리를 기반으로 HTML 요소의 레이아웃(위치와 크기)을 계산하고 브라우저 화면에 HTML 요소를 페인팅한다.
