# JavaScript

## Resources

* [Modern JS Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet#table-of-contents)
* [Understanding JavaScript Function Invocation and "this"](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)
  by Yehuda Katz

## Testing

### Jest

* [Jest docs: expect](https://facebook.github.io/jest/docs/en/expect.html)
* [Jest cheat sheet](https://devhints.io/jest)


## Lil' Bits

### `sleep()`ing in an asynchronous world

Helpful for debugging, e.g. to quickly simulate a slow backend.

```js
const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));

console.log('sleeping...');
await sleep(3400);
console.log('wake up!');
```
