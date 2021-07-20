# Callback Function

### :: Index
- [콜백함수의 필요성](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98%EC%9D%98-%ED%95%84%EC%9A%94%EC%84%B1--%EC%BD%94%EB%93%9C%EC%9D%98-%ED%99%95%EC%9E%A5%EC%84%B1)
- [콜백 함수와 고차 함수](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98%EC%99%80-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98)
- [콜백 함수를 외부에서 정의하는 경우와 이유](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98%EC%99%80-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98)
- [콜백 함수의 활용](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98%EC%99%80-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98)
- [제어권](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98%EC%99%80-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98)
- [콜백 함수: 메서드가 아닌 함수](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98-%EB%A9%94%EC%84%9C%EB%93%9C%EA%B0%80-%EC%95%84%EB%8B%8C-%ED%95%A8%EC%88%98)
- [콜백 함수 내부의 this 에 다른 값 바인딩하기](https://github.com/joonsikyang/dev-dots/new/main/JavaScript#-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98-%EB%82%B4%EB%B6%80%EC%9D%98-this-%EC%97%90-%EB%8B%A4%EB%A5%B8-%EA%B0%92-%EB%B0%94%EC%9D%B8%EB%94%A9%ED%95%98%EA%B8%B0)
- [콜백 지옥과 비동기 제어]()

<br />

### :: 콜백 함수의 필요성 : 코드의 확장성

```jsx
// 어떤 일을 반복 수행하는 repeat 함수
function repeat(n) {
  // i를 출력한다.
  for (var i = 0; i < n; i++) console.log(i);
}

repeat(5); // 0, 1, 2, 3, 4
```

- `repeat` 함수는 `console.log(i)` 에 강하게 의존하고 있어 다른 일을 할 수 없다.

- 따라서 만약 `repeat` 함수의 반복문 내부에서 다른 일을 하고 싶다면 함수를 새롭게 정의해야 한다.

```jsx
// n만큼 어떤 일을 반복한다.
function repeat(n) {
  // i를 출력한다.
  for (var i = 0; i < n; i++) console.log(i);
}

repeat(5); // 0, 1, 2, 3, 4

// n만큼 어떤 일을 반복한다.
function repeat(n) {
  for (var i = 0; i < n; i++) {
    // i가 홀수일 때만 출력한다.
    if (i % 2) console.log(i);
  }
}

repeat(5); // 1, 3
```

- 함수의 일부분만 다르지만 함수를 새롭게 정의해야 하는 문제

- 이 문제는 함수를 합성하는 것으로 해결할 수 있다.

- **함수의 변하지 않는 공통 로직은 미리 정의해 두고, 경우에 따라 변경되는 로직은 추상화해서 함수 외부에서 함수 내부로 전달하는 것이다.**

```jsx
// 외부에서 전달받은 f를 n만큼 반복 호출한다.
function repeat(n, f) {
  for (var i = 0; i < n; i++) {
    f(i); // i를 전달하면서 f를 호출
  }
}

var logAll = function (i) {
  console.log(i);
}

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logAll);

var logOdds = function (i) {
  if (i % 2) console.log(i);
}

// 반복 호출할 함수를 인수로 전달한다.
repeat(5, logOdds); // 1, 3
```

- 위 repeat 함수는 경우에 따라 변경되는 일을 함수 `f` 로 추상화 했고 이를 외부에서 전달받는다.

- 자바스크립트의 함수는 일급 객체이므로 함수의 매개변수를 통해 함수를 전달할 수 있다.

- repeat 함수는 더 이상 내부 로직에 강력히 의존하지 않고 외부에서 로직의 일부분을 함수로 전달받아 수행하므로 더욱 유연한 구조를 갖게 되었다.

<br />

### :: 콜백 함수와 고차 함수
    
- `콜백 함수 (Callback Function)` : 함수의 매개변수를 통해 다른 함수의 내부로(인자로) 전달되는 함수. call + back = 되돌아 호출해달라

- `고차 함수 (HOF, Higher-Order Function)` : 매개 변수를 통해 함수의 외부에서 콜백 함수를 전달받은 함수

- 매개 변수를 통해 함수를 전달받거나 반환값으로 함수를 반환하는 함수를 함수형 프로그래밍 패러다임에서 고차 함수라 한다.

- 중첩 함수가 외부 함수를 돕는 헬퍼 함수의 역할을 하는 것처럼 콜백 함수도 고차 함수에 전달되어 헬퍼 함수의 역할을 한다.

- 단, 중첩 함수는 고정되어 있어서 교체하기 곤란하지만 콜백 함수는 함수 외부에서 고차 함수 내부로 주입하기 대문에 자유롭게 교체할 수 있다는 장점이 있다.

- **즉, 고차 함수는 콜백 함수를 자신의 일부분으로 합성한다.**

- 고차 함수는 콜백 함수를 내부로 전달 받으며 콜백 함수에 대한 **제어권**도 함께 위임 받는다.

- 고차 함수는 매개 변수를 통해 전달받은 콜백 함수의 호출 시점을 결정해서 호출한다. (호출 시점에 대한 제어권)

- 다시 말해, 콜백 함수는 고차 함수에 의해 호출 되며, 이때 고차 함수는 필요에 따라 콜백 함수에 인수를 전달할 수 있다. (인자에 대한 제어권)

- 따라서 고차 함수에 콜백 함수를 전달할 때 콜백 함수를 호출하지 않고 함수 자체를 전달해야 한다.

<br />

### :: 콜백 함수를 외부에서 정의하는 경우와 이유
    
- 콜백 함수로서 전달된 함수 리터럴은 고차 함수가 호출될 때마다 평가되어 함수 객체를 생성한다.

- 따라서 콜백 함수를 다른 곳에서도 호출할 필요가 있거나, 콜백 함수를 전달받는 함수가 자주 호출된다면 함수 외부에서 콜백 함수를 정의한 후 함수 참조를 고차 함수에 전달하는 편이 효율적이다.

```jsx
// 익명 함수 리터럴을 콜백 함수로 고차 함수에 전달한다.
// 익명 함수 리터럴은 repeat 함수를 호출할 때마다 평가되어 함수 객체를 생성한다.
repeat(5, function(i) { if(i % 2) console.log(i) }); // 1 3

// logOdds 함수는 단 한 번만 생성된다.
const logOdds = function(i) { if(i % 2) console.log(i) };
// 고차 함수에 함수 참조를 전달한다.
repeat(5, logOdds);// 1 3 
```

<br />

### :: 콜백 함수의 활용
    
- 콜백 함수는 함수형 프로그래밍 패러다임 뿐만 아니라 비동기 처리(이벤트 처리, Ajax 통신, 타이머 함수 등)에 활용되는 중요한 패턴이다.

    ```jsx
    // 콜백 함수를 사용한 이벤트 처리
    document.getElementById('button').addEventListener('click', function(){ ... });

    // 콜백 함수를 이용한 비동기 처리
    setTimeout(function(){...}, 1000);
    ```

- 콜백함수는 비동기 처리 뿐 아니라 배열 고차 함수에서도 사용된다.

    ```jsx
    // map
    const res = [1, 2, 3].map(function(item){ return item * 2 }); // [2, 4, 6]

    // filter
    const res = [1, 2, 3].filter(function(item){ return item % 2 }); // [1, 3]

    // reduce
    const res = [1, 2, 3].reduce(function(acc, cur){ return acc + cur; }, 0); // 6
    ```

<br />

### :: 제어권

- 1) 호출 시점에 대한 제어권

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

