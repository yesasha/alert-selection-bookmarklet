# alert-selection-bookmarklet
Simple project that shows how to get selected text and how to create a bookmarklet.
These two things are very basic, but also important.

## Bookmarklets
[Bookmarklet](https://en.wikipedia.org/wiki/Bookmarklet) is a javascript stored as a bookmark in browser. While normal links start with `http:` protocol, bookmarklets start with `javascript:`. It is a very interesting mechanism that allows you to run your javascript code on any page. Most desktop browsers support extensions, which are much more powerfull, but mobile browsers laks it in general. Bookmarklets allow you to extend the functionality of almost all browsers (desktop and mobile). `javascript:` protocol is not defined in web standarts.


### So how do you make it?

To make a bookmarklet you must create a link starting with "javascript:" protocol, followed by javascript code. Something like `javascript:alert("Hello!")`. A bookmarklet should not return anything. If it returns, the browser will replace the current page with the result equivalent to `document.write(lastReturnedValue)`. To prevent this you may put `void(0)` to the end of your code or wrap all your code in `void(your code)`. But there is another and better way. Since 'javascript:' protocol evaluates in global scope you will not want to put variables there, so wrap your code in anonymous function, or better say immediately-invoked function expression: `javascript:(function(){var m='Hello!';alert(m)})()`. Sometimes, immediately-invoked function expressions are written like this: `!function(){}()`. This is not good for bookmarklets, since it will return "true". Now your code evaluates in its own scope and since you are not explicitly returning any value it will return `undefined`.

<del>You can (or you can tell to the user of your page to) go to browser's bookmarks manager and create it manually.</del> Create a link like this `<a href="javascript:alert("Hello!")"></a>` and ask user to drag it to bookmarks panel.


<s>So you may want to wrap the last statement in a void(), to prevent this. or if you have a variables you may wrap your code in anonymous function or better say immediately-invoked function expression `javascript:(function(){var message = "Hello!";alert(message)})()` since 'javascript:' protocol evaluates in global scope. A bookmarklet must not return anything. If it returns, the browser will replace the current page with the result. So you may want to wrap the last statement in a void(), to prevent this. Sometimes, immediately-invoked function expression is written like this: `!function(){}()`. This is not good for bookmarklets, since it will return "true".</s>

### Tricks to minification

The bookmarklet's length is limited to an url length. In some browsers it may be very small, less than 500 characters.

<s>If you are shure, you script doesn't return a value, you may omit a void()
`javascript:void((function(){var message = 'Hello!';alert(message)})())`
vs
`javascript:(function(){var message = "Hello!";alert(message)})()`
The second is 6 characters less.

javascript:(function(){var message = "Hello!";alert(message)})()</s>

#### Minifier
Use "one character" names and remove linebreaks and unneeded spaces (this will probably be done by minifiers).


#### New lines
Your final code must not contain new lines. If you want to know how to treat them anyway, other than avoid, for example while debugging, you may test it yourself.

#### Aliaces and functions
Make aliaces and functions if you have a repeated code.

```javascript
javascript:void((function () {
    var d = document,
        h = d.getElementsByTagName('h')[0],
        s = d.createElement('script');

    s.src = 'source_file.js';
    s.type = 'text/javascript';
    h.appendChild(s);
})())
```

```
var h=document.getElementsByTagName('head')[0],s=document.createElement('script');
```
vs
```
var d=document,h=d.getElementsByTagName('head')[0],s=d.createElement('script');
```
3 characters less


The more times you'll use `document` in your script the bigger will be difference.
But if the initial name is short, then it will have inverse effect, and you will get a bigger code. Same with functions. The `function` string is long anough, so creating a function will lead to a bigger code. So you have to compare both versions.
Also, this is an example of how to load an external script if you can't fit your code.

#### text/javascript
Do you need to set a type? As you are targeting any page written by others, it may be non html5, so you need to set a type. Moreover, if you are loading an external script, you are no more limited to the size.



#### Variables
Provide an arguments to anonymous function instead of creating local variables explicitly.

`javascript:(function(){var m='Hello!';alert(m)})()`
vs
`javascript:(function(m){alert(m)})('Hello!')`
6 characters less





### Urlencode and escape
Actually there are 2 problems.

1. Put your string of code into addressbar. For this you need to replace/escape characters that are forbidden for url. When browser sees the "javascript:" protocol, it understands, that there is a javascript code. So you no longer need to escape all those url specific symbols like "?", "&", "#". All you need to encode is "%" symbol. Replace it with %25 or put a space after it, so browser will not recognize it as persent encoding. <del>This is not 100% shure, it depends on browser and there is no defined standard about javascript protocol.</del>



2. Put your string of code into "href" attribute of an \<a\> tag. For this you need to replace/escape characters that are forbidden for html/attribute. This is a quote symbol. If you are using double quotes in html, then you can use single quotes in javascript and vice versa.  You may encode quotes inside javascript with `&quot;`, then, when bookmarked it will be replaced by the browser with quotes. And if user decides to put his bookmarklet back to the link, he will need to encode quotes again. If you encode quotes with percent encoding `%22` for `"` and `%27` for `'`, it will be left intact, and bookmarklet will be "cross usable". But another problem pops up. Now it's not a valid javascript code. So opening it in your javascript editor may become a problem. The same thing with an `&` sign, since it is used to escape html entities. Most browsers will understand it as is, but who knows? You may encode it with `&amp;` or with `%26` as you did it with quotes. `%26` is better choice, because it seems, that accepting `&` symbol only as is in `href` attribute, may become a standart behaviour.






<s>https://stackoverflow.com/questions/33896431/what-is-the-proper-way-to-url-encode-javascript-in-a-bookmarklet

As I've uderstood from there is that you can urlencode entire code, but if you only replace those 3 characters (new lines, # and %) everything will still work.</s>











## Selection
The second thing is [selection](https://developer.mozilla.org/en-US/docs/Web/API/Selection_API). You want your bookmarklet to do something usefull with something that user points to. One way for the user to point on specific part in document is to select it. There is an example in an above link.

https://stackoverflow.com/questions/5379120/get-the-highlighted-selected-text








TODO:
* Eval is not scoped. See https://stackoverflow.com/questions/9781285/specify-scope-for-eval-in-javascript
* onclick is scoped
* Is global? Yes, `javascript:` is in global scope
* Length and tricks
* Side script
* Urlencode?
* Should set `script.type = 'text/javascript';`?
* Click problem. document.execCommand(‘cut’/‘copy’) was denied because it was not called from inside a short running user-generated event handler. Javascript protocol link is not evaluated inside short running user-generated event handler in firefox.
* Get selection from textarea
* Frame problem. Put javascript to iframe
* Minifiers does not minify
* Avoid returns, use state.
* Can run bookmarklet inside iframe?
* Referrer, opener not always pass
* How to put it to toolbar in ie?
* https to http block
* Check if there is an instance running, or there is an effect applied.
* Why it is good to use alerts and prompt?
* Don't use html5 tags and html5 at all if you want it to be crossusable
