---
layout: post
title: "Updating my markdown editor"
date: 2016-03-21 10:45:41 -0400
---
{% raw %}
It has been a couple years since I created my markdown editor and the couple of posts that go with it (See: [A realtime markdown editor, Part 1](/blog/2013/12/10/a-realtime-markdown-editor-part-1) and [Creating an Ember markdown editor component](/blog/2013/12/13/creating-an-ember-markdown-editor-component)). Since then many things have changed in Ember and I have also come a long way as a front-end developer.

_To recap_: As a fun little project, two years ago I created an [Ember markdown editor component](https://github.com/jimmay5469/EmberMarkdownParser) and I started hosting it [on my website](/markdown-editor) which allows me to write posts in markdown for my website, which uses Jekyll. One of the cool things about this is that I can write markdown and see it rendered with my website styles realtime as I write it.

Here are some of my problems with my current implementation:
- No ember-cli.
- Everything is in a single file.
- No regularly used build system means I basically never update the [chjj/marked](https://github.com/chjj/marked) npm package.
- Very large, hardly re-usable markdown-editor component.
- Ember asset isn't hosted locally.
- Styles are messed up.
- Download Jekyll file has issues.
- The version for my website is hosted directly in my website's repo.

As I re-write my editor I plan to write a few posts about things I run into during development. As I write them I will come back and create links to them from this post.

Here are my plans of what I would like to attempt with the new implementation:
- Use ember-cli.
- Include [chjj/marked](https://github.com/chjj/marked) using the normal ember-cli build process so it can be easily updated.
- Host out of its own repository on GitHub and make it visible on my website via the `gh-pages` branch.
- Auto-deploy commits to the `master` branch using a CI tool to build and commit to the `gh-pages` branch.
- Use styles directly from my website so I don't have to include them in the new repository. If possible also do this for my website header and footer.
- Clean up code to use all of the new Ember concepts and the new practices that I use now:
  - Small, focused, easily re-usable components.
  - DDAU (data down, actions up).
  - Etc.
- Stop attempting to "upload/download" Jekyll files with the local file system.
- Work directly with the GitHub API to create and update posts in the main website repository.
- Make use of the Jekyll `drafts` folder to allow me to save a work in progress.
- Continue to use `localStorage` so that you don't lose changes when leaving the page or refreshing.
- While I work on the GitHub API features, make it easy to create Jekyll posts by displaying what the Jekyll file should look like.
{% endraw %}
