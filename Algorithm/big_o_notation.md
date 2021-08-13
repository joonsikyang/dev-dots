# Big O Notaion
### :: Index
- Objectives
- Intro to Big O
- Timing our code, Not Reliable.
- Counting Operations
- Big O Definition
- Simplifying Big O Expressions

<br />

### :: Objectives
1. Motivate the need for sth like Big O Notation
2. Describe what Big O Notations is
3. Simplify Big O Expressions
4. Define `time complexity` and `space complexity`
5. Evaluate the time complexity and space complexity of different algorithms using Big O Notation
6. Describe what a logarithm is

<br />

### :: Intro to Big O
- There's different approaches and implementations for the same task. Big O is about which one is best.

- " When dealing with a big application or a huge data, one algorithm implementation could save an hour every time it runs compared to another implementation. Performance matters at that point. There is an actual best algorithm."

- Big O is a numeric representation of the performance of the code

- It's a system of generalizing code and talking about it and comparing code and its performance to other pieces of code.

- Useful for discussing trade-offs between different approaches considering the context.

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

### :: 
