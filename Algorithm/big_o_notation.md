# Big O Notaion
### :: Index
- [Objectives](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-objectives)
- [Intro to Big O](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-intro-to-big-o)
- [Timing our code, Not Reliable.](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-timing-our-code-not-reliable)
- [Counting Operations](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-counting-operations)
- [Big O Definition](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-big-o-definition)
- [Simplifying Big O Expressions](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-simplifying-big-o-expressions)
- [Space Complexity](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-space-complexity)
- [Logs](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-logs)
- [Section Recap](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/big_o_notation.md#-section-recap)

<br />

### :: Objectives
1. Motivate the need for Big O Notation
2. Describe what Big O Notations is
3. Simplify Big O Expressions
4. Define `time complexity` and `space complexity`
5. Evaluate the time complexity and space complexity of different algorithms using Big O Notation
6. Describe what a logarithm is

<br />

### :: Intro to Big O
- There's different approaches and implementations for the same task. Big O is about which one is the best.

- "When dealing with a big application or a huge data, one algorithm implementation could save an hour every time it runs compared to another implementation. Performance matters at that point. There is an actual best algorithm."

- Big O is a numeric representation of the performance of the code.

- It's a system of generalizing code and talking about it and comparing code and its performance to other pieces of code.

- It is usseful for discussing trade-offs between different approaches considering the context of the code.

- When your code slows down or crashes, identifying parts of the code that are inefficient can help us find pain points in our applications.

- Less important: it comes up in interviews!

<br />

### :: Timing our code, Not Reliable.
- comparing two solutions to the same problem - `addUpTo` function

- solution 1)

    ```jsx
    function addUpto(n) {
    	let total = 0;
    	for (let i = 1; i <= n; i++) {
    		total += i;
    	}
    	return total;
    }
    ```

- solution 2)

    ```jsx
    function addUpTo(n) {
    	return n * (n + 1) / 2
    }
    ```

- Which one is better?
    
    - What does better mean?
    
    - Faster? Less memory-intensive? More readable?
    
    - Let's focus on the speed of the code execution.
    
    - Manually checking the time? The Problem with Time.
        
        - Different machines will record different times.
        
        - Even the same machine will recored different times.
        
        - For fast algorithms, speed measurements may not be precise enough.
    
    - Timing our code, Not reliable.

<br />

### :: Counting Operations
- If not time, then what?
    
    - Rather than counting `seconds`, which are so variable...
    
    - Let's count `the number of simple operations` the computer has to perform.

- Counting Operations
    - solution 1 - the number of operations grows roughly proportionally with `n`
    
    - solution 2 - 3 simple operations, regardless of the size of `n`

<br />

### :: Big O Definition
- Big O Notation is a way to formalize how the runtime of an algorithm grows as the inputs grow.

- We won't care about the details, only the broad trends.

- Bit O Definition
    
    - We say that an algorithm is `O(f(n))` if the number of simple operations the computer has to do is eventually less than a constant times `f(n)`, as `n` increases.
    
    - `f(n)` could be constant : `1`
    
    - `f(n)` could be linear : `n`
    
    - `f(n)` could be quadratic : `n²`
    
    - `f(n)` could be sth entirely different.

- Example
    
    - Example 1)

        ```jsx
        // 3 simple operations, regardless of the size of n
        function addUpTo(n) {
        	return n * (n + 1) / 2
        }
        ```

        - Always 3 operations
        
        - `O(1)`
    
    - Example 2)

        ```jsx
        // the number of operations grows roughly proportionally with n
        function addUpto(n) {
        	let total = 0;
        	for (let i = 1; i <= n; i++) {
        		total += i;
        	}
        	return total;
        }
        ```

        - Number of operations is (eventually) bounded by a multiple of `n` (say, `10n`)
        
        - `O(n)`
    
    - Example 3)

        ```jsx
        function countUpAndDown(n) {
        	// O(n)
        	for(let i = 0; i < n; i++) {
        		console.log(i);
        	}
        	// O(n)
        	for(let j = n - 1; j >= 0; j--) {
        		console.log(j);
        	}
        }
        ```

        - Number of operations is (eventually) bounded by a multiple of `n` (say, `10n`)
        
        - `O(n)`
    
    - Example 4)

        ```jsx
        function printAllPairs(n) {
        	for (let i = 0; i < n; i++) { // O(n)
        		for (let j = 0; j < n; j++) { // O(n)
        			console.log(i, j);
        		}
        	}
        }
        ```

        - `O(n)` operation inside of an `O(n)` operation
        
        - `O(n²)`

