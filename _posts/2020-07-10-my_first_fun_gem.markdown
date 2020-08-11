---
layout: post
title:      "My First FUN Gem!!"
date:       2020-07-10 20:15:10 -0400
permalink:  my_first_fun_gem
---


My first project, the CLI Project, is done! I had big dreams to make it the world's greatest gem and have settled somewhere in the arena of MVP (Minimal Viable Product). I've learned so many lessons on time management and look forward to not making the same mistakes going forward. It was maddening and thrilling to put all of the parts together into some kind of working harmony. On to the REALLY FUN part though!

I wanted to make the program....well, not ugly. Enter in: [rubygems](https://rubygems.org) to the rescue! During study group, a student mentioned "colorize." Color in an otherwise plain terminal window - JACKPOT! I did a quick google to find more information on "colorize" and other gems that may prove useful. I found two great ones to start off with! 

### gem colorize 

It can be found [here](https://rubygems.org/gems/colorize). 

The description: 

> Extends String class or add a ColorizedString with methods to set text color, background color and text effects.

It has an impressive (as of Stardate 98123.67) **48,254,660 downloads!! #goals 

### gem rainbow

It can be found [here](https://rubygems.org/gems/rainbow). 

The description: 

> Colrize printed text on ANSI terminals.

It has (as of Stardate 98123.69) **109,176,622 downloads! #MAJORgoals

### How to use these? 

As with any gem, these need to be downloaded. These are great "starter" gems because they are relatively similar in what they accomplish and how to implement them into your program.

```
gem install 'name of gem' 
```

In your config/environment file, Gemfile, or wherever you are setting up your requirements at runtime, you will need to

` require 'name of gem'`


### Let the FUN Begin!!

As I previously mentioned, these two gems are similar in how you implement them. 

```
    def show_color
        puts ""
        puts Rainbow("My favorite color").turquoise
        puts ""
        puts "Colorize has less color options than rainbow gem.".black.on_green
    end 
```

You can also tag on: .bold, .italic, .underline. Rainbow does have an "extension" of sorts that would allow for a similar .color tag on as colorize. I haven't tried it yet, but the option is there. Check out the [refinement](https://www.rubydoc.info/gems/rainbow/3.0.0) section in their documentation. 

To see the X11 color names available through Rainbow and some background, check out [wikipedia](https://en.wikipedia.org/wiki/X11_color_names). The rubygems documentation is also helpful. For a noob, it's somewhat overwhelming at first. I recommend doing a quick install and require setup , then start tagging your strings to have some fun. (And a mental break from code breaking :) ). 

Happy Coding!




