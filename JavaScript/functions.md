# Functions

### :: Index
- [함수란?](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/functions.md#-%ED%95%A8%EC%88%98%EB%9E%80)
- [함수를 사용하는 이유](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/functions.md#-%ED%95%A8%EC%88%98%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)
- 함수 선언문과 함수 표현식, 함수의 생성 시점에 따른 차이(호이스팅)
- [콜백 함수 (Callback Functions)](https://github.com/joonsikyang/dev-dots/blob/main/JavaScript/functions.md#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98-callback-functions)

<br />

### :: 함수란?
- 프로그래밍 언어의 함수는 일련의 과정을 문(statement)으로 구현하고 코드 블록으로 감싸서 하나의 실행 단위로 정의한 것이다.
- 프로그래밍 언어의 함수도 수학의 함수와 같이 입력을 받아서 출력을 내보낸다.
- 이때 함수 내부로 입력을 전달받는 변수를 매개변수(parameter), 입력을 인수(argument), 출력을 반환값(return value)이라 한다.
- 함수는 값이며, 여러개 존재할 수 있으므로 특정 함수를 구별하기 위해 식별자인 함수 이름을 사용할 수 있다.
- 함수의 구성 요소
    ```jsx
    // 함수의 정의 - 함수이름, 매개변수, 반환값, 함수 몸체
    function add(x, y) {
      return x + y;
    }

    // 함수의 호출 - 인수
    add(2, 5);
    ```
- 함수의 정의
    - 함수는 함수 정의(function definition)를 통해 생성한다.
    - 함수 정의란 함수를 호출하기 이전에 인수를 전달받을 매개 변수와 실행할 문들, 그리고 반환할 값을 지정하는 것을 말한다.
    - 정의된 함수는 자바스크립트 엔진에 의해 평가되어 함수 객체가 된다.
      - cf. 값 value : 식(표현식 expression)이 평가(evaluate)되어 생성된 결과
    - 자바스크립트 함수는 다양한 방법 (함수 선언문, 함수 표현식, Function 생성자 함수, 화살표 함수)으로 정의할 수 있다.

- 함수의 호출
    - 함수를 정의하는 것으로 함수가 실행되는 것은 아니며, 함수의 실행을 명시적으로 지시해야 한다. 
    - 이를 함수 호출(function call / invoke)이라 한다. 
    - 함수를 호출하면 코드 블록에 담긴 문들이 일괄적으로 실행되고, 실행 결과, 즉 반환값을 반환한다.

<br />

### :: 함수를 사용하는 이유
1. 코드의 중복 억제, 재사용성 증진

    : 함수는 필요할 때 여러 번 호출할 수 있다. 즉, 실행 시점을 개발자가 결정할 수 있고 몇 번이든 재사용이 가능하다. 동일한 작업을 반복적으로 수행해야 한다면 미리 정의된 함수를 재사용하는 것이 효율적이다.

2. 유지보수의 편의성

    : 함수를 사용하지 않고 같은 코드를 중복해서 여러 번 작성하면 그 코드를 수정해야 할 때 중복된 횟수반큼 코드를 수정해야 한다. 따라서 중복된 횟수에 비례해서 코드 수정에 걸리는 시간이 증가한다.

3. 코드의 신뢰성

    : 사람은 실수하기 마련이므로 같은 코드를 중복해서 여러번 작성하면 그만큼 실수할 가능성도 높아진다. 코드의 중복을 억제하고 재사용성을 높이는 함수는 실수를 줄여 코드의 신뢰성을 높이는 효과가 있다.

4. 코드의 가독성

    : 적절한 함수 이름은 함수의 내부 코드를 이해하지 않고도 함수의 역할을 파악할 수 있게 돕는다. 이는 코드의 가독성을 향상시킨다.

<br />

### :: 함수 선언문과 함수 표현식, 함수의 생성 시점에 따른 차이(호이스팅)
- 함수를 정의하는 네 가지 방법
    ```jsx
    // 함수 선언문
    function add(x, y) {
        return x + y;
    }

    // 함수 표현식
    const add = function(x, y) {
        return x + y;
    } 

    // Function 생성자 함수
    const add = new Function('x', 'y', 'return x + y');

    // 화살표 함수
    const add = (x, y) => x + y;
    ```
- 함수 선언문
- 함수 표현식
    ```jsx
    // 함수 표현식
    const add = function(x, y) {
        return x + y;
    } 
    ```

    - 함수 표현식 (function expression) : 함수 리터럴로 생성한 함수 객체를 변수에 할당하여 함수를 정의하는 방식
    - 자바스크립트 함수는 객체 타입의 값이다. 자바스크립트의 함수는 값처럼 변수에 할당할 수도 있고 프로퍼티 값이 될 수도 있으며 배열의 요소가 될 수도 있다.
    - 이처럼 값의 성질을 갖는 객체를 일급 객체라 한다. 자바스크립트의 함수는 일급 객체다. 함수가 일급 객체라는 것은 함수를 값처럼 사용할 수 있다는 의미이다.
    - 익명 함수 표현식 vs. 기명 함수 표현식
        ```jsx
        // 기명 함수 표현식
        var add = function foo(x,y) {
            return x + y;
        };

        // 함수 객체를 가리키는 식별자로 호출
        add(2, 5);

        // 함수 이름으로 호출하면 Reference Error가 발생
        // 함수 이름은 함수 몸체 내부에서만 유효한 식별자다.
        foo(2, 5); // *ReferenceError : foo is not defined*
        ```
        - 함수 리터럴 의 함수 이름은 생략할 수 있다. (익명 함수)
        - 함수 표현식의 함수 리터럴은 함수 이름을 생략하는 것이 일반적
        - 함수를 호출할 때는 함수 이름이 아니라 함수 객체를 가리키는 식별자를 사용해야 한다. 함수 이름은 함수 몸체 내부에서만 유효한 식별자이므로 함수 이름으로 함수를 호출할 수 없다.
- 함수 생성 시점과 함수 호이스팅

<br />

### :: 콜백 함수 (Callback Functions)
1. 콜백 함수란?
    - 콜백 함수(callback function)는 다른 코드의 인자로 넘겨주는 함수
    
    - call + back = ‘되돌아 호출해달라’
    
    - 어떤 함수 X를 호출하면서 ‘특정 조건일 때 함수 Y를 실행해서 나에게 알려달라’는 요청을 함께 보내는 것
    
    - 요청을 받은 함수 X의 입장에서는 해당 조건이 갖춰졌는지 여부를 스스로 판단하고 Y를 직접 호출
    
    - 이처럼 콜백함수는 다른 코드(함수 또는 메서드)에게 인자로 넘겨줌으로써 그 **제어권** 도 함께 위임한 함수
    
    - 콜백 함수를 위임받은 코드는 자체적인 내부 로직에 의해 이 콜백 함수를 필요에 따라 적절한 시점에 시행

<br />

2. 제어권

    - 2-1. 호출 시점에 대한 제어권

        ```jsx
        let count = 0;

        cosnt cbFunc = function() {
            console.log(count)
            if(++count > 4) clearInterval(timer)
        }

        let timer = setInterval(cbFunc, 300)

        // -- 실행 결과 --
        // 0 (0.3초)
        // 1 (0.6초) 
        // 2 (0.9초)
        // 3 (1.2초)
        // 4 (1.5초)
        ```

        - `setInterval` 함수에 첫 번째 인자로 콜백 함수를 넘겨주자 제어권을 넘겨받은 `setInterval` 함수가 스스로의 판단에 따라 적절한 시점에(0.3초 마다) 콜백 함수를 실행
        
        - 콜백 함수의 제어권을 넘겨받은 코드는 콜백 함수 호출 시점에 대한 제어권을 가집니다.
        
        - cf. `WindowOrWorkerGlobalScope.setInterval()` (MDN)
            
            - The `setInterval()` method, offered on the `Window` and `Worker` interfaces, repeatedly calls a function or executes a code snippet, with a fixed time delay between each call.
            
            - It returns an interval ID which uniquely identifies the interval, so you can remove it later by calling `clearInterval()`.
            
            - This method is defined by the `WindowOrWorkerGlobalScope` mixin.
    
    - 2-2. 인자에 대한 제어권

        ```jsx
        const newArr = [10, 20, 30].map(function(currentVal, index) {
            console.log(currentVal, index);
            return currentVal + 5;
        });

        console.log(newArr); // [15, 20, 25]
        ```

        - 콜백 함수의 제어권을 넘겨받은 코드는 콜백 함수를 호출할 때 인자에 어떤 값들을 어떤 순서로 넘길 것인지에 대한 제어권을 가집니다.
            
            - `map` 메서드를 호출해서 원하는 배열을 얻기 위해서는 `map` 메서드에 정의된 규칙에 따라 함수를 작성해야 한다.
            
            - `map` 메서드에 정의된 규칙에는 콜백 함수의 인자로 넘어올 값들 및 그 순서도 포함돼 있다.
            
            - 콜백함수를 호출하는 주체가 사용자가 아닌 `map` 메서드 이므로 `map` 메서드가 콜백 함수를 호출할 때 인자에 어떤 값들을 어떤 순서로 넘길 것인지가 전적으로 `map` 메서드에게 달린 것
        
        - `Array.prototype.map(callback [, thisArg])`
            
            - `map` 메서드는 첫 번째 인자로 콜백 함수를 받고
            
            - 생략 가능한 두 번째 인자로 콜백 함수 내부에서 `this` 로 인식할 대상을 특정할 수 있습니다.
            
            - `thisArg` 를 생략할 경우에는 일반적인 함수와 마찬가지로 전역객체가 바인딩 됩니다.
            
            - `map` 메서드는 메서드의 대상이 되는 배열의 모든 요소들을 처음부터 끝까지 하나씩 꺼내어 콜백 함수를 반복 호출하고, 콜백 함수의 실행 결과들을 모아 새로운 배열을 만듭니다.
            
            - 콜백 함수의 첫 번째 인자에는 배열의 요소 중 현재 값이, 두 번째 인자에는 현재값의 인덱스가, 세 번째 인자에는 `map` 메서드의 대상이 되는 배열 자체가 담깁니다.
    
    - 2-3. this
        
        - 제어권을 넘겨받는 코드는 콜백 함수의 this 가 참조할 대상에 대한 제어권을 갖습니다.
            
            - "콜백 함수도 함수이기 때문에 기본적으로는 this 가 전역객체를 참조하지만, 제어권을 넘겨 받을 코드에서 콜백 함수에 별도로 this 가 될 대상을 지정한 경우에는 그 대상을 참조하게 된다."
        
        - map 메서드 구현 (this 에 대한 제어권을 가지게 되는 이유)

            ```jsx
            Array.prototype.map = function(callback, thisArg) {
                var mappedArr = [];

                for (var i = 0; i < this.length; i++) {
                    var mappedVal = callback.call(thisArg || window, this[i], i, this);
                    mappedArr[i] = mappedVal;
                }

                return mappedArr;
            };
            ```

            - 메서드 구현의 핵심은 `call` / `apply` 메서드에 있습니다.
            
            - `this` 에는 `thisArg` 값이 있을 경우에는 그 값을, 없을 경우에는 전역 객체를 지정합니다.
                
                - this 에 다른 값이 담기는 이유 : 제어권을 넘겨 받을 코드에서 `call` / `apply` 메서드의 첫 번째 인자에 콜백 함수 내부에서의 `this` 가 될 대상을 명시적으로 바인딩 하기 때문
            
            - 첫 번째 인자에는 메서드의 `this` 가 배열을 가리킬 것이므로 배열의 i 번째 요소 값을
            
            - 두 번째 인자에는 i 값을
            
            - 세 번째 인자에는 배열 자체를 지정해 호출합니다.
            
            - 그 결과가 변수 `mappedVal` 에 담겨 `mappedArr` 의 i 번째 인자에 할당됩니다.
        
        - 콜백 함수 내부에서의 this

            ```jsx
            // (1) setTimeout
            setTimeout(function () { console.log(this) }, 300); 
            // setTimeout은 내부에서 콜백함수를 호출할 때
            // call 메서드의 첫 번째 인자에 전역객체를 넘기기 때문에
            // 콜백 함수 내부에서의 this가 전역 객체를 가리킵니다.

            // (2) forEach
            [1, 2, 3, 4, 5].forEach(function (x) { console.log(this) });
            // forEach는 '별도의 인자로 this를 받는 경우'에 해당
            // 별도의 인자로 this를 넘겨주지 않았기 때문에 전역 객체를 가리키게 됩니다.

            // (3) addEventListener
            const button = document.body.querySelector('.button');
            button.addEventListener('click', function (e) { console.log(this, e) });
            // addEventListener는 내부에서 콜백 함수를 호출할 때
            // call 메서드의 첫 번째 인자에 addEventListener 메서드의 this를 그대로 넘기도록 정의
            // 콜백 함수 내부에서의 this가 addEventListener를 호출한 주체인 HTML 요소를 가리키게 된다.

            ```

<br />

3. 콜백 함수는 함수다.

    - 콜백 함수로 어떤 객체의 메서드를 전달 하더라도 그 메서드는 메서드가 아닌 함수로서 호출됩니다.

    ```jsx
    var obj = {
        vals: [1, 2, 3];
        logValues: function(v, i) {
            console.log(this, v, i)
        }
    };

    obj.logValues(1, 2); // this >>> obj : 메서드로서 호출

    [4, 5, 6].forEach(obj.logValues); // this >>> Window : 콜백 함수로서 호출
    ```

    - `[4, 5, 6].forEach(obj.logValues)`
        
        - 메서드를 `forEach` 함수의 콜백 함수로 전달
        
        - `obj` 를 this로 하는 메서드를 그대로 전달한 것이 아닌, `obj.logValues` 가 가리키는 함수만 전달
    
    - 결국 어떤 함수의 인자에 객체의 메서드를 전달하더라도 이는 결국 메서드가 아닌 함수일 뿐

<br />
 
4. 콜백 함수 내부의 this 에 다른 값 바인딩하기
    
    - "콜백 함수는 함수다." 객체의 메서드를 콜백 함수로 전달하면 해당 객체를 this 로 바라볼 수 없게 된다.
    
    - 그럼에도 콜백 함수 내부에서 this 가 객체를 바라보게 하는 방법
    
    - 방법 1) 전통적인 방법
        
        - 전통적으로는 this를 다른 변수에 담아 콜백 함수로 활용할 함수에서는 this 대신 그 변수를 사용하게 하고, 이를 클로저로 만드는 방식

        ```jsx
        // 콜백 함수 내부의 this 에 다른 값을 바인딩하는 방법(1) - 전통적인 방식
        var obj1 = {
        	name: 'obj1',
        	func: function () {
        		var self = this;
        		return function () {
        			console.log(self.name);
        		}
        	}
        }

        var callback = obj1.func();
        setTimeout(callback, 1000); // 'obj1' 출력
        ```

        - 이 방식은 실제로 this를 사용하지도 않고, 번거롭고, 메모리를 낭비하는 측면도 있음
        
        - 차라리 this 를 아예 안 쓰는 편이 더 낫겠다는 생각..

        ```jsx
        // 콜백 함수 내부에서 this를 사용하지 않는 경우
        var obj1 = {
        	name: 'obj1',
        	func: function () {
        		console.log(obj1.name);
        	}
        };

        setTimeout(obj1.func, 1000);
        ```


        - 훨씬 간결하고 직관적. 하지만 작성한 함수를 this 를 이용해 다양한 상황에 재활용할 수 없는 아쉬움.


        ```jsx
        // func 함수 재활용
        var obj2 = {
        	name: 'obj2',
        	func: obj1.func // obj1의 func 복사
        }

        var callback2 = obj2.func();
        setTimeout(callback2, 1500);

        var obj3 = { name: 'obj3' };
        var callback3 = obj1.func.call(obj3);
        setTimeout(callback3, 2000);
        ```

        - 위와 같이 전통적인 방법은 번거롭기는 하지만 this를 우회적으로나마 활용함으로써 다양한 상황에서 원하는 객체를 바라보는 콜백 함수를 만들 수 있는 방법
    
    - 방법 2) `bind` 메서드 활용

        ```jsx
        var obj1 = {
        	name: 'obj1',
        	func: function () {
        		console.log(this.name)
        	}
        };

        setTimeout(obj1.func.bind(obj1), 1000);

        var obj2 = { name: 'obj2' };
        setTimeout(obj1.func.bind(obj2), 1500);
        ```
 
<br />
 
5. 콜백 지옥과 비동기 제어
    - (내용 작성중)
