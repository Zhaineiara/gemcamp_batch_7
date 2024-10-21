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

* Create a validation for title and content in post
```ruby =
1. Post.create(title: '', content: '' ).valid? #false
2. Post.create(title: '', content: 'new content' ).valid? #false
3. Post.create(title: 'new title', content: '' ).valid? #false
4. Post.create(title: 'new title', content: 'new content' ).valid? #true
```

* Render validation to new.html.erb
```ruby =
1. Turn the post local variable into instance variable 
    # post to @post
2. add the validation logics to display the error.
    # <% if @post.errors.any? %>
    #   <ul>
    #     <% @post.errors.each  do | error | %>
    #       <li> <%= error.full_message %></li>
    #     <% end %>
    #   </ul>
    # <% end %>
```

* Added flash messages
```ruby = 
1. Add the logic in application.html.erb
    # <% if flash[:notice] %>
    #   <p class="notice"><%= notice %></p>
    # <% end %>
    # <% if flash[:alert] %>
    #   <p class="alert"><%= alert %></p>
    # <% end %>
2. Modify the create instance method in post controller
    # flash[:notice] = 'Post created successfully'
    # flash.now[:alert] = 'Post create failed'
```

* Added show
```ruby =
1. Setting up a show instance method to a post contoller
    # @post = Post.find(params[:id])
2. Setting up a show file to render record in show.html.erb
    # <h1>show post id: <%= @post.id %></h1>
    # <ul>
    #   <li><%= @post.title %></li>
    #   <li><%= @post.content %></li>
    # </ul>
3. How show instance method and rendering work?
    # Controller (show action): Fetches the post from the database using the id passed in the URL and assigns it to @post.
    # View (show.html.erb): Displays the post's attributes (like id, title, content) using the @post variable set by the controller.
```

* Added edit for post
```ruby =
1. Setting up an edit instance method to a post contoller
    # @post = Post.find(params[:id])
2. Setting up a show file to render record in show.html.erb
    # <h1>Edit post id: <%= @post.id %></h1>
    # <%= form_with model: @post do |form| %>
    #   <%= form.label :title %>
    #   <%= form.text_field :title %>
    #   <%= form.label :content %>
    #   <%= form.text_field :content %>
    #   <%= form.submit %>
    # <% end %>
3. How edit and update instance method and form work?
    # The edit action retrieves the post and renders the form with the post’s current data.
    # The update action processes the form submission, validates the data, and either updates the post or displays error messages if validation fails.
    # The view (edit.html.erb) displays the form, handles error messages, and submits the updated data to the server.
```

* Added delete for post
```ruby =
1. Setting up an destroy instance method to a post contoller
    # @post = Post.find(params[:id])
    # @post.destroy
    # flash[:notice] = 'Post destroyed successfully'
    # redirect_to posts_path
```

* Added button and link for create, read, edit and delete
```ruby =
1. Setting up the links in index.html.erb
    # <%= link_to 'New', new_post_path %>
    # <%= link_to 'Show', post_path(post) %>
    # <%= link_to 'Edit', edit_post_path(post) %>
    # <%= button_to 'Delete', post_path(post), method: :delete %>
```

* Added back to post
```ruby =
1. Setting up links to edit, new and show files
    # <%= link_to 'Back to Post', post_path %>
```

* Changes id to index as a counter
```ruby =
1. Change the each loop to each_with_index
    # <% @posts.each_with_index do |post, index| %>
```

* Refactoring (before_action :set_post and post_params)
```ruby =
1. Setting up set_post private method in finding id for show, edit, update, and destroy
    # def set_post
    #   @post = Post.find(params[:id])
    # end
2. Setting up before action where we use the set_post private instance method
    # before_action :set_post, only: [:show, :edit, :update, :destroy]
3. Setting up post_params
    # def post_params
    #   params.require(:post).permit(:title, :content)
    # end
    # This method is connected to create and update instance method.
    # This is responsible for handling strong parameters in Rails.
    # It ensures that only the permitted fields (title and content) are allowed to be submitted when creating or updating a post.
```

* Added partial form for new and edit post
```ruby =
1. Setting up the partial file then add the form code
2. Render the partial file into new and edit files
    # <%= render partial: 'form', locals: { post: @post } %>
3. How partial form works?
    # The detection of whether the form is for a new or edit action is automatically handled by the form_with helper in Rails, based on the state of the model object (post in this case).
    # The @post instance variable in the new or edit view isn't automatically available in the partial. So you use locals to explicitly pass the variable to the partial as a local variable (post).
    # Inside the partial _form.html.erb, you will refer to post (not @post) because it’s now a local variable.
```

* Active record association
```ruby =
1. Types of association: 
    # belongs_to, has_one, has_many, has_many :through, has_one :through and has_and_belongs_to_many
```

* Create comment model
```ruby =
1. Enter " rails generate model Comment content:string post:references"
    # check the files
2. Enter "rails db:migrate"
    # check the schema
```

* Query to connect comment to a post
```ruby = 
1. post = Post.first
2. post.comments
3. comment = Comment.new(content: 'comment of post 1', post_id: post.id)
4. comment.save
5. post.comments
6. post.reload
7. post.comments
```

* Create a comments controller
```ruby =
1. Enter "rails generate controller CommentsController --skip-routes --no-test-framework"
2. Added comment routes into post route
    # resources :posts do
    #   resources :comments
    # end
3. Create logic into comment controller
    # before_action :set_post
    # def index
    #   @comments = @post.comments
    # end
    # private
    # def set_post
    #   @post = Post.find params[:post_id]
    # end
```

* Create new comment using build method
```ruby =
1. Setting up logic for new comment in comment controller
2. Setting up new instance method for comment
    # @comment = @post.comments.build
3. Setting up create instance method for comment
    # @comment = @post.comments.build(comment_params)
    # if @comment.save
    #   flash[:notice] = 'Comment created successfully'
    #   redirect_to post_comments_path(@post)
    # else
    #   render :new
    # end
4. Setting up comment_params private instance method for comment 
    # params.require(:comment).permit(:content)
```

* Create form for add comment
```ruby =
1. Setting up form for add comment
2. Setting up validation for comments
3. Setting up link_to button for add comment
4. Exclude show in comment resources
```

* Create edit for comments
```ruby = 
1. Setting up logic for edit and update instance method
2. Setting up set_comment private instance method
3. Setting up before_action with set_comment for edit and update
4. Create a partial form for new and edit for comment
4. Render comment's partial form in new.html.erb and edit.html.erb
```