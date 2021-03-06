# The Guide to Smaller Browserified JS

First, and foremost:

## Use Browserify

I'm a massive fan of [browserify](https://github.com/substack/node-browserify). If I'm telling people to __do just one thing to improve their own experience with writing JS for a browser environment__, it's to use browserify (ideally in conjuction with a tool like [beefy](https://github.com/chrisdickinson/beefy)).

As it's evolved, browserify has continued to improve as a tool.  Actually, let's call it a weapon.  Now at major version 4, browserify is a sharp, well crafted weapon that allows even a beginner swordsperson to do real damage to the enemies of efficient and modular clientside code.  There is a lot to know though, and as you journey with your trusty blade it's important to know some more advanced moves.

This short guide provides some specific information on how to tune your packages to reduce the size of the resulting browserified JS.  Before reading this guide I would recommend reading [@substack](https://github.com/substack)'s [browserify handbook](https://github.com/substack/browserify-handbook) as that provides an excellent cross-section of information.

## Understanding the Overheads of Browserify

Browserify incurs __minimal overheads__ on your code.  Consider the following example of two modules:

`a.js`:

```js
module.exports = function(message) {
  console.log(message);
};
```

`b.js`:

```js
var a = require('./a');
a('hello');
```

At a raw code level, the two files above are around 100 bytes.  When browserified (try `browserify examples/01-overhead/b.js | wc -c`) we get something around 613 bytes. So we are paying a cost of around 500 bytes for improved modularity in our code.  I don't know about you but that's something I can live with.

## Keeping an Eye on the Size

One of the main benefits of using browserify is that it uses static analysis to determine what modules should be included into your code.  Through using this technique browserify provides a __low-friction approach__ to bundling code that feels very "node-like" for a browser environment.

It is, however, possible to increase the size of your code quite significantly with just a couple of `require` statements.  I will go into more detail on the main offenders later, but for now I would simply recommend getting into the habit of running the following command in any package that we are targeting for browser distribution:

```
browserify . --standalone test | uglifyjs | wc -c
```

Please note, while I'm asking you to keep an eye on the resulting size of a package in the browser, I'm begging you not to obsess over it.

__NEVER:__

- trade away better functionality for a package/module with fewer bytes.
- start any kind of thorough size optimization too early.

  _(As a side note, I'm only writing this guide after now beginning to seriously optimize the size of [rtc.io](https://github.com/rtc-io) packages now - which is almost 12 months after the first commit on some of the packages)_.