- 2) 인자에 대한 제어권

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

- 3) this 가 바라보는 대상에 대한 제어권

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
        ```

        - setTimeout은 내부에서 콜백함수를 호출할 때

        - call 메서드의 첫 번째 인자에 전역객체를 넘기기 때문에

        - 콜백 함수 내부에서의 this가 전역 객체를 가리킵니다.

        ```jsx
        // (2) forEach
        [1, 2, 3, 4, 5].forEach(function (x) { console.log(this) });
        ```

        - forEach는 '별도의 인자로 this를 받는 경우'에 해당

        - 별도의 인자로 this를 넘겨주지 않았기 때문에 전역 객체를 가리키게 됩니다.

        ```jsx
        // (3) addEventListener
        const button = document.body.querySelector('.button');
        button.addEventListener('click', function (e) { console.log(this, e) });
        ```

        - addEventListener는 내부에서 콜백 함수를 호출할 때
        - call 메서드의 첫 번째 인자에 addEventListener 메서드의 this를 그대로 넘기도록 정의
        - 콜백 함수 내부에서의 this가 addEventListener를 호출한 주체인 HTML 요소를 가리키게 된다.

<br />

### :: 콜백 함수: 메서드가 아닌 함수

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
 
### :: 콜백 함수 내부의 this 에 다른 값 바인딩하기
    
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
 
### :: 콜백 지옥과 비동기 제어
- 콜백 지옥 Callback Hell

    - 콜백 함수를 익명 함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 감당하기 힘들 정도로 깊어지는 현상.

    - 주로 이벤트 처리나 서버 통신과 같이 `비동기적인 작업`을 수행하기 위해 이런 형태가 자주 등장.

- `동기 synchronous` vs. `비동기 asynchronous`

    - 동기적인 코드

        - 현재 실행 중인 코드가 완료된후 다음 코드 실행

        - CPU의 계산에 의해 즉시 처리가 가능한 대부분의 코드는 동기적인 코드.

        - 계산식이 복잡해서 CPU가 계산하는 데 시간이 많이 필요한 경우라 하더라도 이는 동기적인 코드.

    - 비동기적인 코드

        - 현재 실행 중인 코드의 완료 여부와 무관하게 즉시 다음 코드 실행

        - **별도의 요청, 실행 대기, 보류 등과 관련된 코드**

        - 사용자의 요청에 의해 특정 시간이 경과되기 전까지 어떤 함수의 실행을 보류 (`setTimeout`)

        - 사용자의 직접적인 개입이 있을 때 비로소 어떤 함수를 실행하도록 대기(`addEventListener`)

        - 웹 브라우저 자체가 아닌 별도의 대상에 무언가를 요청하고 그에 대한 응답이 왔을 때 비로소 어떤 함수를 실행하도록 대기(`XMLHttpRequest`)

        - **현대의 자바스크립트는 웹의 복잡도가 높아진 만큼 비동기적인 코드의 비중이 예전보다 훨씬 높아진 상황**

        - (그만큼 콜백 지옥에 빠지기 쉬움)

- 콜백 지옥 예시

    ```jsx
    // callback hell
    setTimeout(function (name) { 
      var coffeeList = name;

      setTimeout(function (name) {
        coffeeList += ', ' + name;

        setTimeout(function (name) {
          coffeeList += ', ' + name;

          setTimeout(function (name) {
            coffeeList += ', ' + name;
          })
        }, 500, '카페모카')
      }, 500, '아메리카노' )
    }, 500, '에스프레소');
    ```

    - 가독성이 떨어지고 값이 전달되는 순서가 '아래에서 위로' 향하고 있어 어색함

- 콜백 지옥 해결 (전통적 방법) - 기명 함수로 변환

    ```jsx
    // 기명 함수를 사용한 해결 방식
    var coffeeList = '';

    var addEspresso = function(name) {
      coffeeList = name;
      setTimeout(addAmericano, 500, '아메리카노')
    }

    var addAmericano = function(name) {
      coffeeList = ', ' + name;
      setTimeout(addMocha, 500, '카페모카')
    }

    var addMocha = function(name) {
      coffeeList = ', ' + name;
    }

    setTimeout(addEspresso, 500, '에스프레소')
    ```

    - 가독성이 조금 높아지고 직관적

    - 하지만 일회성 함수를 전부 변수에 할당하는 것...

    - 코드명을 일일이 따라다녀야 해서 가독성 측면에서도 불편함

- 비동기 작업의 동기적 표현

    - 자바스크립트는 비동기적인 일련의 작업을 동기적으로, 혹은 동기적인 것처럼 보이게끔 처리해주는 장치를 마련하고자 끊임없이 노력

        - ES6 - `Promise`, `Generator` 도입

        - ES7 - `async` / `await` 도입

    - 비동기 작업의 동기적 표현 - 1) `Promise(1)`

        ```jsx
        // Promise(1)
        new Promise(function(resolve) {
          setTimeout(function() {
            var name = '에스프레소';
            console.log(name);
            resolve(name);
          }, 500);
        }).then(function(prevName) {
          return new Promise(function(resolve) {
            setTimeout(function() {
              var name = prevName + ', 아메리카노';
              console.log(name);
              resolve(name);
            }, 500);
          })
        }).then(function(prevName) {
          return new Promise(function(resolve) {
            setTimeout(function() {
              var name = prevName + ', 카페모카';
              console.log(name);
              resolve(name);
            }, 500);
          })
        });
        ```


        - 첫 번째로 ES6의 `Promise` 를 이용한 방식

        - `new` 연산자와 함께 호출한 `Promise` 의 인자로 넘겨주는 콜백 함수는 호출할 때 바로 실행되지만 그 내부에 `resolve` 또는 `reject` 함수를 호출하는 구문이 있을 경우 둘 중 하나가 실행되기 전까지는 다음(`then`)  또는 오류 구문(`catch`)으로 넘어가지 않습니다.

        - 따라서 비동기 작업이 완료될 때 비로소 `resolve` 또는 `reject` 를 호출하는 방법으로 비동기 작업의 동기적 표현이 가능합니다.

    - 비동기 작업의 동기적 표현 - 2) `Promise(2)`

        ```jsx
        // Promise(2)
        const addCoffee = function(name) {
          return function(prevName) {
            return new Promise(function(resolve) {
              setTimeout(function() {
                const newName = prevName ? prevName + ', ' + name : name;
                console.log(newName);
                resolve(newName);
              }, 500);
            })
          }
        };

        addCoffee('에스프레소')()
          .then(addCoffee('아메리카노'))
          .then(addCoffee('카페라떼'));
        ```

        - 위의 코드 중 반복되는 내용을 함수로 간단하게 표현한 것

        - cf. 클로저 (Closure)

    - 비동기 작업의 동기적 표현 - 3) `Generator`

        ```jsx
        // Generator
        var addCoffee = function(prevName, name) {
          setTimeout(function() {
            coffeemaker.next(prevName ? prevName + ', ' + name : name);
          }, 500);
        };

        var coffeeGenerator = function* () {
          var espresso = yield addCoffee('', '에스프레소');
          console.log(espresso);

          var americano = yield addCoffee(espresso, '아메리카노');
          console.log(americano);

          var mocha = yield addCoffee(americano, '카페모카')
          console.log(mocha);
        }

        var coffeemaker = coffeeGenerator();
        coffeemaker.next();
        ```

        - ES6 의 `Generator` 를 이용한 방법

        - 6번째 줄의 `*` 이 붙은 함수가 바로 `Generator` 함수

        - `Generator` 함수를 실행하면 `Iterator` 함수가 반환되는데, `Iterator` 는 `next` 라는 메서드를 가지고 있습니다.

        - 이 `next` 메서드를 호출하면 `Generator` 함수 내부에서 가장 먼저 등장하는 `yield` 에서 함수의 실행을 멈춥니다.

        - 이후 다시 `next` 메서드를 호출하면 앞서 멈췄던 부분부터 시작해서 그 다음에 등장하는 `yield` 에서 함수의 실행을 멈춥니다.

        - 이와같이 비동기 작업이 완료되는 시점마다 `next` 메서드를 호출해준다면 `Generator` 함수 내부의 소스가 위에서부터 아래로 순차적으로 진행됩니다.

    - 비동기 작업의 동기적 표현 - 4) `Promise + async/await`

        ```jsx
        // Promise + Async/Await
        var addCoffee = function(name) {
          return new Promise(function(resolve) {
            setTimeout(function() {
              resolve(name);
            }, 500);
          });
        };

        var coffeeMaker = async function() {
          var coffeeList = '';

          var _addCoffee = async function(name) {
            coffeeList += (coffeeList ? ',' : '') + await addCoffee(name);
          }

          await _addCoffee('에스프레소');
          await _addCoffee('아메리카노');
          await _addCoffee('카페모카');
        };

        coffeeMaker();
        ```

        - ES 2017의 `async` / `await` 을 활용하는 방법

        - 가독성이 뛰어나면서도 작성법이 간단함

        - 비동기 작업을 수행하고자 하는 함수 앞에 `async` 를 표기하고, 함수 내부에서 실질적인 비동기 작업이 필요한 위치마다 `await` 를 표기하는 것만으로 뒤의 내용을 `Promise`로 자동 전환하고, 해당 내용이 `resolve` 된 이후에야 다음으로 진행된다.

        - 즉 Promise의 then 과 흡사한 효과
