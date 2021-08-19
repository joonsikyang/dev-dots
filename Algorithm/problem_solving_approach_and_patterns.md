# Problem Solving Approach and Patterns
### :: Index
- [Problem Solving Approach](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#-problem-solving-approach)
- [Problem Solving Patterns](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#-problem-solving-patterns)
    - [1) Frequency Counter Pattern](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#1-frequency-counter-pattern)
    - [2) Multiple Pointers Pattern](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#2-multiple-pointers-pattern)
    - [3) Sliding Window Pattern](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#3-sliding-window-pattern)
    - [4) Divide and Conquer Pattern](https://github.com/joonsikyang/dev-dots/blob/main/Algorithm/problem_solving_approach_and_patterns.md#4-divide-and-conquer-pattern)

<br />

### :: Objectives
1. Define what an algorithm is : A process or set of steps to accomplish a certain task.
2. Devise a plan to solve algorithms
3. Compare and contrast problem solving patterns

<br />

### :: Problem Solving Approach
- `Step 1 : Understand The Problem`
    - Can I restate the problem in my own words?
    - What are the inputs that go into the problem?
    - What are the outputs that should come from the solution to the problem?
    - Can the outputs be determined from the inputs? (Do I have enough information to solve the problem?)
    - How should I label the important pieces of data that are a part of the problem?
- `Step 2 : Explore Concrete Examples`
    - Start with simple examples with an input and the output.
    - Progress to more complex examples.
    - Explore examples with empty inputs.
    - Explore example with invalid inputs.
- `Step 3 : Break It Down`
    - Explicitly write out the steps you need to take.
- `Step 4 : Solve or Simplify`
    - Solve the problem.
    - If you can't, solve a simpler problem.
    - Find the core difficulty in what you're trying to do.
    - Temporarily ignore that difficulty.
    - Write a simplified solution.
    - Then incorporate that difficulty back in.
- `Step 5 : Look Back and Refactor`
    - Can you check the result?
    - Can you derive the result differently?
    - Can you understand it at a glance?
    - Can you use the result or method for some other problem?
    - Can you improve the performance of your code?
    - Can you think of other ways to refactor?
    - How have other people solved this problem?

<br />

### :: Problem Solving Patterns

#### 1) Frequency Counter Pattern
- This pattern uses objects or sets to collect values / frequencies of values.

- This can often avoid the need for nested loops of `O(n²)` operations with arrays / strings.

- It is a way of breaking down the contents of linear structure, an array or a string, and then quickly comparing that breakdown to how another object looks that was constructed from a string or an array.

- (In terms of Big O Complexity)

- Example 1) `same` function
    - 1) Nested loops of `O(n²)` operations

        ```jsx
        function same(arr1, arr2){
            if(arr1.length !== arr2.length){
                return false;
            }
            for(let i = 0; i < arr1.length; i++){
                let correctIndex = arr2.indexOf(arr1[i] ** 2) // nested loop
                if(correctIndex === -1) {
                    return false;
                }
                console.log(arr2);
                arr2.splice(correctIndex,1)
            }
            return true;
        }

        same([1,2,3,2], [9,1,4,4])
        ```

    - 2) Refactored - `O(n)`

        ```jsx
        function same(arr1, arr2){
            if(arr1.length !== arr2.length){
                return false;
            }
            let frequencyCounter1 = {}
            let frequencyCounter2 = {}
            for(let val of arr1){
                frequencyCounter1[val] = (frequencyCounter1[val] || 0) + 1
            }
            for(let val of arr2){
                frequencyCounter2[val] = (frequencyCounter2[val] || 0) + 1        
            }
            console.log(frequencyCounter1);
            console.log(frequencyCounter2);
            for(let key in frequencyCounter1){
                if(!(key ** 2 in frequencyCounter2)){
                    return false
                }
                if(frequencyCounter2[key ** 2] !== frequencyCounter1[key]){
                    return false
                }
            }
            return true
        }

        same([1,2,3,2,5], [9,1,4,4,11])
        ```

        - We had two arrays, break them down into objects that sort of classify what's in those arrays.
        
        - Then we can compare those objects, and this allows us to improve our code significantly.

- Example 2) Anagrams
    
    - An anagram is a word, phrase, or name formed by rearranging the letters of another, such as *cinema*, formed form *iceman*.
    
    - Given two strings, write a function to determine if the second string is an anagram of the first.
    
    - Exercise)

        ```jsx
        // my solution
        function validAnagram(str, str2){
            if (str.length !== str2.length) return false;
            let strObj = {};
            let str2Obj = {};
            for (let x of str) strObj[x] = (strObj[x] || 0) + 1;
            for (let x of str2) str2Obj[x] = (str2Obj[x] || 0) + 1;
            for (let key in strObj) {
                if(!(key in str2Obj)) return false;
                if(strObj[key] !== str2Obj[key]) return false;
            }
            return true;
        }

        // solution
        function validAnagram(first, second) {
          if (first.length !== second.length) {
            return false;
          }

          const lookup = {};

          for (let i = 0; i < first.length; i++) {
            let letter = first[i];
            // if letter exists, increment, otherwise set to 1
            lookup[letter] ? lookup[letter] += 1 : lookup[letter] = 1;
          }
          console.log(lookup)

          for (let i = 0; i < second.length; i++) {
            let letter = second[i];
            // can't find letter or letter is zero then it's not an anagram
            if (!lookup[letter]) {
              return false;
            } else {
              lookup[letter] -= 1;
            }
          }

          return true;
        }

        // {a: 0, n: 0, g: 0, r: 0, m: 0,s:1}
        validAnagram('anagrams', 'nagaramm')
        ```

    - When to use Frequency Counter Pattern?
    
    - Any time you have multiple pieces of data and you need to compare them in order to see if they consist of the same individual pieces.

