# README

```
$ rbenv local 2.7.1
$ gem install rails
$ rails new test-app --api -T
$ cd test-app
```
```
# add to Gemfile
gem 'graphql', '<1.11'
gem 'graphql_devise'
```
```
$ bundle install
$ rails generate graphql:install
$ rails generate graphql_devise:install User --mount TestAppSchema
$ rails db:migrate
```
```
## app/controllers/graphql_controller.rb
# add this line after the commented protect_from_forgery
before_action -> { set_resource_by_token(:user) }

# change schema execute to use graphql_context helper
result = TestAppSchema.execute(query, variables: variables, context: graphql_context, operation_name: operation_name)
```
