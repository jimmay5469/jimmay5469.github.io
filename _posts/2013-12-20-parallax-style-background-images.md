---
layout: post
title:  "Parallax style background images"
date:   2013-12-20 09:30:00
---
{% raw %}
If you're interested in how I created the parallax scrolling background image on my homepage or even on the top of this page keep reading on.  _Note:_ I like to change things, so if I no longer have this effect on my site, you can see the effect demonstrated at the bottom of this post.

Here is how you get the effect:

1. You will need 2 divs, one which will be responsible for displaying your background image, and the other is either a placeholder, or a content container, depending on how you want to use it.  These do not need to be the first elements in the page.  If you would like the effect to be lower down on the page, just put the elements there.

    ```html
    <div class="fixedBackground image dimensions"></div>
    <div class="dimensions">Either leave this empty or add content here.</div>
    ```

2. As you can see from above, we will also need to define a few CSS classes.  You will need a few properties, `fixedBackground`, which will make the first div act as a background of the second div, and be fixed (for the parallax effect).  You will also need to make the two divs have equal dimensions: `dimensions`.  For the purposes of this example, I also chose to separate out the actual image, `image`, so I could reuse some of the other styles.  You can see the style class definitions below:

    ```css
    .fixedBackground {
      background-attachment: fixed;
      background-size: cover;
      position: absolute;
      z-index: -1;
    }

    .dimensions {
      width: 100%;
      height: 200px;
    }

    .image {
      background-image: url(yourImage.jpg);
    }
    ```

See the full demonstration below:

<a class="jsbin-embed" href="http://jsbin.com/aZAyaCUj/3/embed?html,css,output&height=500px">JS Bin</a><script src="http://static.jsbin.com/js/embed.js"></script>
{% endraw %}
