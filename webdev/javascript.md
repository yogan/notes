# JavaScript

## Resources
* [Modern JS Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet#table-of-contents)


## Lil' Bits

### `sleep()`ing in an asynchronous world
Helpful for debugging, e.g. to quickly simulate a slow backend.

```js
const sleep = (ms) => {
    return new Promise(resolve => setTimeout(resolve, ms));
};

console.log('sleeping...');
await sleep(3400);
console.log('wake up!');
```