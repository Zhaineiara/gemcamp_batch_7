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

* Using resources instead of setting up manually
```ruby =
1. Enter the "resources :posts" on config/routes
```

* Fetch and render all data from posts table
```ruby =
1. In routes, change the root. Put "root 'posts#index'"
2. Add an instance method in post controller that will gather all the data.
    # In here, I use the 'Post.all' which I tried running in rails c
3. Render the data to posts/index.html.view (looping the data)
    # <%@posts.each do |post|%>
    # <%= post.title %>
    # <%= post.content %>
    # <%end%>
```

* Putting simple design to make it more organize
```ruby =
1. Get a design from bootstrap and transfer and ruby codes.
2. These are the following designs that I've used to design the table
    # 1. class="table" - to make a table
    # 2. class="table-striped" - to make the table stripe in rows
    # 3. class="table-primary" - to add color to the table, i always tried putting it in each rows that worked
    # 4. class="border" - to put a border
    # 5. class="border-secondary" - to add color to the border
    # 6. class="mx-auto" - for margin left and right
    # 7. class="my-5" - for margin top and bottom
    # 8. style="width: 1200px; - setting up the width

    # Not that required
    # 1. scope="col" - improves the semantics of the table and enhances accessibility by clearly identifying column headers.
```

* Modified table into responsive
```ruby =
1. Put the table into a div with a class (class="table-responsive) then add the margin (m-5)
2. Remove the my-5 (top and bottom margin)
3. Remove the style="width: 1200px"
4. Add w-100

. Additional bootstrap classes to remember:
    # 1. class="table-responsive" - to make the table adjustable in accordance to screen size
    # 2. class="w-100" - width sizing
```

* Create a record for post
```ruby =
1. Setting up a new instance of a post model 
    # @post = Post.new
    # handles displaying the form for creating a new post object.
    # This is server-side code that runs in the controller to prepare a new Post object for the view.
2. Setting up form for new post
    # form_with model: @post 
    # This is view code that generates a form tied to the @post object for the user to fill out.
3. How new instance method and form work?
    # When a user accesses the New Post page (triggering the new action), the controller creates a new Post instance and assigns it to @post.
    # The view then uses @post to generate a form where the user can input the title and content for the new post.
```

* Create a debugger
```ruby =
1. Put debugger in post controller (we use debug gem here)
    # def create
    #   debugger
    # end
    # This will generate data in terminal when you submit into the form
    # Parameters: {"authenticity_token"=>"[FILTERED]", "post"=>{"title"=>"sdsds", "content"=>"dsdsd"}, "commit"=>"Create Post"}
```

* Create a save for post that will save the instance
```ruby =
1. Enter this into create instance method.     
    # post = Post.new(params[:post])
    #   if post.save
    # redirect_to posts_path
2. Add the permit method into post
end
```
