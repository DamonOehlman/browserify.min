# The Guide to Smaller Browserified JS

I'm a massive fan of [browserify](https://github.com/substack/node-browserify). If I'm telling people to do __just one thing__ to improve their own experience with writing JS for a browser environment, it's to use browserify (ideally in conjuction with a tool like [beefy](https://github.com/chrisdickinson/beefy)).

As it's evolved, browserify has continued to improve as a tool.  Actually, let's call it a weapon.  Now at major version 4, browserify is a sharp, well crafted weapon that allows even a beginner swordsperson to do real damage to the enemies of efficient and modular clientside code.  There is a lot to know though, and as you journey with your trusty blade it's important to know some more advanced moves.

This short guide provides some specific information on how to tune your packages to reduce the size of the resulting browserified JS.  Before reading this guide I would recommend reading [@substack](https://github.com/substack)'s [browserify handbook](https://github.com/substack/browserify-handbook) as that provides an excellent cross-section of information.
