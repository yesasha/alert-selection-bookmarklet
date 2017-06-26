# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.
These two things are very basic, but also important.

## Introduction to bookmarklets
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


Provide an arguments to anonymous function instead of creating local arguments explicitly.

`javascript:void((function(){var m='Hello!';alert(m)})())`
vs
`javascript:(function(m){alert(m)})('Hello!')`
12 characters less


Make aliaces





TODO:
* Eval is not scoped. See https://stackoverflow.com/questions/9781285/specify-scope-for-eval-in-javascript
* onclick is scoped
* Is global? Yes, `javascript:` is in global scope
* Length and trics
* Side script
* Urlencode?
