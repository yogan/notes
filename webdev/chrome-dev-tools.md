# Chrome Developer Tools

## Console

### Retrieving DOM Elements

Use `$$('css-selector')`
([$$()](https://developers.google.com/web/tools/chrome-devtools/console/utilities#queryselectorall)
is equivalent to
[document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)).

This API returns an array, where you can easily call `.map()` on, etc.
(in contrast to e.g. `document.getElementsByClassName()`, which returns an
`HTMLCollection`, for which iterating
[is possible](https://stackoverflow.com/a/22754453), but a pain in the butt.)

Example usage:

```js
$$('h2').map(el => el.textContent);    // get all h2 headline texts
```

### Negative filter (remove some entries)

Since Chrome 62 (see [What's New in DevTools
62](https://developers.google.com/web/updates/2017/08/devtools-release-notes#negative-filters)):

* just use `-toBeRemoved`

Before Chrome 62:

* enable Regex
* `^((?!ToBeHidden|SomethingElse).)*$`

## Network

### Exclude resources from Chrome Extensions (e.g. Vimium)

* set filter to: `larger-than:1` (the resources have no size, they are loaded
  from disk cache)
