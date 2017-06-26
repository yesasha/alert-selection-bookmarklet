# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.
These two things are very basic, but also important.

## Bookmarklets
[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) are a very interesting mechanism that allows you to run your javascript code on any page. Most desktop browsers support extensions, which are much more powerfull, but mobile browsers laks it in general. Bookmarklets allow you to extend the functionality of almost all browsers (desktop and mobile).

### So how do you make it?

To make a bookmarklet you must create a link starting with "javascript:" protocol, follow by javascript code. Something like `javascript:alert("Hello!")` or if you have a variables you may wrap your code in anonymous function `javascript:(function(){var message = "Hello!";alert(message)})()` since 'javascript:' protocol evaluates in global scope. A bookmarklet must not return anything. If it returns the browser will replace the current page with the result. So you may want to wrap the last statement in a void(), to prevent this.

### Trics to minification

The bookmarklet length is limited to an url length.

If you are shure, you script doesn't return a value, you may omit a void()
`javascript:void((function(){var message = 'Hello!';alert(message)})())`
vs
`javascript:(function(){var message = "Hello!";alert(message)})()`
The second is 6 characters less.

javascript:(function(){var message = "Hello!";alert(message)})()

Provide an arguments to anonymous function instead of creating local arguments explicitly.

`javascript:void((function(){var m='Hello!';alert(m)})())`
vs
`javascript:(function(m){alert(m)})('Hello!')`
12 characters less

`javascript:!function(m){alert(m)}('Hello!')`
Minus one

Make aliaces and functions if you have a repeated code.

```javascript
javascript:void((function () {
    var d = document,
        h = d.getElementsByTagName('h')[0],
        s = d.createElement('s');

    s.src = 'source_file.js';
    h.appendChild(s);
})())
```

`var h=document.getElementsByTagName('head')[0],s=document.createElement('script');`
vs
`var d=document,h=d.getElementsByTagName('head')[0],s=d.createElement('script');`
3 characters less


This one will give better results if you'll use `document` more times.
Also, this is an example of how to load an external script if you can't fit your code.


### Urlencode
https://stackoverflow.com/questions/33896431/what-is-the-proper-way-to-url-encode-javascript-in-a-bookmarklet

As I've uderstood from there is that you can urlencode entire code, but if you only replace those 3 characters (new lines, # and %) everything will still work.


## Selection
The second thing is [selection](https://developer.mozilla.org/en-US/docs/Web/API/Selection_API). You want your bookmarklet to do something usefull with something that user points to. One way for the user to point on specific part in document is to select it. There is an example in an above link.




TODO:
* Eval is not scoped. See https://stackoverflow.com/questions/9781285/specify-scope-for-eval-in-javascript
* onclick is scoped
* Is global? Yes, `javascript:` is in global scope
* Length and trics
* Side script
* Urlencode?
