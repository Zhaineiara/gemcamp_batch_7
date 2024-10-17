* Hello World
```ruby =
1. Added "root 'welcome#index'" on config/routes.rb
2. Enter "rails generate controller WelcomeController index --skip-routes --no-test-framework" on /usr/src/app which is the docker container
    # This will generate welcome_controller.rb and index.html.erb
3. Enter the "Hello world on index.html.erb"
```

* Active Record Basics
```ruby =
1. Enter "rails generate migration create_posts" on docker container
    # This will generate a migration file that is use for database schema
2. Check the migration file and identify the column datatype and title
3. Enter "rails db:migrate"
    # This will run all the migration files in db/migrate which will reflect in the db/schema
```

* Scaffold add and remove
```ruby = 
1. Enter "rails generate scaffold Post title:string content:text" on docker container
    # It generates the following: db/migrate/20241017072138_create_posts.rb, app/models/post.rb,  app/controllers/posts_controller.rb,
    # app/views/posts/index.html.erb, app/views/posts/edit.html.erb, app/views/posts/show.html.erb, app/views/posts/new.html.erb, app/views/posts/_form.html.erb, app/views/posts/_post.html.erb
    # app/helpers/posts_helper.rb,  app/views/posts/index.json.jbuilder, app/views/posts/show.json.jbuilder, app/views/posts/_post.json.jbuilder
2. Enter "rails destroy scaffold Post"
```

* Added model and controller for post
```ruby =
1. Enter "rails generate model Post"
2. Enter "rails generate controller Posts"
3. Identify the column datatype and title
4. Enter "rails db:migrate"
5. Enter "rails db:reset"
```

* Creates record for posts table
```ruby =
1. Post.create(title: 'My first post', content: 'My first post blog')
2. post = Post.new                      
   post.title = 'My second post'           
   post.content = 'My second post blog'
   post.save 
3. Post.create(title: 'My third post', content: 'My third post blog')
   Post.create(title: 'My fourth post', content: 'My fourth post blog')
   Post.create(title: 'My fifth post', content: 'My fifth post blog')
   Post.create(title: 'My sixth post', content: 'My sixth post blog')
```

* Reading records from the database (all records)
```ruby =
1. Post.all
```

* Reading records from the database (first and last records)
```ruby =
1. Post.first
2. Post.last
```

* Reading records from the database (find by id)
```ruby =
1. Post.find(1)
2. Post.find(6)
```

* Reading records from the database (find by column value)
```ruby =
1. Post.find_by(title: 'my first post')
2. Post.find_by(title: 'My sixth post')
```

* Reading records from the database (find by column value)
```ruby =
1. Post.where(title: 'my first post')
2. Post.where(title: 'My sixth post')
```

* Reading records from the database with orders (asc, desc)
```ruby =
1. Post.order(created_at: :asc)
2. Post.order(created_at: :desc)
```

* Updating record (.update, save, where)
```ruby =
1. post.update(content: 'The first post is updated') 
2. post = Post.second
   post.content = 'The second post is updated'
   post.save
3. Post.where(id: [3, 4]).update(content: 'Update multiple contents')
4. Post.where(id: [3, 4]).update_all(content: 'Update multiple contents with update_all')
```

* Deleting record (.update, save, where)
```ruby =
1. Post.last.destroy
2. Post.where(id: 3).destroy
3. posts = Post.where(id: [3, 4])
   posts.destroy_all
```