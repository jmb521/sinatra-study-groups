# Sinatra 5. Sinatra Debugging & Difficult Concepts
**Title**: Sinatra Debugging & Difficult Concepts (Render vs. Redirect, Validations, Protecting Your Routes)
**Description**: Let’s learn how to debug in Sinatra, what the difference is between render and redirect, how to make sure a user is unique, and how to protect your routes from unwanted visitors.

## Table of Contents
1. Debugging in Sinatra
2. The Difference Between Render (`erb` ) and Redirect (`redirect`)
3. User Uniqueness Validation
4. Protecting Your Routes From Unwanted Visits

## Debugging in Sinatra
### **Raise params** to debug
- Why to use:
	- Allows you to see the params without having to use pry. You would use it to make sure that the params from your form are correct.
- How to use:
	- In controller: `raise params.inspect` or `puts params.inspect`
	- In view: `<%= params.inspect %>`

### Use **tux** to test out models
- Why to use:
	- Similar to an irb session except for it loads in the models and relationships from active record and allows us to access the database.
	- Is a good way to test methods created in a model (a slug method for example)
	- Good for quickly checking to make sure models and relationships are working correctly
	- Also useful when wanting to clear out any instances that were created or to add seed data
- How to use:
	- `tux` in Gemfile, `bundle install`, type `tux` in console

### Use **pry** in a way that allows them to pinpoint where bugs are occurring
- 	How to use:
	- `pry` in Gemfile, `bundle install`, add `require ‘pry'` to application controller
	- In controller: `binding.pry` 
	- In view: `<%= binding.pry %>`

### Read error messages and understand what they mean


## The Difference Between Render (`erb` ) and Redirect (`redirect`)
### What are the different parts of a route handler?
```ruby
get '/games/:id' do
	erb :'/games/show'
end
```
- Each route handler starts with an HTTP verb (get, post, put, delete or patch)
- The part that comes next is the URL or route (which can contain parameters `:id`)
- What’s inside of the `do ... end` block is the action or the behavior
- Each route needs to end in one of two things, `erb` or `redirect`

### Render (`erb`)
- The `erb` syntax allows you to render partials, it knows to look in our views folder to render a certain view
- You can pass information via `instance variables` to your views from the controller
- `erb` does NOT create a new `get` request instead it's a reference to a file that will load in the browser
- Example: If you want to tell your application to render a view called `index` (which is inside of your views directory), you would do it like this:
```ruby
get ‘/‘ do
	erb :index
end
````

### Redirect (`redirect`)
- A redirect will make a separate http request to the server, so for example when you type a url in your browser to fetch a new page, that’s a separate http request.
- Does not allow for `instance variables` to be passed along
- Example: When loading the url `/redirect-to-games` two get requests will be fired (check server) 1. the get request to `/redirect-to-games` and 2. the get request to `/games` (`/games` does not fire another get request because it renders via `erb`).
```ruby
get '/redirect-to-games' do
	redirect '/games'
end

get '/games' do
	erb :'games/index'
end
```

### When to use each one
*General rule of thumb: if it’s a successful post, patch, or delete do a redirect*
1. Don’t make a new HTTP request when not necessary
2. Likely any kind of successful `get` action will render something(`erb`) 
3. Any other successful HTTP POST, PATCH, or DELETE request will use `redirect` (to prevent resubmission of a form). Only use render for a form if errors occur and you want to pre-fill the form.
4. Remember that a “render” doesn't change the url of the page, make sure the urls make sense to the user when you use render.


*# Redirect:*
*# - Any successful post/patch/delete*
*# - Any unsuccessful get*
*# Render (erb):*
*# - Any successful get*
*# - Any unsuccessful post/patch/delete*


## User Uniqueness Validation
- make sure users can only sign up when they have a unique username or email (have one field about your user be unique)
```ruby
post '/users' do
	@user = User.find_by(email: params[:email])

	if @user
		redirect '/signin'
	else
		@user = User.create(email: params[:email], password: params[:password])
		if @user.save
			redirect '/user/#{@user.id}'
		else
			erb :signup
		end
	end
end
```


## Protecting Your Routes From Unwanted Visits
### You want two types of protection:
1. Hide edit/delete buttons from users that shouldn’t see them
```ruby
<% if @game.user == current_user %>
  <a href="/journal_entries/<%= @journal_entry.id %>/edit">Edit Entry</a>
  <br><br>
  <form class="" action="/games/<%= @game.id %>" method="post">
    <input type="hidden" name="_method" value="DELETE">
    <input type="submit" name="" value="Delete this Game">
  </form>
<% end %>
```

2. Make sure users can’t see urls they shouldn’t be able to see 

```ruby
get '/games/:id/edit' do
	if !logged_in?
		redirect '/'
	end

  @game = Game.find(params[:id])

  if @game.user == current_user
    erb :'/journal_entries/edit'
  else
    redirect "users/#{current_user.id}"
  end
end
```
