# Performance of Arrays and Objects
> Built-in Data Structures through the lens of Big O

### :: Index
- Objectives
- The Big O of Objects
- The Big O of Arrays

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

### :: The Big O of Arrays
- Arrays : Ordered lists

    ```jsx
    let names = ["Michael", "Melissa", "Andrea"];
    let values = [true, {}, [], 2, "awesome"];
    ```

- When to use Arrays
    
    - When you need order (cf. linked list)
    
    - When you need fast access / insertion and removal (depends on what you're trying to do)

- Big O of Arrays (When are Arrays Slow?)
    
    - Searching - `O(n)`
    
    - Access - `O(1)`
    
    - Insertion - It depends...
        
        - Inserting at the end - `O(1)`
        
        - Inserting at the beginning - `O(n)` (reindexing)
      
    - Removal - It depends...
        
        - Removing the last element - `O(1)`
        
        - Removing the first element - `O(n)` (reindexing)

- Big O of Array Methods

    - push - `O(1)`
    
    - pop - `O(1)`
    
    - shift - `O(n)`
    
    - unshift - `O(n)`
    
    - concat - `O(n)` (it grows in proportion with the total size of the new array)
    
    - slice - `O(n)`
    
    - splice - `O(n)`
    
    - sort - `O(N * logN)` (slowest thing in here)
    
    - forEach / map / filter / reduce / etc. - `O(n)`
