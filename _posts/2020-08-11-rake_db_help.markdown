---
layout: post
title:      "rake db:help"
date:       2020-08-11 01:17:10 -0400
permalink:  rake_db_help
---


The Sinatra Project, I love how fancy it makes it sound! As with the CLI project, this project is the hands on practice I absolutely need to fully understand concepts. As much as I live for filling those yellow hollow circles with solid green 'completed' dots on the lab list, the concepts do not sink in until I'm faced with the task of doing it myself from start to finish. For a few tid bits regarding rake, that I have no doubt were covered in labs and lecture, that did not sink in until it was 'show time', see below. 

Rake migrations! 

Absolutely essential to getting started, is creating your tables! Insert 'rake db:migrate' here! There are a few steps that need to come first. You need a general idea of the content you will be adding to your type, and the content type. So, let's get started. 

```
rake db:create_migration 'name_of_table_or_alteration'
```

this also can be entered as: 

```
rake db:create_migration NAME='name_of_table_or_alteration'
```

The convention to pay attention to here is the lower case snake_case. If you forget how to migrate, a very helpful 'rake:db aborted!' message appears. The error message is actually extremely informative and tells you exactly where you went wrong. 

```
rake db:create_migration 'create_table_volunteers'
```

``` 
class Volunteers < ActiveRecord::Migration[5.2]
  def change 
	  create_table :volunteers do |t|
		  t.string :name
			t.string :email
			t.boolean :training, default: false
			t.string :password_digest
			t.timestamps
		end
	end
end
```


To make modifications to your table, it would be extremely unlikely that you would get everything captured at the start. You will want to create a new migration for the alteration. 

```
def change
  add_column :name_of_table, :what_you_want_to_add, :type_of_input
	add_column :projects, :role, string
end 
```

Conversely, you can remove columns (I had to look this up more than once, I wanted to delete_column). You will create a new migration, using the rake db:create_migration 'name' then insert: 

```
def change
   remove_column :projects, :role, :string
end 
``` 

There are a few potential snags that you may hit. Depending on the type you want to add, you may need different syntax to add the column than if you had it in your initial creation. One example of this is 'timestamps.' When you first add them, you'd insert them in your create table iteration as seen above. I forgot to add timestamps into my Projects table. This can be done by... you got it- create a new migration. Then:

```
  def change
	  add_column :projects, :created_at, :datetime
	  add_column :projects, :updated_at, :datetime
	end
```

The nice packaging that 'timestamps' does is only available with the table creation. You can check out your schema of a table you created with 'timestamps' to see that once 'rake db:migrate' is done, it will indeed separate into the 'created_at' and 'updated_at' for you. 

Another tidbit that I found helpful with Rake, was to use the seeds.rb file. I learned the hard way, save yourself some time and add a ClassName.delete_all at the start of your seeds file. If you need to make edits to your current seeds, you have to change it then run 'rake db:seed.' Without that ClassName.delete_all, you will be creating more instances, on top of the ones you already created. I did not realize this until I ran 'Volunteer.all' in my pry to debug and saw I had multiple Kristen and Eliseo's listed! Here's a quick example: 

```
Volunteer.delete_all
Project.delete_all

kristen = Volunteer.create(name: 'Kristen', email: 'kristen@me.com', password: 'pass', training: 1)
eliseo = Volunteer.create(name: 'Eliseo', email: 'eliseo@me.com', password: 'pass', training: 1)

pride = Project.create(name: 'Pride 2020', role: 'interpreter', date: '7/15/20', assigned: 0)
townhall = Project.create(name: 'Town Hall', role: 'interpreter', date: '10/1/20', assigned: 1)
```

I found that creating two instances of each class to be helpful and plenty. This allowed me to make changes in one volunteer account (for example, creating a new project), then test authentications in my second volunteer's account (being able to view but not edit the project made by other volunteer). 

One last thing I wanted to point out is: 

```
t.boolean :training, default: false
```

This will set the training value default to false. You can see in my seeds file above, the volunteers are set to both having been trained '1' to set the default from false to true. The Project.first[:assigned] will return false, and Project.last[:assigned] will return false. You MUST enter an integer when you instantiate. If you want the default to remain, use 0. Otherwise, 1 works to change the boolean value to true. It's worth noting, I played around in my 'rake console' with a few numbers. When I used '0' , '3', '4' it returned false. '1' and '2' returned true. I didn't try past 4. The point being- 0 will keep the default value. 

As always, you have rake -T at the ready to help with commands. I found this a useful place to start, but it doesn't give the full syntax. If you've really hit a wall...you can delete the files and start again! In the development stages, this has been really helpful when I have raked myself into a corner. 


