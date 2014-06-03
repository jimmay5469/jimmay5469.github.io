---
layout: post
title: "VIM: Why did I wait until now to start using macros?"
date: 2014-06-03 08:00:35
---
{% raw %}
I started using VIM full time almost a year ago.  I have gotten to a point where I feel like learning to use it has probably paid off.  I am probably a little bit faster than I was before I used VIM but overall the biggest difference is that it feels more fun to code with.

I had been putting off learning macros the whole time.  I had enough new key bindings to learn, why would I want to add more custom "key bindings" of my own to the mix of things I needed to remember?

Little did I know, one of the most fun features of VIM was macros.  They are super easy to record and to use, and it is fun trying to think in the mindset of doing something in a reusable way.

![vimMacroAnimation1](http://ljlauzau.smugmug.com/Hidden/My-Site-Images/i-Bfcgv96/0/O/vimMacro1.gif)

Just press `qj` to start recording, type a bunch of commands, and then press `q` to stop recording your macro.  Then press `20@j` to run your macro 20 times.  Of course, you can assign a macro to any letter, not just `j`, and if you only want to run the macro once just hit `@j`.

![vimMacroAnimation2](http://ljlauzau.smugmug.com/Hidden/My-Site-Images/i-96WBMwx/0/O/vimMacro2.gif)

You can do a lot of cool things with this, if you're not already using macros then you should check it out!

Answers to some questions I had about macros:

- By default they go away when you close VIM and you just write new ones when you open VIM up again.
- I've only been using them for short term purposes, so I really don't have more "key bindings" I have to remember.  I just write one, use it a few times, and then forget about it.
- If you've already assigned one to `j`, you can record over it simply by typing `qj` and recording another.
- You can chain them, just press `@j` while you are recording a macro assigned to `k`.  This is helpful if you had meant to navigate to the next line before stopping your recording in order to make a macro you can execute on the next 20 lines.  Simply press`qk@jjq`.  Now you can type `20@k` and the `j` macro will be executed on the next 20 lines!
{% endraw %}
