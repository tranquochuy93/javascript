### basic
#### Array
1. Splice: adds/removes items to/from an array, and returns the removed item
  ```js
  let fruits = ["Banana", "Orange", "Apple", "Mango"];
  let removeEles = fruits.splice(2); // remove items from index = 2
  // fruits = ["Banana", "Orange"]
  // removeEles = ["Apple", "Mango"]
  ```
### export
- Name exports: are useful to export several values
```js
// Exporting individual features 
export var name1 = …, name2 = …, …, nameN; // also let, const 
  
// Export list 
export { name1, name2, …, nameN }; 
  
//Exporting everything at once 
export { object, number, x, y, boolean, string } 
  
// Renaming exports 
export { variable1 as name1, variable2 as name2, …, nameN }; 
  
// export features declared earlier 
export { myFunction, myVariable }; 

//file math.js 
function square(x) { 
  return x * x; 
} 
function cube(x) { 
  return x * x; 
} 
export { square, cube }; 
  
   
//while importing square function in test.js 
import { square, cube } from './math; 
console.log(square(8)) //64 
console.log(cube(8)) //512 
```
- Default exports: are useful to export only a single object, function, variable
```js
// file module.js 
var x=4;  
export default x; 
  
// test.js 
// while importing x in test.js 
import y from './module';  
// note that y is used import x instead of  
// import x, because x was default export 
console.log(y);         
// output will be 4 
```
- Using Named and Default Exports at the same time
```js
//module.js 
var x=2; 
const y=4; 
function fun() { 
   return "This a default export."
} 
function square(x) { 
  return x * x; 
} 
export { fun as default, x, y, square };

//test.js file 
import anyname, { x, y, square} from './module.js'; 
console.log(anyname()); //This is a default export. 
console.log(x); //2 
```
### Promise, Async / Await
ES5: callback -> ES6: Promise -> ES7: async/await
- Async - khai báo một hàm bất đồng bộ (async function someName(){...}).

  - Tự động biến đổi một hàm thông thường thành một Promise.
  - Khi gọi tới hàm async nó sẽ xử lý mọi thứ và được trả về kết quả trong hàm của nó.
  - Async cho phép sử dụng Await.
- Await - tạm dừng việc thực hiện các hàm async. (Var result = await someAsyncCall ()😉.

  - Khi được đặt trước một Promise, nó sẽ đợi cho đến khi Promise kết thúc và trả về kết quả.
  - Await chỉ làm việc với Promises, nó không hoạt động với callbacks.
  - Await chỉ có thể được sử dụng bên trong các function async.
  
  ```js
  // cách 1: 
    function getJSON() {

        // To make the function blocking we manually create a Promise.
        return new Promise( function(resolve) {
            axios.get('https://tutorialzine.com/misc/files/example.json')
                .then( function(json) {

                    // The data from the request is available in a .then block
                    // We return the result using resolve.
                    resolve(json);
                });
        });
    }
    // cách 2:
    // Async/Await approach

    // The async keyword will automatically create a new Promise and return it.
    async function getJSONAsync() {

        // The await keyword saves us from having to write a .then() block.
        return await axios.get('https://tutorialzine.com/misc/files/example.json');
    }
    
    // call async function
    getJSONAsync().then( function(result) {
        // Do something with result.
    });
  ```
  - Call mutiple independent request
   ```js
   async  function  getABC () {
      let A = await getValueA(); // getValueA takes 2 second to finish
      let B = await getValueB(); // getValueB takes 4 second to finish
      let C = await getValueC(); // getValueC takes 3 second to finish

      return (await A) * (await B) * (await C);
    }
    
    async  function  getABC () {
      // Promise.all() allows us to send all requests at the same time. 
      let results = await Promise.all([ getValueA, getValueB, getValueC ]); 

      return results.reduce((total,value) => total * value);
    }
   ```
   - catch error
   ```js
   async function doSomethingAsync(){
        try {
            // This async call may fail.
            let result = await someAsyncCall();
        }
        catch(error) {
            // If it does we will catch the error here.
        }  
    }
   ```
   ```js
   / Async function without a try/catch block.
    async function doSomethingAsync(){
        // This async call may fail.
        let result = await someAsyncCall();
        return result;  
    }

    // We catch the error upon calling the function.
    doSomethingAsync().
        .then(successHandler)
        .catch(errorHandler);
   ```
  
### Tricks
1) Remove duplicates from an Array!
```js
const array = [1, 2, 3, 2, 1, true, true, false, 'Ratul', 1, 5];
const filtered__array = [...new Set(array)];
console.log(filtered__array) // [ 1, 2, 3, true, false, 'Ratul', 5 ]
```
2) Turn a Decimal Number to a integer.
```js
const number = 23.6565
console.log(number | 0);
```
3) Getting the Last Value of an Array!
```js
const array = [1, 2, 3, 4, 5]
const last_Item = array.slice(-1)
console.log(last_Item)
```
