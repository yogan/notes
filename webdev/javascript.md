# JavaScript

## Resources

* [How Web Apps Work](https://blog.isquaredsoftware.com/2020/11/how-web-apps-work-client-dev-deployment)
  by Mark Erikson - has a nice description of the mess that is (was) JS module
  formats
* [Modern JS
  Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet#table-of-contents)
* [Understanding JavaScript Function Invocation and
  "this"](https://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)
  by Yehuda Katz
* [Jake Archibald: In The Loop](https://youtu.be/cCOL7MC4Pl0)
  (JSConf.Asia 2018, YouTube, 35 min.) - JS event loop, tasks, microtasks, promises,
  `setTimeout`, `requestAnimationFrame`, event listeners

## Testing

### Jest

* [Jest docs: expect](https://facebook.github.io/jest/docs/en/expect.html)
* [Jest cheat sheet](https://devhints.io/jest)
* [But really, what is a JavaScript mock?](https://kentcdodds.com/blog/but-really-what-is-a-javascript-mock)
  by Kent C. Dodds - nice article how you would implement a JS mock yourself,
  and how to use Jest's module mocking

## Lil' Bits

### `sleep()`ing in an asynchronous world

Helpful for debugging, e.g. to quickly simulate a slow backend.

```js
const sleep = ms => new Promise(resolve => setTimeout(resolve, ms));

console.log('sleeping...');
await sleep(3400);
console.log('wake up!');
```
