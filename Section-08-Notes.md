- [ ] 08 02:04:39 | More on Arrays & Iterables
  - [x] 183 01 Module Introduction | 01:08
    - Arrays and Iterables
    - Lists of Data
    - Different Ways of Creating Arrays
    - Working with Arrays - A Deep Dive!
    - Important Array Methods
    - Other Iterables: Maps & Sets
  - [x] 184 02 What are "Iterables" & "Array-like Objects"? | 02:11
    - Technically: Objects that implement the "iterable" protocol and have an @iterator method (i.e. Symbol.iterator)
    - To use humans: Objects where you can use the for-of loop
    - Not every iterable is an array!
    - Other iterables are (for example): NodeList, String, Map, Set
    - What's an "Array-Like Object"?
      - Have a length
      - Use indexes to access items
  - [x] 185 03 Creating Arrays | 08:55
    - const arr = [1];
    - const arr = Array(1);
    - const arr = new Array(1);
    - const arr = ['Hi'];
    - const arr = Array('Hi');
    - const arr = new Array('Hi');
    - const arr = Array.of(1);
    - const arr = Array.of('Hi');
    - const arr = Array.from(1);
    - const arr = Array.from('Hi');
```javascript
const numbers = [1, 2, 3]; // trailing commas work. Does that create a new element? No. Most common
```
### Alternative Techniques for Creating Arrays

