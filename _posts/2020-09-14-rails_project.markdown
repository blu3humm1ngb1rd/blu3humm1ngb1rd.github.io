---
layout: post
title:      "Rails Project "
date:       2020-09-14 04:24:03 +0000
permalink:  rails_project
---


My biggest takeaway from this project was realizing that I did not have clearly defined goals going in. I had originally planned to build off of my Sinatra project. I hit a big snag at the beginning of a Holiday weekend. I figured that help would be less available, `<input type="emotion" name="FREAKOUT">` ... so I decided to start a new project, new ideas, and new associations. 

True to my 80's kid nature, I still feel a strong need to put pen to paper. I started drawing and mapping out what I thought I needed. I mapped out associations and started making lists of what I things I needed to accomplish. I <em>know</em> that there are so many amazing planning resources, and learn.co provides one as well in the curriculum. I have utilized various online formats, such as draw.io. 

My goal going forward is to integrate paper drafts with digital drafts more efficiently. Especially with Covid-19, it seems like an online presence and digital information is more important than ever when trying to find and be seen by potential employers.

#### HTTP is StateLESS....no biggie? BIGGIE!

During my Sinatra project review, a main theme was reviewing the concept of HTTP being a stateLESS protocol. My, <em>very</em> patient accessor explained a few different ways why this was an important concept to know, understand and practice. In practice, this means when setting up controller actions, it is important to remember that you have to reinstantiate an object upon a redirect. 

```
def destroy
  @room.destroy
  redirect_to rooms_path
end	
```

##### Quick Note about paths - 
I literally just learned this 'trick' today. Check out: [http://localhost:3000/rails/info/routes](http://http://localhost:3000/rails/info/routes) while your server is running for a complete list of your current routes. There are other ways to get the routes list, `rails routes` in your command line, or localhost:3000/lakjdsf (obviously not a route) and doing the mental acrobatics of mapping them out using your routes.rb file. I've found that adding localhost:3000 and localhost:3000/rails/info/routes into my bookmarks toolbar has been a time saver. 

##### Back to the main program... 

So the rooms_path goes to my Rooms controller, Index action, which looks like this: 

```
def index
  @rooms = current_user.rooms
end
```

I am instantiating @rooms for the index page to have access to this information. The very cool thing about Rails, is that if you are not instantiating anything for your controller action, then you don't even have to list it at all, given that you are following RESTful routing. 

##### slight caveat ... 

If you use a before_action, then you will need to have the controller action. For example: 

`  before_action :set_room, only: %i[show edit update destroy]` 

Although I am not using anything else to pass into my Show.html.erb, this information of #set_room will not be passed without listing out

` def show; end` 

That simple line will do the trick. I was half expecting Rails to know without me having to type out 11 extra characters. pfft. Given the powerful methods and possibilities already available, this seemed reasonable. 


#### PARTIALly Addicting!

I did <em>not</em> expect to love partials so much! When this topic first came up in lecture and the labs, I was feeling firmly against it. Sometime after the fourth video tutorial and a few lectures, I started to feel more confident about using them. I officially fell in love when I was able to boil down my Tasks Index Page to: 

```
Tasks Index Page

<h4> My Tasks: </h4>
<%= render 'tasks' %>


<h4> Signed up to Help: </h4>

<%= render 'help_signup' %>
```

Insert *gasp* here! How great is that! Partials have been useful to, not necessarily abstract away anything, but to declutter my code. It also is good practice in following naming conventions; you want to use names that relate to what they are being used for. It seems obvious, however it can't be said enough: keep it simple and relevant.  


	
