# Chrome Developer Tools

## Console

### Negative filter (remove some entries)

Since Chrome 62 (see [What's New in DevTools 62](https://developers.google.com/web/updates/2017/08/devtools-release-notes#negative-filters)):

* just use `-toBeRemoved`

Before Chrome 62:

* enable Regex
* `^((?!ToBeHidden|SomethingElse).)*$`

## Network

### Exclude resources from Chrome Extensions (e.g. Vimium)

* set filter to: `larger-than:1` (the resources have no size, they are loaded from disk cache)
