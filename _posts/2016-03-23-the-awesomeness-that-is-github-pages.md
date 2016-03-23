---
layout: post
title: "The awesomeness that is GitHub Pages"
date: 2016-03-23 12:15:00 -0400
---
{% raw %}
I have tried many different over the years to host my personal website. Anything from WordPress to a custom built server rendered app. The one thing I have used that seems to have stuck: [GitHub Pages](https://pages.github.com/).

> ### Websites for you and your projects.
> Hosted directly from your [GitHub repository](https://github.com/). Just edit, push, and your changes are live.

This actually doesn't even get to the coolest parts:

- It's all FREE!
- You can use a custom domain name if you don't mind paying $10-15 a year to register it using your favorite registrar.
- You can actually host from multiple repositories.
- It is lightning fast, Google will love you.
- You can write pages and posts using Markdown.
- You have full control over every line of code that gets sent to your visitors. No more hacking WordPress templates to try and customize it.

You can follow the instructions over at the [GitHub Pages](https://pages.github.com/) website to get started and then browse around their docs there to really get going, or you can see a summary of what I do below.

## Creating static pages

One of the first things you will notice if you follow their instructions is that you don't have the comfort of your Rails server here. No big deal, you've written plain ol' html, css, and javascript before. Can't be too bad, right?

How long has it actually been since you've done this? You're gonna be copying over a navigation to every page, google analytics to every page, everything! Sounds tedious and like a bear to maintain. That's because it is!

That's where [Jekyll](http://jekyllrb.com/) comes in. Jekyll is no Phoenix or Rails server though. It is very specialized in creating _static_ webpages. Sure, you can still make an AJAX call to an external server and load in some data if you want, but you'll soon find there isn't normally a need.

Jekyll will take the tedious things out of creating a static webpage. It will allow you to create layouts, partial includes, pages and posts written in Markdown if you choose, and even process your SASS.

## Getting started

First we need to go to GitHub and create a repository named `[your username].github.io`. Don't initialize the repository because we will take care of that locally.

Next you're gonna need to install Jekyll:

```
$ gem install jekyll
```

Then lets create a local git repository we can push to the GitHub repository we just created.

```
$ jekyll new my-awesome-site
$ cd my-awesome-site
$ git init
$ git add .
$ git commit -m 'Initial Jekyll commit'
$ git remote add origin git@github.com:[your username]/[your username].github.io.git
$ git push -u origin master
```

At this point you should already be in business. Go visit `http://[your username].github.io` and you should see your new webpage.

When you push to `master` GitHub runs a build command which converts all of your code to static html files immediately. When a user visits your website they will not have to wait for a server to generate these files. The prebuilt files are served up just as if you had created html files manually. This makes your site lightning fast to browse and Google will love you for it.

If you want to run it locally for development, just do:

```
$ jekyll serve
```

Visit `http://localhost:4000` in your browser to see it running. Then dig around the code to learn the structure and make some changes. You can also use the [Jekyll docs](http://jekyllrb.com/docs/home/) as a reference. The Jekyll server will automatically rebuild the changes as you go so all you should need to do is refresh your browser and you will see an up-to-date `localhost:4000`. Don't worry about messing it up because you've made a commit you can always revert back to if needed.

If you are satisfied with the `http://[your username].github.io` address then you can skip the custom domain section and continue on to see how to create even more Jekyll websites.

## Custom Domains

First go get your domain if you don't already have it, and please don't go to GoDaddy for this. If you need a recommendation, use [iwantmyname](http://iwantmyname.com/), they are the most responsible registrar I've ever used. When you register a domain, your registrar will typically offer you a free DNS server so you'll need to set up a couple things there to tell it where you site lives.

Visit the DNS server configuration on your registrar and create 3 records:
1. An `A` record for your root domain. In my case that is `jimmylauzau.com` but usually you will just need to put `@` in the textbox. In the address textbox type `192.30.252.153`.
2. A second `A` record. This one should look exactly the same as the previous one but you will want to type `192.30.252.154` into the address textbox this time.
3. A `CNAME` record for the `www` subdomain. In the domain name textbox type `[your username].github.io`.

You are almost done. The next step is to go back into your repository and create a file named `CNAME` (with no extension) at the root of your repository. In the contents of the file just put `www.[your domain name].com`. This will set up the redirects to your `www` subdomain. If you want a reference, check out [my CNAME file](https://github.com/jimmay5469/jimmay5469.github.io/blob/master/CNAME). Don't forget to push that to GitHub.

Now you should be able to visit your site at `http://[your domain name].com`, `http://www.[your domain name].com`, or `http://[your username].github.io`. All three of these urls will resolve to `http://www.[your domain name].com`. If it isn't working quite yet then go drink a coffee or a beer and come back later today or tomorrow. Sometimes it takes a bit after setting up a brand new domain name or changing DNS records.

_Note:_ There are many other ways to set up your custom domain name DNS records and CNAME file if want a different subdomain or to change how the domain names resolve. I just explained what I do and what I recommend. Visit the GitHub [custom domain help page](https://help.github.com/articles/using-a-custom-domain-with-github-pages/) if you would like it set up differently.

## Hosting multiple repositories

On my website I have a couple little applications that I mess around with, one of them is a [markdown editor](/markdown-editor). Lately, I have been [updating my markdown editor](/blog/2016/03/21/updating-my-markdown-editor) and one of the motivations was to separate it's code out of my website's main repository. It is, after all, an application of its own.

Before, I just had a `/markdown-editor` directory in my main repository that it was contained in and now it has [it's own repository](https://github.com/jimmay5469/markdown-editor).

If you visit the new repository you will notice that in addition to a `master` branch, it has a `gh-pages` branch. When you _correctly_ create a `gh-pages` branch on one of your repositories, that `gh-pages` branch works like the `master` branch on your `[your username].github.io` repository. You can even use Jekyll if you desire. The only difference is that instead of being published to `http://[your username].github.io`, it is published to `http://[your username].github.io/[repository name]`.

So, I created a `markdown-editor` repository with a `gh-pages` branch and removed the `/markdown-editor` directory from my main repository, and now instead of serving that directory at [http://jimmylauzau.com/markdown-editor](/markdown-editor), it serves the `gh-pages` branch of the new repository!

You may have noticed I said _correctly_ create a `gh-pages` branch though. You actually have to do things slightly different than when creating a normal branch. The `gh-pages` branch must be an _orphaned_ branch, so that means you have to `git checkout --orphan gh-pages`, remove all files that you don't want hosted, and then start from there. That's it!

## What next?

That may be all you ever need, but if not then you can get a little more creative with it.

For example, in my markdown-editor, I use the `master` branch to host an ember-cli project and the `gh-pages` branch to serve a built version of that project. This project is built with ember-cli though, not Jekyll. I use [ember-cli-github-pages](https://github.com/poetic/ember-cli-github-pages) to simplify building the `master` branch and committing that build to my `gh-pages` branch (_Note:_ ember-cli-github-pages is advertised to be used with ember addon projects but will actually work with any ember project). I've even simplified that into an `npm run deploy` command which runs ember-cli-github-pages and pushes the updated `gh-pages` branch to GitHub. Next step I'm considering is to hook up a continuous integration tool like [Travis CI](https://travis-ci.org/) or [CircleCI](https://circleci.com/) to automatically run my `npm run deploy` command for me every time I commit push to `master`. Then I could basically forget I even have a `gh-pages` branch and focus on my code in `master`, taking for granted the fact that my `gh-pages` will stay up-to-date with my `master` branch.
{% endraw %}