<br />

### :: Simplifying Big O Expressions
- Constants Don't Matter
    - `O(2n)` >>> `O(n)`
    - `O(500)` >>> `O(1)`
    - `O(13²`) >>> `O(n²)`

- Smaller Terms Don't Matter
    - `O(n + 10)` >>> `O(n)`
    - `O(1000n + 50)` >>> `O(n)`
    - `O(n² + 5n + 8)` >>> `O(n²)`

- There are several rules that can help as a starting point. (Big O Shorthands)
    - Arithmetic operations are constant
    - Variable assignment is constant
    - Accessing elements in an array (by index) or object(by key) is constant
    - In a loop, the time complexity is the length of the loop times the complexity of whatever happens inside of the loop

- Example 1) `O(n)`

    ```jsx
    function logAtLeast5(n) {
      for (var i = 1; i <= Math.max(5, n); i++) {
        console.log(i);
      }
    }
    ```

- Example 2) `O(1)`

    ```jsx
    function logAtMost5(n) {
      for (var i = 1; i <= Math.min(5, n); i++) {
        console.log(i);
      }
    }
    ```

<br />

### :: Space Complexity
- `Time complexity` : analyzing the runtime of an algorithm as the size of the inputs increases.

- `Space complexity` : analyzing how much additional memory we need to allocate in order to run the code in algorithm.
    
    - `Auxiliary space complexity` : space required by the algorithm, not including space taken up by the inputs.
    
    - When we talk about space complexity, it is about `auxiliary space complexity`. We care about algorithm itself, not about the inputs, focusing on what happens inside the algorithm.

- Space Complexity in JS (Rules of Thumb)
    
    - Most primitives (`booleans`, `numbers`, `undefined`, `null`) are constant space.
    
    - Strings require `O(n)` space (where `n` is the string length)
    
    - Referenced types are generally `O(n)`, where n is the length (for arrays) or the number of keys (for objects)

- Example 1) `O(1)` space

    ```jsx
    function sum(arr) {
      let total = 0; // one number
      for (let i = 0; i < arr.length; i++) { // another number (let i = 0)
        total += arr[i];
      }
      return total;
    }
    ```

- Example 2) `O(n)` space

    ```jsx
    function double(arr) {
      let newArr = [];
      for (let i = 0; i < arr.length; i++) {
        newArr.push(2 * arr[i]);
      }
      return newArr; // n numbers
    }
    ```

<br />

### :: Logs
- Logarithms
    
    - Besides `O(n)`,  `O(1)`, `O(n²)`, which is the most common complexities, big O expression involve more complex mathematical expressions which might appear often.
    
    - Certain searching algorithms have logarithmic time complexity.
    
    - Efficient sorting algorithms involve logarithms.
    
    - Recursion sometimes involves logarithmic space complexity
    
    - and more.

- What's a log?
    
    - `Logarithmic form`  >>>  `Exponential form`
    
    - `log2(8) = 3`  >>>  `2^3 = 8`
    
    - `log2(value) = exponent`  >>>  `2^exponent = value`
    
    - We'll omit the 2. `log` === `log2`
    
    - The logarithm of a number roughly measures the number of times you can divide that number by 2 before you get a value that's less than or equal to one.
    
    - ex. log(8) = 3 / log(25) = 4.64

- Logarithm Complexity

    <img width="600" alt="Screen Shot 2021-08-14 at 2 14 25 PM" src="https://user-images.githubusercontent.com/43266792/129434931-efa62b1d-034f-41be-9627-201ffe9e6f71.png">

<br />

### :: Section Recap
- To analyze the performance of an algorithm, we use Big O Notation.

- Big O Notation can give us a high level understanding of the time or space complexity of an algorithm.

- Big O Notation doesn't care about precision, only about general trends (linear? quadratic? constant?)

- The time or space complexity (as measured by Big O) depends only on the algorithm, not the hardware used to run the algorithm.

- Big O Notation is everywhere, so get lots of practice!
