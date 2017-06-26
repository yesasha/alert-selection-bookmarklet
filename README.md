# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.

These two things are very basic, but also important.
[Bookmarklets](https://en.wikipedia.org/wiki/Bookmarklet) are a very interesting mechanism that allows you to run a javascript code on any page. Most desktop browsers support extensions, which are much more powerfull, but mobile browsers luks it in general. Bookmarklets allow you to extend the functionality of almost all browsers (desktop and mobile).

So how do you make it?
To make a bookmarklet you must create a link starting with "javascript:" protocol. Something like `javascript:alert("Hello!")` test it javascript:alert("Hello!") or if you have a variables you may wrap your code in anonimous function `javascript:function(){var message = "Hello!";alert(message)}` test it javascript:function(){var message = "Hello!";alert(message)}