<br />

#### 2) Multiple Pointers Pattern
- Creating **pointers** or values that correspond to an index or position and move towards the beginning, end or middle based on a certain condition.

- **Very** efficient for solving problems with minimal space complexity as well.

- Example 1) `sumZero` function
    
    - 1) nested loop

        ```jsx
        function sumZero(arr){
            for(let i = 0; i < arr.length; i++){
                for(let j = i+1; j < arr.length; j++){
                    if(arr[i] + arr[j] === 0){
                        return [arr[i], arr[j]];
                    }
                }
            }
        }
        ```

    - 2) refactor - Time Complexity : `O(n)` / Space Complexity : `O(n)`

        ```jsx
        function sumZero(arr) {
        	let left = 0;
        	let right = 0;
        	while(left < right){
        		let sum = arr[left] + arr[right];
        		if(sum === 0) return [arr[left], arr[right]];
        		if(sum > 0) right--;
        		else left++;
        	}
        }
        ```

- Example 2) `countUniqueValues`
    
    - Implement a function called countUniqueValues, which accepts a sorted array, and counts the unique values in the array.
    
    - There can be negative numbers in the array, but it will always be sorted.

    ```jsx
    // my solution
    function countUniqueValues(nums){
      if(nums.length === 0) return 0;
    	let pointer = 0;
    	let pointer2 = 1;
    	while (pointer2 < nums.length) {
    	    if (nums[pointer] !== nums[pointer2]) {
    	        nums[pointer + 1] = nums[pointer2];
    	        pointer++;
    	        pointer2++;
    	    } else {
    	        pointer2++
    	    }
    	}
    	
    	return pointer + 1;
    }

    // solution
    function countUniqueValues(arr){
    	if(arr.length === 0) return 0;
    	let i = 0;
    	for(let j = 1; j < arr.length; j++) {
    		if(arr[i] !== arr[j]){
    			i++;
    			arr[i] = arr[j];
    		}
    	}
    	return i + 1;
    }
    ```
<br />

#### 3) Sliding Window Pattern
- This pattern involves creating a **window** which can either be an array or number from one position to another.

- Depending on a certain condition, the window either increases or closes (and a new window is created).

- Very useful for keeping track of a subset of data in an array / string etc.

- Example 1) `maxSubArraySum`
    
    - Write a function called `maxSubArraySum` which accepts an array of integers and a number called `n`.
    
    - The function should calculate the maximum sum of `n` consecutive elements in the array.
    
    - naive ver. - Time Complexity :  `O(n^2)`

        ```jsx
        function maxSubarraySum(arr, num) {
          if ( num > arr.length){
            return null;
          }
          var max = -Infinity; // num could be consist of negative numbers.
          for (let i = 0; i < arr.length - num + 1; i ++){
            temp = 0;
            for (let j = 0; j < num; j++){ // nested loop... >>> O(n^2)
              temp += arr[i + j];
            }
            if (temp > max) {
              max = temp;
            }
          }
          return max;
        }

        maxSubarraySum([2,6,9,2,1,8,5,6,3],3)
        ```

    - refactored ver. - Time Complexity : `O(n)`

        ```jsx
        function maxSubarraySum(arr, num) {
        	let maxSum = 0;
        	let tempSum = 0;
        	if (arr.length < num) return null;
        	for (let i = 0; i < num; i++) {
        		maxSum += arr[i];
        	}
        	tempSum = maxSum;
        	for (let i = num; i < arr.length; i++) {
        		tempSum = tempSum - arr[i - num] + arr[i];
        		maxSum = Math.max(maxSum, tempSum);
        	}
        	return maxSum;
        }
        ```
<br />

#### 4) Divide and Conquer Pattern
- This pattern involves dividing a data set into smaller chunks and then repeating a process with a subset of data.

- This pattern can tremendously **decrease time complexity.**

- (Will be treated in later sections, for example, merge sort and quick sort.)

- Example 1) `search` function
    
    - Given a sorted array of integers, searching the value, returning the index of the value. If not, return -1.
    
    - naive ver. - Time Complexity `O(n)` / Linear Search

        ```jsx
        // Linear Search
        function search(arr, val){
            for(let i = 0; i < arr.length; i++){
                if(arr[i] === val){
                    return i;
                }
            }
            return -1;
        }
        ```

    - refactored ver. - Time Complexity `Log(n)` / Binary Search!

        ```jsx
        // Binary Search
        function search(array, val) {
         
            let min = 0;
            let max = array.length - 1;
         
            while (min <= max) {
                let middle = Math.floor((min + max) / 2);
                let currentElement = array[middle];
         
                if (array[middle] < val) {
                    min = middle + 1;
                }
                else if (array[middle] > val) {
                    max = middle - 1;
                }
                else {
                    return middle;
                }
            }
         
            return -1;
        }
        ```
<br />
