#Using Tux and ActiveRecord query methods

## simple query methods
### first, last and find
   {
       single_instance: [Model.first: , Model.last, Model.find: {
           takes in a primary key as an argument as a way to find the object in the database. You can pass in an array of primary keys to get multiple instances from the database, returned as an array. 
       }, Model.find_by], 
       relation: [Model.group, Model.where], 
       additional_details: grabs the first/last item in the database based on id #. Can also take an argument for the amount of instances you want it to return, ie. Model.first(3) will grab the first/last 3 instances from the db. 
   }
    
### tak
    {
        take: can take an argument of how many instances you want it to return. It will grab the first x number. 
    }

### find_by