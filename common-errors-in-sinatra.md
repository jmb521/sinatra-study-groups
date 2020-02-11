####Common Errors in Sinatra

#common errors in Sinatra

## not mounting the controller
    - comment out users controller in config.ru
    
## undefined method for nil class
    - the object wasn't found in the database (returned a nil value)
    - or the object wasn't fetched in the database. 
        - missing @model = Model.find(params[:id])
## redirecting to post on a patch request
    - use Rack::MethodOverride wasn't put in config.ru

## template missing error (no such file or directory)
    - you are referencing a template that doesn't exist. 
    - add the template to make the error go away
    - or you don't have the correct extension (.html)
## Sinatra doesn't know this ditty
 - could be missing a '/' before the route 
 - didn't properly interpolate when redirecting to a show page

## record not found
- Couldn't find User with 'id' = :id
didn't interpolate the id and used the :id variable instead

##
    