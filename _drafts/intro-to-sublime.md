---
layout: post
title: Intro to Sublime
---

<!-- links -->
[sublime]: http://www.sublimetext.com/
[sublime_download]: http://www.sublimetext.com/2
[tutsplus_sublime_t1]: https://code.tutsplus.com/courses/perfect-workflow-in-sublime-text-2/lessons/welcome
[tutsplus_sublime_t2]: https://code.tutsplus.com/courses/perfect-workflow-in-sublime-text-2/lessons/services-and-opening-sublime-from-the-terminal
[sublime_commandline]: https://www.sublimetext.com/docs/2/osx_command_line.html

Today I'm going to introduce a very powerful and well-known tools, Sublime text. Sublime Text is a sophisticated text editor for code, markup and prose. [Click here][sublime] for its offical website.


First, [download][sublime_download] Sublime Text from the offical website. Here's a good [tutorial video][tutsplus_sublime_t1] I used to gain the basic overview of Sublime. It convers a lot of information and tips on how to use Sublime but here I'll just quickly demonstrate how to open Sublime from terminal.


After the installation, make a symlink to subl. Assuming you've placed Sublime Text 2 in the Applications folder, and that you have a ~/bin directory in your path, you can run:
{% highlight bash %}
ln -s "/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl" ~/bin/subl
{% endhighlight %}
Now, you can use subl command to open up a file or the whole driectory from the terminal. Example:
{% highlight bash %}
subl example.txt
{% endhighlight %}


Note: If you have the MacPorts version of Python installed, then starting Sublime Text 2 via the subl will not work correctly. As a workaround, start Sublime Text 2 first via Finder, and then interact with it using subl.


For detail information and explanation, you can check out this [tutorial video][tutsplus_sublime_t2] or this [sublime offical document][sublime_commandline].


## Resources ##
- [Sublime] [sublime]
- [Tuts+] [tutsplus_sublime_t1]
