# README

## How to make this demo
Create a new app
```
$ rbenv local 2.7.1
$ gem install rails
$ rails new test-app --api -T
$ cd test-app
```
Add the necessary gems to Gemfile

Capping Graphql to 1.11 because newer version is not compatible with graphql_devise 0.12.1
```
# add to Gemfile
gem 'graphql', '<1.11'
gem 'graphql_devise'
```
Install and run generators
```
$ bundle install
$ rails generate graphql:install
$ rails generate graphql_devise:install User --mount TestAppSchema
$ rails db:migrate
```
Implement devise in controller
```
## app/controllers/graphql_controller.rb
# add this line after the commented protect_from_forgery
before_action -> { set_resource_by_token(:user) }

# change schema execute to use graphql_context helper
result = TestAppSchema.execute(query, variables: variables, context: graphql_context, operation_name: operation_name)
```