```javascript
const moreNumbers = new Array(); // []

const moreNumbers = new Array('Hi', 'Welcome'); // Array of length 2

const moreNumbers = new Array(1, 5); // Array of length 2

const moreNumbers = new Array(5); // Array of length 5, with empty elements

const yetMoreNumbers = new Array.of(1, 2); // Slower performance

const moreNumbers = new Array.from(iterable); // Only accepts iterables/array-like objects as parameters
                                              // Used for converting a non-array iterable into an array
                                              // Is there a tool for converting from array to NodeList?
```

  - [ ] 186 04 Which Data Can You Store In Arrays? | 03:47
    - numbers, strings, objects
    
    ```javascript
    const hobbies = ['Cooking', 'Sports'];              // uniform data
    const personalData = [30, 'Doug', {moreDetail:[]}]; // mixed data
    
    const analyticsData = [[1, 1.6], [-5.4, 2.1]];      // nested/multidimensional data
                                                        // be careful to not use non-array elements
    
    for (const data of analyticsData) {
      for (const dataPoint of data) {
        console.log(dataPoint);
      }
    }
    ```
    - Arrays are "index-based"
    
  - [ ] 187 05 push(), pop(), unshift(), shift() - Adding & Removing Elements | 06:59
  
  ```javascript
  const hobbies = ['Sports', 'Cooking'];
  hobbies.push('Reading'); // Added to the end of the array
  
  hobbies.unshift('Coding'); // Added to the beginning of the array
  
  hobbies.pop(); // The last element of the array was removed
  const poppedValue = hobbies.pop() // Just in case I need to know what was removed
  
  hobbies.shift(); // Removes the first element of the array
  ```
  
  Why "shift" or "unshift"?
  [<strike>'A'</strike>, 'B', 'C', 'D'] // Shift to the left
  [place element in new spot, 'A', 'B', 'C', 'D'] // Unshift to the right

  - [ ] 188 06 The splice() Method | 05:37
  
  ```javascript
  hobbies.splice(startIndex, itemsToDelete, replaceables); // Only available on real arrays
  ```
  
  - [ ] 189 07 Selecting Ranges & Creating Copies with slice() | 06:06
  
    ```javascript
    const testResults = [1, 5.3, 1.5, 10.99, -5, 10];
    
    const copiedArray = testResults.slice(); // A brand-new array! Not a shared reference
    
    // Selecting a PART of an array
    
    const storedResults = testResults.slice(0, 2); // storedResults contents: [1, 5.3]
    
    const storedResults = testResults.slice(2); // storedResults contents: [1.5, 10.99, -5, 10], index 2 to the end of the array
    ```
    
  - [ ] 190 08 Adding Arrays to Arrays with concat() | 02:23
  
  ```javascript
  const storedResults = testResults.concat(); // Add arrays elements to the end of the existing array (creating a new, combined array)
  ```
  
  - [ ] 191 09 Rtrvg Idxes w indexOf() & lastIndexOf() | 03:47
  
  ```javascript
  const testResults.indexOf(1.5); // Finds the FIRST INSTANCE of the value I want the index of
  
  // lastIndexOf starts from the right
  ```
  
  - Great with primitives, reference values...not so great with those
  
  - [ ] 192 10 Finding Stuff: find() and findIndex() | 05:20
  
  - find()
  
  ```javascript
  const personData = [{ name: 'Doug' }, { name: 'Gilberto' }];
  const doug = personData.find((person, index, persons) => {
    // JavaScript will call this anonymous function for me
    // On every element in personData
    
    // returns after the first hit
    return person.name === 'Doug';
  });
  
  console.log(Doug); // returns name: 'Doug'
  
  // find() does not create a copy
  ```
  
  -findIndex()
  ```javascript
  const dougIndex = personData.findIndex((person, index, persons) => {
    // JavaScript will call this anonymous function for me
    // On every element in personData
    
    // returns after the first hit
    return person.name === 'Doug';
  });

console.log(dougIndex); // returns 0
```
  
  - [ ] 193 11 Is it Included? | 01:20
  
  ```javascript
  const incl = testResults.includes(10.99); // works on primitives
  ```
  - [ ] 194 12 Alt to for Loops: The forEach() Method | 04:24
  
  ```javascript
  const prices = [10.99, 5.99, 3.99, 6.59];
  const tax = 0.19;
  const taxAdjustedPrices = [];
  
  // Could use a for-of loop...
  
  prices.forEach((price, idx, prices) => {
    const priceObj = { index: idx, taxAdjustPrices.push(price * (1 + tax)); }
    taxAdjustPrices.push(priceObj);
  });
  ```
  
  - [ ] 195 13 Transforming Data with map() | 02:38
  
  ```javascript
  const prices = [10.99, 5.99, 3.99, 6.59];
  const tax = 0.19;
    
  prices.map((price, idx, prices) => {
    const priceObj = { index: idx, taxAdjustPrices.push(price * (1 + tax)); }
    taxAdjustPrices.push(priceObj); // Returns a NEW element for a NEW array
  });  
  ```
  
  - [ ] 196 14 sort()ing and reverse()ing | 04:15
  ```javascript
  const prices = [10.99, 5.99, 3.99, 6.59];
  const tax = 0.19;

  const sortedPrices = prices.sort(); // Sorts the array (by converting to a string [default])
  const sortedPrices = prices.sort((a, b) => {
    // sort logic
    if (a > b) {
      return 1;
    } else if (a === b) {
      return 0;    
    } else {
      return -1;
    }
  });
  
  // reverse();
  const sortedPrices = prices.reverse();
  ```
  
  - [ ] 197 15 Filtering Arrays with filter() | 02:35
  
  - A NEW array is created
  
  ```javascript
  const filteredArray = prices.filter((price, idx, prices) => {
    // returns true or false
    return price > 6;
  });
  ```
  
  - [ ] 198 16 Where Arrow Functions Shine! | 01:31
  
  ```javascript
  const filteredArray = prices.filter(price => price > 6);
  ```
  
  - [ ] 199 17 The Important reduce() Method | 07:33
  
  ```javascript
  // let sum = 0;
  
  // prices.forEach((price) => {
  //  sum += price
  // });
  
  // console.log(sum);
  
  const sum = prices.reduce((prevValue, currValue, curIndex, prices) => {
    return prevValue + curValue;
  }, 0); // optional 2nd argument; initial value
  ```
  
  - [ ] 200 18 Chaining Methods in JavaScript | 00:48
  
  - [ ] 201 19 Arrays & Strings - split() and join() | 04:21
  
  ```javascript
  const data = 'new york;10.99;2000';
  const transformedData = data.split(';'); // array with 3  elements
  
  const nameFragments = ['Doug', 'Frank'];
  const name = nameFragments.join(' '); // default separator is ','
  ```
  
  - [ ] 202 20 The Spread Operator (...) | 10:31
  
  ```javascript
  const copiedNameFragments = [...nameFragments];
  console.log(copiedNameFragments);
  
  Math.min(1, 5, -3); // -3, works with numbers, not arrays
  
  Math.min(...prices); // The spread operator makes the VALUES available
  
  For two distinctly different arrays, use map()
  ```
  
  - [ ] 203 21 Understanding Array Destructuring | 04:24
  
  ```javascript
  const nameData = ['Doug', 'Frank', 'Mr.', 10];

  // const firstName = nameData[0];
  // const lastName = nameData[1];
  
  const [firstName, lastName, ...otherInformation] = nameData;
  ```
  
  - [ ] 204 22 Maps & Sets - Overview | 04:16
  
    - Arrays
      - nested, data of any kind and length
      - iterable, many methods available
      - order is guaranteed, duplicates allowed, zero-based index access
    - Sets
      - nested, data of any kind and length
      - iterable, some special set methods
      - order is NOT guaranteed, duplicates are NOT allowed
      - no index-based access
    - Maps
      - store key-value data of any kind and length
        - any key values are allowed
      - iterable, some special map methods
      - order is guaranteed, duplicate keys are not allowed, key-based access
  
  - [ ] 205 23 Working with Sets | 07:21
  - [ ] 206 24 Working with Maps | 09:30
  - [ ] 207 25 Maps vs Objects | 03:41
  - [ ] 208 26 Understanding WeakSet | 04:50
  - [ ] 209 27 Understanding WeakMap | 02:51
  - [ ] 210 Wrap Up | 01:25
  - [ ] Useful Resources & Links | 00:12
