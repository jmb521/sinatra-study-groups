# Sinatra 3. What is Sinatra, MVC, (Nested) Forms
**Title**: What is Sinatra, MVC, and (Nested) Forms
**Description**: We'll be talking about what Sinatra is (including Rack), the MVC (Model, View, Controller) pattern, and (nested) forms in Sinatra.

## Table of Contents
1. What is Sinatra? (Sinatra Basics, Shotgun, Routes)
2. MVC, The Basics You Need To Know
3. (Nested) Forms

## What is Sinatra? (Sinatra Basics, Shotgun, Routes)
- Sinatra is a framework for creating web applications
- Sinatra is a Domain Specific Language implemented in Ruby that’s used for writing web applications. Sinatra is Rack-based, which means it can fit into any Rack-based application stack, including Rails.
- Essentially, Sinatra is nothing more than some pre-written methods that we can include in our applications to turn them into Ruby web applications.
- Unlike Ruby on Rails, which is a Full Stack Web Development Framework that provides everything needed from front to back, Sinatra is designed to be lightweight and flexible. Sinatra is designed to provide you with the bare minimum requirements and abstractions for building simple and dynamic Ruby web applications.

### What is Rack?
- Rack is a web server interface and the underlying technology behind nearly all of the web frameworks in the Ruby world
- When you make a request Rack figures out how to respond and what information to respond with

### Shotgun
### Routes

## MVC, The Basics You Need To Know  (file/folder structure)
### What is MVC?
MVC stands for Model View Controller and is an architectural programming pattern, or a way to structure your application. It is a popular pattern (although by far not the only one) which essentially separates your application out into 3 main components, Models, Views, and Controllers.

### Why do we use it
- Separation of concerns

### How do we use it
#### Model
The Model represents the data of your application, it is essentially the main logic behind your application and should not depend on your controller or view.

#### View
Views are what the end user actually sees.

#### Controller
The controller is where everything comes together, it provides model data to your views and deals with information that comes back from the user (e.g. in the form of a button press).  - The controller pretty much does all the work.

### A Sinatra MVC Example
Game ratings

## (Nested) Forms
- Forms That Create Multiple Objects
- Thankfully, ERB provides a similar syntax. It handles that first level of nesting, so instead of having to domy_hash[“student”]={}we can just go straight into thestudenthash. ERB assumes that the name of your top-level hash is the first key, so the code to call the value associated with the nested”name”key would be student[“name”].
*  `Student Name: <input type=“text” name=“student[name]”>`
```ruby
params = {
  "game" => {
    "title" => "Asteroids",
    "description" => "Asteroids is a space-themed multidirectional shooter arcade game designed by Lyle Rains, Ed Logg, and Dominic Walsh and released in November 1979 by Atari, Inc. The player controls a single spaceship in an asteroid field which is periodically traversed by flying saucers.",
	  "image_url" => "https://www.gamasutra.com/db_area/images/feature/187385/image1.jpg",
	  "rating" => "5",
    "reviews" => [
      {
        "content" => "Awesome game"
      },
      {
        "content" => "Could play this for hours",
      }
    ]
  }
}
```
`Course Name: <input type="text" name="student[courses][][name]">`
Again, because a Student can have multiple courses in their schedule, we’ve nested each student’s courses within their primary hash. This creates a key calledcoursesinside of thestudenthash inparams. Thecourseskey will store an array of hashes, each containing course details.

ERB makes it even easier on us. Instead of manually indexing each entry, we can use an empty array ([]) in our form view, and ERB will automagically index the array for us, turningmy_hash[“student”][“courses”][0][“name”]intostudent[courses][][name]. The[]is some ERB magic that we just need to accept and use. It saves us time and simplifies our code!


### Review Form
```ruby
<h1>Create A New Game & Reviews</h1>

<form action="/reviews" method="post">
<h2>New Game</h2>
<div class="input-wrapper">
<label for="title">Title:</label>
<input type="text" name="game[title]" id="title">
</div>

<div class="input-wrapper">
<label for="description">Description:</label>
<textarea rows="4" cols="50" name="game[description]" id="description"></textarea>
</div>

<div class="input-wrapper">
<label for="image_url">Image URL:</label>
<input type="text" name="game[image_url]" id="image_url">
</div>

<div class="input-wrapper">
<label for="rating">Rating:</label>
<input type="number" name="game[rating]" id="rating" min="1" max="5">
</div>

<h2>Review 1</h2>
<div class="input-wrapper">
<label for="review-content">Content:</label>
<textarea rows="4" cols="50" name="game[reviews][][content]" id="review-content"></textarea>
</div>

<h2>Review 2</h2>
<div class="input-wrapper">
<label for="review-content">Content:</label>
<textarea rows="4" cols="50" name="game[reviews][][content]" id="review-content"></textarea>
</div>

<input type="submit" class="button">
</form>
```

### Review Controller post route
```ruby
post '/reviews' do
	game = Game.new(title: params[:game][:title], description: params[:game][:description], image_url: params[:game][:image_url], rating: params[:game][:rating])
	game.user = current_user

	params[:game][:reviews].each do |review_details|
		review = Review.new(review_details)
		review.game = game
		review.user = current_user

		review.save
	end

	game.save
	redirect "/games"
end
```
