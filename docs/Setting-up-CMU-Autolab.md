NOTE: This page exists for historic reference. We have abandoned the deployment of CMU Autolab in favor of group up solution that is being developed now.


1. Install `ruby 2.0.0` from `https://www.ruby-lang.org/en/downloads/`

2. Install `bundler` by `sudo gem install bundler`

3. Setup MySQL

4. `cd` into `autolab-src` and install the required gems by `bundle install`

5. Configure your database next. You need to fill the `username` and `password` fields on `config/database.yml.template` and rename it to `config/database.yml`. Change the database socket setting in this file. Search online to determine where your MySQL server's socket is if you don't already know.

6. Create and initialize the database tables: `bundle exec rake db:create` 
If you have no existing database:
`bundle exec rake db:reset`
If you already have a database whose data you want to preserve:
`bundle exec rake db:migrate`

7. (Optional) Populate dummy data for development purposes:
`rake autolab:populate`

8. (Optional) Setup Tango (TODO).

9. Create the autogradeConfig file by editing `config/autogradeConfig.rb.template` and renaming to `config/autogradeConfig.rb`

10. Start rails server: `bundle exec rails s -p 3000`

11. Go to :3000 to see if the application is running. You can use the `Developer Login` option with the email `"admin@foo.bar"`.