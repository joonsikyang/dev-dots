# TypeScript
### :: Index
- 타입이란? (타입의 원칙)
- 기본 타입 정리
- 함수에서 타입 이용하기

<br /> 

### :: 타입이란? (타입의 원칙)
- Programming 은 크게 세 가지로 구성 : Input / Operation / Output

- 프로그래밍은 이 세 가지를 반복적으로 수행할 수 있도록 코드를 작성하는 것을 의미

- 프로그래밍에 있어서 타입의 역할
    
    - `Data` (Input / Output)
        
        - 변수 : Operation 에 사용하는 데이터를 담아두는 곳이 변수
        
        - Input, Output 데이터(변수)의 타입을 지정
        
        - 해당 변수에 어떠한 데이터 타입이 저장 되는지 알 수 있음
    
    - `Function` (Operation)
        
        - 함수에 사용하는 데이터 타입을 지정
        
        - 타입을 지정함으로써 어떠한 데이터로 연산을 수행하는지, 연산의 결과 어떠한 데이터가 출력 되는지 파악할 수 있음

- 최대한 타입이 보장되는 방식으로(안정적으로) 코드를 작성하는 것이 중요 (안전성 증가, 가독성 증가, 문서화)

- 너무 광범위한 타입을 사용하거나, 타입이 보장되지 않는 방식으로 코드 작성하는 방식 지양할 것

<br />

### :: 기본 타입 정리
- 기본 타입 1 (`number`, `string`, `boolean`, `undefined`, `null`)
    ```tsx
    // 1) number
    const num: number = 5;

    // 2) string
    const str: string = 'joon';

    // 3) boolean
    const bool: boolean = false;

    // 4) undefined
    let name: undefined; // BAD (undefined 만 단독적으로 선언하지는 X)
    let age: number | undefined = 31; // optional type (cf. Union Type)
    age = undefined;
    age = 1;

    function find(): number | undefined { // 무언가를 찾았으면 number return / 그렇지 않으면 undefined return
      // return 1;
      return undefined;
    }

    // 5) null
    let size: null; // BAD (null 만 단독적으로 사용하지 X)
    let person: string | null;

    // undefined vs. null : 보편적으로는 undefined 많이 이용, 값이 있거나 없다는 것을 나타낼 때는 null 타입이 적합
    ```
- 기본 타입 2 (`unknown`, `any`, `void`, `never`, `object`)
    ```tsx
    // 1) unknown >>> BAD
    // 타입스크립트는 타입이 없는 자바스크립트와 연동해서 쓸 수 있기 때문에 이런 타입 존재
    // ex) 타입스크립트에서 자바스크립트 라이브러리를 이용할 때 return 타입을 모르는 경우
    let notSure: unknown = 9;
    notSure = 'hi';
    notSure = true;

    // 2) any >>> BAD
    let anything: any = 0;
    anything = 'hello'

    // 3) void : 함수에서 아무 값도 return 하지 않는 경우
    // return 하는 경우 return 값의 타입을 명시하는 것이 좋은 관례
    // void 생략 가능
    // 변수에 선언하는 경우는 X, 함수에 사용
    function print():void {
      console.log('hello')
      return;
    }

    // 4) never >>> 절대 return 하지 않는 함수
    // 예시 1. 에러 핸들링
    function throwError(message: string): never {
      // 1) message >>> server (log) 에러 메세지를 서버로 보내서 로그를 남기고,
      // 2) 로그를 남기고 에러를 throw, 에러를 던지면 어플리케이션이 죽기 때문에 절대 return 하지 않도록 never 타입 지정
      throw new Error(message);
    }

    // 예시 2. while 문 true 로 지정해서 계속 반복 되는 경우
    function infinite(): never { 
      while (true) { }
    }

    // 5) object : 원시 타입을 제외한 모든 object 타입 할당 가능 >>> BAD
    // 광범위하고 추상적 >>> 사용하지 않는 것이 좋음
    let obj: object;
    function acceptSomeObject(obj: object) {}

    acceptSomeObject({ name: 'joon' });
    acceptSomeObject({ animal: 'dog' });
    ```
<br />

### :: 함수에서 타입 이용하기
