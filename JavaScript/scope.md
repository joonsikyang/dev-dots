# Scope
### :: Index
- [스코프의 정의](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/scope.md#-%EC%8A%A4%EC%BD%94%ED%94%84%EC%9D%98-%EC%A0%95%EC%9D%98)
- [스코프의 종류 - 전역 스코프와 지역 스코프](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/scope.md#-%EC%8A%A4%EC%BD%94%ED%94%84%EC%9D%98-%EC%A2%85%EB%A5%98---%EC%A0%84%EC%97%AD-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%EC%A7%80%EC%97%AD-%EC%8A%A4%EC%BD%94%ED%94%84)
- [스코프 체인](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/scope.md#-%EC%8A%A4%EC%BD%94%ED%94%84-%EC%B2%B4%EC%9D%B8)
- [함수 레벨 스코프](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/scope.md#-%ED%95%A8%EC%88%98-%EB%A0%88%EB%B2%A8-%EC%8A%A4%EC%BD%94%ED%94%84)
- [Lexical(Static) Scope](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/scope.md#-lexical-scope)

<br />

### :: 스코프의 정의
- `스코프(Scope)` : 식별자가 유효한 범위
    - 모든 식별자(변수 이름, 함수 이름, 클래스 이름 등)는 자신이 선언된 위치에 의해 다른 코드가 식별자 자신을 참조할 수 있는 유효범위가 결정된다. 이를 `스코프` 라 한다.

        ```jsx
        // Scope : 식별자가 유효한 범위
        // 선언된 위치에 의해 유효범위가 결정됨 (cf. Lexical Scope / Static Scope vs. Dynamic Scope)

        var var1 = 1; // 코드의 가장 바깥 영영에서 선언한 변수 (전역 변수)

        if(true) {
        	var var2 = 2; // 코드 블록 내에서 선언한 변수 (var 키워드 사용 >>> 전역 변수)
        	if(true) {
        		var var3 = 3; // 중첩된 코드 블록 내에서 선언한 변수
        	}
        };

        function foo() {
        	var var4 = 4; // 함수 내에서 선언한 변수

        	function bar() {
        		var var5 = 5; // 중첩된 함수 내에서 선언한 변수
        	}
        };

        console.log(var1); // 1
        console.log(var2); // 2
        console.log(var3); // 3
        console.log(var4); // ReferenceError: var4 is not defined
        console.log(var5); // ReferenceError: var5 is not defined
        ```

- `스코프(Scope)` :  자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙

    ```jsx
    var x = 'global';

    function foo() {
    	var x = 'local';
    	console.log(x); // 1) 'local'
    }

    foo();

    console.log(x); // 2) 'global'
    ```

    - `식별자 결정 Identifier Resolution`
    
		- 자바스크립트 엔진은 이름이 같은 두 개의 변수 중에서 어떤 변수를 참조해야 할 것인지를 결정해야 한다. 이를 식별자 결정이라 한다.

		- 자바스크립트 엔진은 스코프를 통해 어떤 변수를 참조해야 할 것인지를 결정한다.

		- 따라서 스코프란 자바스크립트 엔진이 식별자를 검색할 때 사용하는 규칙이라고도 할 수 있다.
    
    - 전역에서 선언된 x 와 함수 내부에서 선언된 변수 x 는 이름이 동일한 식별자이지만 자신이 유효한 범위, 즉 스코프가 다른 별개의 변수다.

- 스코프로 인한 식별자 Name Binding
    
    - 식별자는 어떤 값을 구별할 수 있어야 하므로 유일해야 한다. 따라서 식별자인 변수 이름은 중복될 수 없다. 즉, 하나의 값은 유일한 식별자에 연결 `name binding` 되어야 한다.
    
    - 프로그래밍 언어에서는 스코프, 즉 유효범위를 통해 식별자인 변수 이름의 충돌을 방지하여 같은 이름의 변수를 사용할 수 있게 한다. 스코프 내에서 식별자는 유일해야 하지만 다른 스코프에는 같은 이름의 식별자를 사용할 수 있다. 즉, 스코프는 네임스페이스다.
    
    - cf. `var` 키워드로 선언한 변수의 중복 선언
        
		- var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언이 허용된다. 이는 의도치 않게 변수값이 재할당되어 변경되는 부작용을 발생시킨다.

		    ```jsx
		    function foo() {
			var x = 1;
			// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
			// 아래 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
			var x = 2;
			console.log(x); // 2
		    }

		    foo();
		    ```


		- 하지만 let 이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.

		    ```jsx
		    function bar() {
			let x = 1;
			// let 이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
			let x = 2; // SyntaxError: Identifier 'x' has already been declared
		    }

		    bar();
		    ```

<br />

### :: 스코프의 종류 - 전역 스코프와 지역 스코프
- 코드는 `전역 global` 과 `지역 local` 으로 구분할 수 있다.

- 이 때 변수는 자신이 선언된 위치(전역 또는 지역)에 의해 자신이 유효한 범위인 스코프가 결정된다.

- 즉, 전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역에서 선언된 변수는 지역 스코프를 갖는 지역 변수다.

- 전역 / 지역
    - 전역 - 코드의 가장 바깥 영역 - 전역 스코프 - 전역 변수
    - 지역 - 함수 몸체 내부 - 지역 스코프 - 지역 변수

```jsx
// 전역 스코프와 전역 변수
var x = "global x";
var y = "global y";

funciton outer() { // 지역 스코프
	var z = "outer's local z";

	console.log(x); // global x
	console.log(y); // global y
	console.log(z); // outer's local z

	function inner() { // 지역 스코프
		var x = "inner's local x";

		console.log(x); // inner's local x >>> scope chain
		console.log(y); // global y
		console.log(z); // outer's local z
	}

	inner();
}

outer();

console.log(x); // global x
console.log(z); // ReferenceError: z is not defined
```

<br />

### :: 스코프 체인
- 함수의 중첩에 의해 스코프는 계층적 구조를 갖는다.
    
    - 함수의 중첩 : 함수 몸체 내부에서 함수가 정의된 것
    
    - `외부 함수 Outer function` vs. `중첩 함수 Nested function`
    
    - 외부 함수의 지역 스코프를 중첩 함수의 상위 스코프라 한다.
    
    - `inner` 지역 스코프 >>> `outer` 지역 스코프 >>> 전역 스코프

- 스코프 체인 (Scope Chain)
    
    - `스코프 체인 (Scope Chain)` : 스코프가 계층적으로 연결된 것
    
    - 모든 스코프는 하나의 계층적 구조로 연결되며, 모든 지역 스코프의 최상위 스코프는 전역스코프다.
    
    - cf. `Lexical Environment`
        
	- 스코프 체인은 실행 컨텍스트의 렉시컬 환경을 단방향으로 연결(chaining)한 것이다.
        
	- 전역 렉시컬 환경은 코드가 로드되면 곧바로 생성되고 함수의 렉시컬 환경은 함수가 호출되면 바로 생성된다.

- 스코프 체인에 의한 변수 검색 (Identifier Resolution)
    
    - 변수를 참조할 때 자바스크립트 엔진은 스코프 체인을 통해 변수를 참조하는 코드의 스코프에서 시작하여 상위 스코프 방향으로 이동하며 선언된 변수를 검색(identifier resolution)한다.
    
    - 이를 통해 상위 스코프에서 선언한 변수를 하위 스코프에서도 참조할 수 있다.

- 스코프 체인에 의한 함수 검색

    ```jsx
    // 전역 함수
    function foo() {
    	console.log('global function foo');
    };

    function bar() {
    	// 중첩 함수
    	function foo() {
    		console.log('local function foo'); 
    	};

    	foo(); // 1)
    };

    bar(); // 'local function foo'
    ```

    - 함수 선언문으로 함수를 정의하면 런타임 이전에 함수 객체가 먼저 생성된다.
    
    - 그리고 자바스크립트 엔진은 함수 이름과 동일한 이름의 식별자를 암묵적으로 선언하고 생성된 함수 객체를 할당한다.
    
    - 따라서 위 예제의 모든 함수는 함수 이름과 동일한 이름의 식별자에 할당된다.
    
    - `1)` 에서 foo 함수를 호출하면 자바스크립트 엔진은 함수를 호출하기 위해 먼저 함수를 가리키는 식별자 foo를 검색한다.
    
    - 이처럼 함수도 식별자에 할당되기 때문에 스코프를 갖는다.
    
    - 사실 함수는 식별자에 함수 객체가 할당된 것 외에는 일반 변수와 다를 게 없다.
    
    - 따라서 스코프를 '변수를 검색할 때 사용하는 규칙'이라고 표현하기 보다는 "식별자를 검색하는 규칙" 이라고 표현하는 것이 더 적합하다.

<br />

### :: 함수 레벨 스코프
- 지역은 함수 몸체 내부를 말하고 지역은 지역 스코프를 만든다.

- 이는 코드 블록이 아닌 함수에 의해서 지역 스코프가 생성된다는 의미다.

- `Block level scope` vs. `Function level scope`
    
    - Block level scope
        
	- C나 자바등을 비롯한 대부분의 프로그래밍 언어는 함수 몸체만이 아니라 모든 코드 블록(if, for, while, try/catch 등)이 지역 스코프를 만든다.
        
	- 이러한 특성을 블록 레벨 스코프라 한다.
    
    - Function level scope
        
	- `var` 키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다.
        
	- 이러한 특성을 함수 레벨 스코프라 한다.
        
	- `var` 키워드로 선언된 변수는 오로지 함수의 코드 블록만을 지역 스코프로 인정하지만 ES6 에서 도입된 `let`, `const` 키워드는 블록 레벨 스코프를 지원한다.

- Example 1)

    ```jsx
    var x = 1; // 전역 변수

    if(true) { // 코드 블록
    	// 함수 밖에서 var 키워드로 선언된 변수는 코드 블록 내에서 선언되었다 할지라도 모두 전역 변수다.
    	var x = 10; // 전역 변수 >> x 변수 중복 선언 
    }

    console.log(x); // 10 >> 의도치 않은 전역 변수 값의 재할당
    ```

- Example 2)

    ```jsx
    var i = 10;

    // for 문에서 선언한 i는 전역 변수 >> x 변수 중복 선언
    for (var i = 0; i < 5; i++) {
    	console.log(i); // 0 1 2 3 4
    }

    console.log(i); // 5 >> 의도치 않은 전역 변수 값의 재할당
    ```
    
 <br />
 
 ### :: Lexical Scope
 - 함수의 상위 스코프 결정 방식
    
    - 함수를 어디서 호출 했는지 vs. 함수를 어디서 정의 했는지
    
    - 프로그래밍 언어는 일반적으로 이 두 가지 방식 중 한 가지 방식으로 함수의 상위 스코프를 결정한다.
    
    - 동적 스코프 : 함수를 어디서 호출 했는지
        
	- Dynamic Scope
        
	- 함수가 호출되는 시점에 동적으로 상위 스코프를 결정
    
    - 정적 스코프 : 함수를 어디서 정의 했는지
        
	- Static Scope / Lexical Scope
        
	- 함수 정의가 평가되는 시점에 상위 스코프를 결정
        
	- 자바스크립트를 비롯한 대부분의 프로그래밍 언어는 정적 스코프를 따른다.

- 자바스크립트와 정적 스코프
    
    - 자바스크립트는 함수를 어디서 호출했는지가 아니라 함수를 어디서 정의했는지에 따라 상위 스코프를 결정한다. 즉, 함수의 상위 스코프는 언제나 자신이 정의된 스코프다.
    
    - 이처럼 함수의 상위 스코프는 함수 정의가 실행될 때 정적으로 결정된다.
    
    - 함수 정의(함수 선언문 또는 함수 표현식)가 실행되어 생성된 함수 객체는 이렇게 결정된 상위 스코프를 기억한다.
    
    - 함수가 호출될 때마다 함수의 상위 스코프를 참조할 필요가 있기 때문이다.

- 코드 예시

    ```jsx
    var x = 1;

    function foo() {
    	var x = 10;
    	bar(); // 함수가 호출되는 시점
    }

    function bar() { // 함수가 정의되는 시점
    	console.log(x);
    }

    foo(); // ?
    bar(); // ?
    ```

    - `bar` 함수의 상위 스코프
        
	- 동적 스코프를 따른다면 : `foo` 함수의 지역 스코프와 전역 스코프
        
	- 정적 스코프를 따른다면 : 전역 스코프
    
    - 자바스크립트는 정적 스코프를 따른다.
        
	- `bar` 함수는 전역에서 정의된 함수다.
        
	- 함수 선언문으로 정의된 `bar` 함수는 전역 코드가 실행되기 전에 먼저 평가되어 함수 객체를 생성한다.
        
	- 이때 생성된 `bar` 함수 객체는 자신이 정의된 스코프, 즉 전역 스코프를 기억한다.
        
	- 그리고 `bar` 함수가 호출되면 호출된 곳이 어디인지 관계 없이 언제나 자신이 기억하고 있는 전역 스코프를 상위 스코프로 사용한다.
        
	- 다라서 위 예제를 실행하면 전역 변수 `x`의 값 `1`을 두 번 출력한다.
