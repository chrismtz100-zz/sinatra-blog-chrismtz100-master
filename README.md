# Sinatra HW
 
## Prerequisites

1. Install Ruby via [RailsInstaller](http://railsinstaller.org/en) *(install latest version)*

2. ```
   gem install sinatra
   ```

3. ```
   gem install data_mapper
   ```

4. ```
   gem install dm-sqlite-adapter
   ```

## Instructions - Part 1 [50 points]

1. Clone this repository to your local harddrive

2. Run server: `ruby web.rb`

3. Go to `http://localhost:4567` and verify that you can see the posts

4. Add the template for the `new` route that has a form with the following properties:

   1. form action attribute is set to "/create"
   2. form has a textbox with an attribute name of "title"
   3. form has a textbox with an attribute name of "body"
   4. form has a submit button

5. Verify that you did this correctly by submitting the form. You should see a hash as output. (Make sure you restart the server to reload new changes)

6. Modify the `create` action to load information from the `params` variable and make a new `Post` object from it. Set the title and body of the `Post` object then call `save` on the post object. 

7. After calling `save` , you should render a success template

8. Deploy this onto Heroku (Your database on heroku will be blank, add some posts) (submit your link to Blackboard)


## Instructions - Part 2 [50 points]

1. Make this look nice with Bootstrap and get 50 points
   ​
## Grading

1. I will go to your Heroku link and try to add a post to your blog, if it doesn't work you get a 0. If it does work you get +50 points.
2. If it works, and you styled it with Bootstrap then you get +50 points.
3. There are no RSpec tests for this assignment.

## Deploying to Heroku

Once you have successfully deployed to Github it is time to deploy to Heroku.

Heroku does not allow you to use SQLite 3, which was the database file I gave you.

Heroku only likes real databases. Therefore, I have modified the example code in web.rb

Previously:

```ruby
DataMapper::setup(:default, "sqlite3://#{Dir.pwd}/blog.db") 

```

Now:

```ruby
# if on heroku, use Postgres database
# if not use sqlite3 database I gave you
if ENV['DATABASE_URL']
  DataMapper::setup(:default, ENV['DATABASE_URL'] || 'postgres://localhost/mydb')
else
  DataMapper::setup(:default, "sqlite3://#{Dir.pwd}/blog.db")
end
```

This allows us to use PostgreSQL (the database heroku allows us to use), instead of SQLite3, when running on Heroku. On our local machine, we will use the database file.

This means after deployment, your initial database will be blank.

Your correct `new` and `create` actions will allow you to populate the database.

### Deployment Instructions

1. Create a Heroku server: `heroku create`
2. Create a database for your server: `heroku addons:create heroku-postgresql:hobby-dev`
3. Push the code to Heroku: `git push heroku master`
4. I preconfigured the necessary files for this to work.
5. Verify all is working and submit your links (github and heroku) to me.
