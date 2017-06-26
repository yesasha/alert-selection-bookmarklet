# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.
These two things are very basic, but also important.

## Introduction to bookmarklets
[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) are a very interesting mechanism that allows you to run your javascript code on any page. Most desktop browsers support extensions, which are much more powerfull, but mobile browsers laks it in general. Bookmarklets allow you to extend the functionality of almost all browsers (desktop and mobile).

### So how do you make it?

To make a bookmarklet you must create a link starting with "javascript:" protocol, follow by javascript code. Something like `javascript:alert("Hello!")` or if you have a variables you may wrap your code in anonymous function `javascript:(function(){var message = "Hello!";alert(message)})()` since 'javascript:' protocol evaluates in global scope. A bookmarklet must not return anything. If it returns the browser will replace the current page with the result. So you may want to wrap the last statement in a void(), to prevent this.
Bookmarklet length is limited to an url length.

