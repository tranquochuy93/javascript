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
  