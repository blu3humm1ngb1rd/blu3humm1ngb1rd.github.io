---
layout: post
title:      "JavaScript Project : DISCGOLFR"
date:       2020-10-11 22:52:04 +0000
permalink:  javascript_project_discgolfr
---


It was nice to see some familiar functions when starting JS. Although you aren't exactly enumerating through JS objects, the foundation was nicely laid to lead into some more complex functions. Having a parallel to the CLI project when thinking of how the JS Project will execute was really helpful. 

### The SetUp
I had two basic classes: Course Class, Comment Class. 
```
class Course < Application Record
   has_many :comments
end 
```

```
class Comment < Application Record
   belongs_to  :course
end 
```


### Serializer 

I did decide to set up a Serializer. Aside from labs, I had not tried one out yet, so why not?! I used the Active_Model_Serializer, and used this resource to set it up: https://medium.com/@wajeeh.ahsan/rails-serialization-active-model-serializer-7af16ee9a466 . The reason why I used this was because I wanted to see it in action, IRL, and I wanted my ActiveModel relationships to be available in JSON at my disposal. I set up the relationship within the serializer classes as my courses 'has_many' comments. This implementation was immediately available by viewing your API. 

Prior to adding in the serializer relationship, I checked out my courses path. Here is a preview of one of the courses:
```
{
    "id": 101,
    "name": "Brengle Terrace",
    "city": "Vista",
    "state": "CA"
  },
	```

Now, adding the line of `has_many :comments` in the class CourseSerializer, we now see: 

```

  {
    "id": 101,
    "name": "Brengle Terrace",
    "city": "Vista",
    "state": "CA",
    "comments": [
      {
        "course_id": 101,
        "content": "Lots of hills!"
      },
      {
        "course_id": 101,
        "content": "Intermediate - Advanced"
      }
    ]
  },
	```
	
This is infinitely helpful to see the object that you will be passing to your frontend to render. The attributes that are visible in the API are manually set. Within the CourseSerializer class, I added: `attributes :id, :name, :city, :state`. The courses table also had timestamps that I could have rendered as attributes, however these weren't needed. 

### JavaScripting ... 

The hardest part was decided which path to take as far as setting up the application. As a noob, I set it up one way and then struggled to stick to that path. 

```
JS-BACKEND
   src
	   appContainer.js
		 comment.js
		 course.js
		 index.js
	 index.html
```

If I could go back in time, I would not have used an AppContainer class. Initially, it seemed like a good idea but I think a simpler approach would be to use my index.js as the 'controller' of sorts, and then utilize my two classes: comment.js and course.js more efficiently. It is admittedly convoluted right now as far as flow. I had originally set up arrays in my AppContainer constructor, that halfway through the build I decided I did not want to use. I am using the course array from the AppContainer, but decided not to use the comment container. I see these projects build as a time to experiement and play with different ideas, so I felt free to try different things. However, I would use a more singular, concise design in the future. 



