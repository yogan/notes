# Chrome Developer Tools

## Console

### Negative filter (remove some entries)
* enable Regex
* `^((?!ToBeHidden|SomethingElse).)*$`

## Network

### Exclude resources from Chrome Extensions (e.g. Vimium)
* set filter to: `larger-than:1` (the resources have no size, they are loaded from disk cache)
