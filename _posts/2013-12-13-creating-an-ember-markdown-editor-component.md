---
layout: post
title:  "Creating an Ember markdown editor component"
date:   2013-12-13 08:15:00 -0500
---
{% raw %}
(If you haven't already, checked out my first post in this series: [A realtime markdown editor, Part 1](http://www.jimmylauzau.com/blog/2013/12/10/a-realtime-markdown-editor-part-1/). In that post I explain my motivation for creating this editor, I compile a NPM markdown library for use within the browser, and I create my first version of the editor.)

_The goal:_ I want to be able to include a markdown editor anywhere within my markup using the syntax below:

```
{{markdown-editor value=myMarkdownPost}}
```

I like this syntax because it looks very similar to `{{textarea value=myMarkdownPost}}` which should already be familiar.

It turns out creating an Ember component which makes this syntax possible is very easy. All you have to do is create a template named `components/markdown-editor` and include your markup for the editor within it:

```html
<script type="text/x-handlebars" id="components/markdown-editor">
  <div id="container">
    {{textarea id="input" value=value}}
    <div id="output">{{convert-markdown value}}</div>
  </div>
</script>
```

_Bonus:_ If you read my previous post, you may also notice a change in my markup for the output. I am now using a [Handlebars helper](http://emberjs.com/guides/templates/writing-helpers/) to render the markdown as html. That was also really easy to create. Here is the code:

```js
Ember.Handlebars.helper('convert-markdown', function(markdown) {
  return new Ember.Handlebars.SafeString(marked(markdown));
});
```

You can see this version of the code on [GitHub](https://github.com/jimmay5469/EmberMarkdownParser/blob/eb38f7c0f854b32f75dd91bfb9f959ace71a9c8c/index.html) and the latest version of the code on [GitHub](https://github.com/jimmay5469/EmberMarkdownParser) as well!

Demo: [Realtime Markdown Editor](/markdown-editor/)
{% endraw %}
