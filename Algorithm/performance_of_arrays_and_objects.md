# Performance of Arrays and Objects
> Built-in Data Structures through the lens of Big O

### :: Index
- Objectives
- The Big O of Objects
- When are Arrays Slow?
- Big O of Array Methods

<br />

### :: Objectives
1. Understand how objects and arrays work, through the lens of Big O.
2. Explain why adding elements to the beginning of an array is costly.
3. Compare and contrast the runtime for arrays and objects, as well as built-in methods.

<br />

### :: The Big O of Objects
- Objects : Unordered, key value pairs

    ```jsx
    let instructor = {
        firstName: "JOON",
        isInstructor: true,
        favoriteNumbers: [1,2,3,4]
    }
    ```

- When to use objects
    
    - When you don't need order
    
    - When you need fast access / insertion / removal

- Big O of Objects
    
    - Insertion - `O(1)`
    
    - Removal - `O(1)`
    
    - Searching - `O(n)`
    
    - Access - `O(1)`
    
    - cf. searching : checking to see if a given piece of information is in a value somewhere.
    
    - cf. hash tables, hash maps

- Big O of Object Methods
    
    - Object.keys - `O(n)`
    
    - Object.values - `O(n)`
    
    - Object.entries - `O(n)`
    
    - hasOwnProperty - `O(1)` (accessing > constant time)

<br />

### :: When are Arrays Slow?

<br />

### :: Big O of Array Methods
