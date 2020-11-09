---
layout: post
title:      "React-Redux Application"
date:       2020-11-09 02:04:25 +0000
permalink:  react-redux_application
---


As this is the last project, I decided to go heavier on the backend. I set up 6 models to accomodate the basics I needed, and room to grow  as I get more comfortable using React-Redux. They are as follows: 

1. User
2. Location
3. Courses
4. Comments
5. Bucket List
6. Activities (joins for BucketList/Courses)

For starters, one of the biggest lessons I learned was stick to single word names for tables. Using 'Bucket List' has been a nightmare. The comments table is not currently in use. The models I needed to get working initially were: User, Courses, Location, Bucket List and Activities. Activities in the join table from Courses to Bucket List. I intentionally named this something generic instead of CoursesBucketList or another standard joins table conventional name, because I may want to expand and pull more things in. I am still brainstorming the relationships, for now these work for what I need. 

### Set Up

Figuring out the backend took a decent amount of time. I haven't set up relationships in a while, so getting the associations working took a while. Rails Console, `rails c` was instrumental in testing out the relationships while making them. For example, User `has_many :bucket_lists` , so if I set up a user

```
bj = User.create(name: "BJ", username: "bjdev", password: "password")
bj.bucket_lists
=> <ActiveRecord::Associations::CollectionProxy []>
```

If I am able to return an empty array from my user's associated bucket_list, that means the association was set up properly. 

Users do not have a relationship with Location, so I would expect to get an error if trying out: 

```
  User.first
  bj = _ 
  bj.locations
  => NoMethodError (undefined method `locations' for #<User:0x00007fb4df98eb08>)
```

*Quick note*: if you forget to first set your variable before `User.first` , you can catch it in the next line by setting your variable = to `_` , as shown above. 

Ideally, use a seeds file to get your inital data set up. I typically use the console to test everything out and then just stick with that for "seed data". However, this can be cumbersome to upkeep when you are working on CRUD actions. For example, I initially had 3 courses set up from my backed. When I was able to delete them from the front end, I quickly ran out of courses from testing my `destroy`. Seeds would have been helpful here, a quick `db:seed` and I would have information again to use. 

#### Serializer 

For this project, I tried out the [`fast_jsonapi`](http://https://github.com/Netflix/fast_jsonapi). This was fairly easy to set up, with a quick `rails g serializer modelName` . You are able to set your relationships in the serializer. The documentation goes through custom setups. Mine were fairly straightforward, I didnt' dive into that. Once you have set up your serializer, you need to add into your controller actions that will be rendering the json to your front end. Here is an example from my Course Controller for the index action: 
 ```
   courses = Course.all
   courses_json = CourseSerializer.new(courses).serialized_json 
   render json: courses_json
```

If you are looking at that and wondering if it could be refactored to two lines, you're on point. The extra step was for my sake to see the process. 

At this point, it was a matter of fine-tuning my information being rendered and serialized. I utilized: `http://localhost:3000/rails/info/routes` to accomplish this. I have this bookmarked for quick viewing. Once the routes checked out, I was able to view my api information, aka see how much damage repair was in my near future for how I set up the information. 

### Frontend React/Redux

This was a very different experience from JavaScript in that, you don't necessarily have immediate access to your data. There is a LOT of set up that needs to be accomplished before you are able to `console.log` , use devTools, or throw a `debugger`. 

What was on the more simple side of rendering information, quickly expanded into multiple folders and files. I utilized the file structure:

```
public
  index.html
src
  actions
	reducers
	components
index.js
```

This has been helpful to quickly identify between reducers and actions and components, which have the same or similar names. The import process becomes much easier.

The project would not have been possible without the `react-redux` middleware function:` connect`. With connect, I have access to my store, which ultimately should be responsible for the applicaiton's data. From what I've learned so far, it is the main advantage to incorporating `redux`.  

I look forward to continuing to expand on this application and jazzing it up with CSS! 


