### basic
#### Hoisting
```js
console.log(x); // undefined
var x = 5;
console.log(x);// 5
```
- Nếu x chưa được khai báo thì js sẽ khai báo biến x và không gán giá trị => var x; console.log(x);

#### bind function
- set context(this) to function
```js
var mouse = {
  name: 'mickey',
  showName: function() {
    console.log(this.name);
  }
}

function run(callback) {
  callback();
}

run(mouse.showName);
run(mouse.showName.bind(mouse));
var show = mouse.showName;
show();
var bindShow = mouse.showName.bind(mouse);
bindShow();
```
#### Arrow function
```js
var mouse = {
  name: 'mickey',
  showName: function() {
    var run = function() {
      console.log(this.name);
    }

    var runArrow = () => {
      console.log(this.name);
    }

    run(); // undefined => using bind
    runArrow(); // mickey
  }
}

mouse.showName();
```

- Arrow function không có context.

#### arguments
- arguments is object like array
```js
function run() {
  var numbers = Array.from(arguments);
  /*
  arguments = {
    0: 1,
    1: 2,
    2: 3,
    3: 10,
    length: 4
  }
  */
  console.log(arguments);
  var sum = numbers.reduce((sum, num) => sum + num, 0);
  console.log(sum); // 16
}

run(1, 2, 3, 10);
```
#### apply, call
- apply(this, [param1, param2])
- call(this, param1, param2)
```js
function sum() {
  var numbers = Array.from(arguments);
  return sum = numbers.reduce((sum, num) => sum + num, 0);
}

function avg() {
  var x = sum.apply(null, arguments);// this, [param1, param2, ...]
  console.log(x / arguments.length);
}

avg(1, 2, 3, 10);

var mouse = {
  name: 'mickey',
  age: 100,
};

function showInfo() {
  console.log(`${this.name}: ${this.age}`);
}

showInfo.call(mouse);
```

#### class
```js
class Bird {
  constructor(name) {
    this.name = name;
  }

  eat() {
    console.log('Eating');
  }
}

var bird = new Bird();
bird.eat();

class Parrot extends Bird {
  fly() {
    console.log(`${this.name} is flying`);
  }
}

var parrot = new Parrot('parrot');
parrot.fly();// parrot is flying
```

- extends using constructor function

```js
function Bird(name) {
  this.name = name;
}

Bird.prototype.eat = function() {
  console.log(`${this.name} is eating`);
}

var bird = new Bird('bird');
bird.eat();

function Parrot() {
  Bird.apply(this, arguments);
}

Parrot.prototype = Bird.prototype;
var parrot = new Parrot('parrot');
parrot.eat();
```

#### super
```js
class Hero {
  constructor(name, hp, damge) {
    this.name = name;
    this.hp = hp;
    this.damge = damge;
  }

  attack(enermy) {
    enermy.hp -= this.damge;
  }
}

class HeroAttack extends Hero {
  constructor(name, hp, damge, level) {
    super(name, hp, damge);
    this.level = level;
  }
  attack(enermy) {
    super.attack(enermy);
    this.hp += this.damge;
  }
}

const heroA = new HeroAttack('A', 200, 10);
const heroB = new Hero('B', 100, 5);
console.log(heroA, heroB);
heroA.attack(heroB);
console.log(heroA, heroB);
```
#### static method
```js
function Foo() {
}

// normal method
Foo.prototype.normalMethod = function() {
  console.log('normalMethod');
}

// static method
Foo.normalMethod = function() {
  console.log('staticMethod');
}
```

#### rest
```js
function substract(minuend, ...subtrahends) { // subtrahends is array
  return subtrahends.reduce((num, subtrahend) => {
    return num - subtrahend;
  }, minuend);
}

console.log(substract(10, 1, 2, 3));
```

#### closure
```js
function debug(name) {
  return function(error) {
    console.log(`[${name}]: ${error}`);
  }
}

const log = debug('Connect');
log('Timeout');
```

#### Destructuring
```js
// Destructuring array
let array = [1, 2 , 3, 4];
let [a, b, c, d] = array;
console.log(d);
[a, , , d] = array;
console.log(d);
[a, b] = array;
console.log(b);
[a, ...b] = array;
console.log(b);
[...b] = array;
console.log(b);
array = [1];
[a, b = 20] = array;
console.log(b);

//Destructuring 

let object = {
  name: 'abc',
  age: 10,
}

let {name: x, age: y} = object;
console.log(x, y);

let {name, age} = object;
console.log(name, age);
```

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

### critical rendering path
1. concept
@media (orientation: landscape): the height is greater than or equal to the width
@media (orientation: landscape): the width is greater than the height

2 order to render HTML
- The DOM and CSSOM trees are combined to form the render tree.
- Render tree contains only the nodes required to render the page.
- Layout computes the exact position and size of each object.
- The last step is paint, which takes in the final render tree and renders the pixels to the screen.

| Normal | Async | Defer |
|
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
