---
layout: post
title: Tips for installing Jekyll with So Simple and Jekyll Slideshow
description: "A fix for some difficulties I had setting up my So Simple theme installation"
modified: 2014-01-16
category: articles
share: true
tags: [jekyll, github, ruby, so simple theme]
 
---
[Jekyll](http://jekyllrb.com/) is my new favourite thing. I used it to build this site and most excitingly it integrates seamlessly with [GitHub](http://github.com). There are a number of shiny themes available for Jekyll. This site uses the [So Simple Theme](http://mademistakes.com/articles/so-simple-jekyll-theme/).

The processes for [installing Jekyll](http://jekyllrb.com/docs/installation/), [installing this theme](https://github.com/mmistakes/so-simple-theme/) and [using Jekyll with GitHub Pages](https://help.github.com/articles/using-jekyll-with-pages) are well documented and mostly simple, but I did run into a few weird errors when I added the [Jekyll Slideshow](https://github.com/matthewowen/jekyll-slideshow) gallery plugin to my installation - I think due to version conflicts between all the different bits of software.

I managed to debug the process on my home laptop, then tried running Jekyll on my work machine and ran into the same problem. Stupidly, I couldn't remember what the hell I'd done to fix it in the first place. For my own future reference and for your edification and delight, here is a list of commands that should install Jekyll, (Ruby and RubyGems), the So Simple theme and the Jekyll Slideshow plugin. These instructions should work for Ubuntu 12.04 and 13.10.

To install Jekyll you'll first need to install Ruby and RubyGems:

    sudo apt-get install ruby1.9.3
    sudo apt-get install gem

For good measure install the following Ruby extensions too:

    sudo apt-get install libreadline-ruby1.9 libruby1.9 libopenssl-ruby

Then use RubyGems to install Jekyll:

    sudo gem install jekyll

Once this is done, [fork](https://github.com/mmistakes/so-simple-theme/fork) and clone the So Simple theme repo and follow the instructions [here](https://github.com/mmistakes/so-simple-theme/) to customise and set up your new site.

Instructions for getting the Jekyll Slideshow plugin into your own repo are available [here](https://github.com/matthewowen/jekyll-slideshow). (Assuming you're already using plugins, you'll just need to copy across the <code>_plugins</code> and <code>jesl</code> folders into your projects, and call some additional CSS.)

Jekyll Slideshow uses ImageMagick as well as the RMagick and nokogiri gems however, and this is where things started getting hairy for me but theoretically it should work if you've got the latest versions of everything on your machine. 

ImageMagick is probably already installed if you're in Ubuntu. To check:
    convert -version

If it isn't installed:
    sudo apt-get install imagemagick

While you're at it, also install the following library:
    sudo apt-get install libmagickwand-dev 

Assuming you've already copied the necessary bits of Jekyll Slideshow into your repo, you'll need to install this plugins required gems:

    sudo gem install rmagick
    sudo gem install nokogiri

Theoretically this should work. If it doesn't, you might also want to try:

    sudo apt-get install libxslt-dev libxml2-dev

You should now be able to build and serve up your Jekyll site (with a functional theme and plugin) using the [standard Jekyll commands](http://jekyllrb.com/docs/usage/).

To integrate your new Jekyll repo with GitHub, you'll also need to install Bundler:

    sudo gem install bundler

After this, create a file in your repo called <code>Gemfile</code> and add the line <code>gem 'github-pages'</code>. Then run the command:
   
    bundle install.

I suspect there may be an overlap between Bundler and the other gems I've installed, but following this process was the only way I could get everything to work, error free. 
