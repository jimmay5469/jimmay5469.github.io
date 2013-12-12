---
layout: post
title:  "A realtime markdown editor,  Part 1"
date:   2013-12-10 05:45:00
---
{% raw %}
_Note:_ I suspect this is the first of many blog "Part 1's" that may or may not get a followup.  There is definitely more I would like to play with and write about on this topic, the question is whether something else grabs my attention before I get there... but without further ado...

**TL;DR:**  This was a fun and easy problem to solve.  You can view the current version of my code on [GitHub](https://github.com/jimmay5469/EmberMarkdownParser).  Also, look down below if your interested in compiling [NPM](https://npmjs.org/) modules to a web usable form, or realtime rendering using [Ember.js](http://emberjs.com/).

_The high level problem:_ Starting a blog is something I've always wanted to do.  However, I tried a couple years ago with a [Wordpress](http://wordpress.com/) blog and decided I didn't like writing... Fast forward a year and I realized that when I was young I always had a personal website that I had created to play around with the newest HTML or CSS tricks I found online.  However, now I am more interested and invested in code than ever but I no longer had a personal site.  I began to make personal websites, and that was fun, but I also had a desire to do more spontaneous one off proof of concepts with whatever the latest cool thing I found.  I also would like to do this without throwing away my old site code and writing a new personal site every time.

Around this time I also found [Ghost](https://ghost.org/), a blogging platform which supported a realtime [markdown](http://en.wikipedia.org/wiki/Markdown) preview of your blog post as you wrote, which fascinated me.  I thought, if I could only write a blog with markdown, I would surely have a more pleasant experience writing.  Everytime I started a new one off project I took notes in a [Gist](https://gist.github.com/) anyways, what if I just refined those a little more and posted them...

While evaluating other blogging engines like Ghost, I found [Jekyll](http://jekyllrb.com/).  This seemed to bring it all together for me.  When I felt like writing a blog post, or publishing my Gists, I could write in markdown, and when I felt like demonstrating working code, I could write in pure, good old fashioned HTML.  Furthermore, call me weird but for some reason I just liked the idea of storing my posts in actual files instead of a database.  I think that has something to do with my first Wordpress blog and feeling like I didn't have real access to my content if I ever wanted to switch hosting platforms.

_The technical problem:_ I still wanted the realtime editor from Ghost!  I soon decided I should just make one.  I could embed it as a side page in my site so I could even see my posts with my current stylesheets, etc.

_The solution:_ For now, my first iteration, my "Part 1", I would just write a quick page with realtime editing capabilities but would not worry about actually having the editor save my blog posts for me.  For now I would just rely on copy/paste to and from the editor.  Later in further iterations I will worry about additional features and saving capabilities.

As I searched for javascript libraries that could parse markdown for me, I didn't find any that worked exactly how I would like.  However, I did finde a [Node.js](http://nodejs.org/) NPM module that worked just how I would like: [marked](https://github.com/chjj/marked).

_The result:_ This turned out to be much easier than I thought it would be, but I felt like I learned a few interesting things in the process:

1. How to compile an [NPM](https://npmjs.org/) module to a web usable form.
2. This code was really fun and easy to write, fun to see execute, and did I mention fun?

## How to compile an NPM module to a web usable form
_Note:_ First and foremost you will need [Node.js](http://nodejs.org/) and NPM installed on your computer.  Visit [nodejs.org](http://nodejs.org/) for more information if you need it.

Your best friend here is [Browserify](http://browserify.org/).  This makes the whole process one line of code and one or two terminal commands.

1. Install browserfiy: `npm install -g browserify`
2. Install marked: `npm install marked`
3. Create a file called `markedModule.js` with the following line of code: `window.marked = require('marked');`  (_Note:_ you can actually call the file whatever you want)
4. Run the following Browserify command in your terminal: `browserify markedModule.js -o marked.js`
5. Include a script tag to `marked.js` in your webpage and use marked as specified in their [GitHub page](https://github.com/chjj/marked).

##Realtime rendering with Ember.js
I've pretty much been doing everything with [Ember](http://emberjs.com/) lately and love it.  If you're not using Ember then you should check it out, or at least use [Angular](http://angularjs.org/) or something, although I suppose you could always use [jQuery](http://jquery.com/) if you wanted, but that would make me :(.

I would like to roll this into an [Ember component](http://emberjs.com/api/classes/Ember.Component.html) or [Angular directive](http://docs.angularjs.org/guide/directive) later but for now here we are:

1. You're gonna need an object with a markdown and an html property that is smart enough to do the conversion:

    ```js
    App.MarkdownParser = Ember.Object.extend({
      markdown: null,
      html: function() {
        return marked(this.get('markdown'));
      }.property('markdown')
    });
    ```

2. You're going to need to define your application route with your model object:

    ```js
    App.ApplicationRoute = Ember.Route.extend({
      model: function() {
        return App.MarkdownParser.create({
          markdown: "#something"
        });
      }
    });
    ```

3. Your will need to define your application template with a textbox and an output pane (notice that the output pane uses a tripple handlebar so that it does not escape the html):

    ```html
    <script type="text/x-handlebars">
      {{textarea id="input" value=markdown}}
      <div id="output">{{{html}}}</div>
    </script>
    ```

Thats pretty much it.  You can see this version of the code on [GitHub](https://github.com/jimmay5469/EmberMarkdownParser/tree/9a4b8689c77ff8c8eff5d833d4f674be8c776b5a/index.html) and the latest version of the code on [GitHub](https://github.com/jimmay5469/EmberMarkdownParser) as well!
{% endraw %}
