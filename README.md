# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.
These two things are very basic, but also important.

## Introduction to bookmarklets
[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) are a very interesting mechanism that allows you to run your javascript code on any page. Most desktop browsers support extensions, which are much more powerfull, but mobile browsers laks it in general. Bookmarklets allow you to extend the functionality of almost all browsers (desktop and mobile).

### So how do you make it?

To make a bookmarklet you must create a link starting with "javascript:" protocol. Something like `javascript:alert("Hello!")` or if you have a variables you may wrap your code in anonimous function `javascript:(function(){var message = "Hello!";alert(message)})()` since 'javascript:' protocol evaluates in global scope. A bookmarklet must not return anything. The `return` instruction will lead to syntax error, the same way it does when you put `return` in your code in global scope. But you probably won't do that. I saw people wrapping the whole thing in `void()`, but I don't see the point, since as far as I've tested, if you return a value from inside the anonimous function, it doesn't harm. So `javascript(function(){/* Your code here*/})()` is anough.

TODO:
* Eval is not scoped. See https://stackoverflow.com/questions/9781285/specify-scope-for-eval-in-javascript
* onclick is scoped
* Is global? Yes, `javascript:` is in global scope
* Length and trics
* Side script
