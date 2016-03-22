---
layout: post
title: "Importing node modules in Ember.js"
date: 2016-03-22 10:35:00 -0400
---
{% raw %}
## What about Bower?

[Bower](http://bower.io/) is great! I remember including all of my dependencies by downloading them, adding them to my `vendor` folder, checking them into my repository, and then having to figure out a way to manage keeping them up to date. Sure I could have tried to find a gem for each of them but many libraries were not wrapped by gems so then I'd have to manage my dependencies in two different ways. Bower brought sanity to this, one tool that was capable of importing any of our dependencies, and in a more manageable fashion.

Fast forward a few years and here we are in 2016, managing dependencies in our Ember projects _in two different ways_ again. It's all just JS but we've been including some libraries using [NPM](https://www.npmjs.com/) and others using Bower. Bower is not capable of managing our development dependencies so we had to turn to NPM.

The good news is that it doesn't have to be this way. The community is already making an effort to condense down to just using NPM. With ember-data being an Ember addon you no longer have to include it in both your `bower.json` and `package.json`. I have heard that they are also making an effort to move the last few ember dependencies into NPM, including ember itself.

## Marked

As I [update my markdown editor](/blog/2016/03/21/updating-my-markdown-editor) on my website I once again go looking at [chjj/marked](https://github.com/chjj/marked). It seems to have come a long way since I created my original markdown editor. They even maintain a browser version that you can include using Bower now so you don't have to [compile your own](/blog/2013/12/10/a-realtime-markdown-editor-part-1#how-to-compile-an-npm-module-to-a-web-usable-form) using [Browserify](http://browserify.org/). Thats great, but remember I'm trying to use NPM as much as possible now so here I go:

```
$ npm install --save-dev marked
```

That was so easy! I'm amazing! Now lets go write a `markdown-renderer` component and use our new NPM module.

```js
import Ember from 'ember';
import marked from 'marked';

const { Component, computed } = Ember;

export default Component.extend({
  value: null,

  htmlValue: computed('value', function() {
    let value = this.getWithDefault('value', '');
    return marked(value);
  })
});
```

This is really great! Wait...

```
Uncaught Error: Could not find module `marked` imported from `markdown-editor/components/markdown-renderer`
```

Bummer, I was so excited! Turns out marked is a CommonJS (Node) module and that doesn't play nice with ES6 import statements. I guess now I have to use the Bower version or something after all.

WRONG!!

## Browserify

Well, as I referenced once already, we could use Browserify to [compile our own](/blog/2013/12/10/a-realtime-markdown-editor-part-1#how-to-compile-an-npm-module-to-a-web-usable-form) browser friendly version of marked. We'll proabably have to add some custom build logic to our `ember-cli-build.js` file and then use `marked` as a global, or if we're feeling fancy maybe we'll wrap the global version and export it as a module so we only have to reference the global version directly once.

WRONG AGAIN!

## Ember-browserify

We are actually not the first ones to come across this problem. Our good friend [ef4](https://github.com/ef4) has already written [an ember addon](https://github.com/ef4/ember-browserify) doing all the dirty work for us.

So, to get our NPM CommonJS version of marked to work with our ES6 import, all we have to do is...

```
$ ember install ember-browserify
```

Restart our `ember server`...

And then make a slight modification to our import statement. Just append `npm` to the module name:

```js
import marked from 'npm:marked';
```

Thats it! Now it just works! Thanks Edward Faulkner and everyone else who has contributed to ember-browserify!
{% endraw %}
