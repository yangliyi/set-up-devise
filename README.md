# README


[Devise](https://github.com/plataformatec/devise) is the most popular authentication solution in Rails community.


This is a note to help you set up devise in your project.

* The code comes after dollar sign is a command to type and execute in your terminal.
* Other code inside a block should be put into some files in your Rails project.

## Step1: Add devise to your Gemfile

```
# In your Gemfile
...
gem 'devise'
...
```

```$ bundle install```

## Step2: Generate configuration files

```$ rails g devise:install```

## Step3: Set up default URL options for mailer

```
# For example, in your config/environments/development.rb
...
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
...

```

## Step4: Ensure you set up root_url

```
# In config/routes.rb
...
root to: "one_existing_controller#one_of_the_actions_inside"
...

```

For example:

```$ rails g controller welcome```

```
# In app/controllers/welcome_controller.rb
...
class WelcomeController < ApplicationController
  def index
  end
end
...

```

```
# In app/views/welcome/index.html.erb
...
<h1>Home Page!</h1>
...

```

```
# In config/routes.rb
...
root to: "welcome#index"
...

```

## Step5: Ensure it could show flash messages

```
# In app/views/layouts/application.html.erb
...
# Check if there's something like:
<body>
  ...
  <p class="notice"><%= notice %></p>
  <p class="alert"><%= alert %></p>

  <%= yield %>
  ...
</body>
...

```

## Step6: Generate User model and migration

```$ rails g devise user``` Generate **User** model and migration.

```$ rails generate devise:views``` (Optional) Generate all devise view templates in **app/views/devise** so you can customize them later.

```$ rails db:migrate``` Create **users** table

## Step7: Add links based on the route setting:

```
# In app/views/layouts/application.html.erb
<body>
  <!-- current_user is a method defined by devise to help us check if a user has signed in or not. -->
  <!-- Add below links: -->
  <% if current_user %>
    <%= link_to('Log Out', destroy_user_session_path, :method => :delete) %> |
    <%= link_to('Change Password', edit_user_registration_path) %>
  <% else %>
    <%= link_to('Sign Up', new_user_registration_path) %> |
    <%= link_to('Sign In', new_user_session_path) %>
  <% end %>

  <p class="notice"><%= notice %></p>
  <p class="alert"><%= alert %></p>
  <%= yield %>
</body>
```


## Step8: Set up a controller with user authentication by using devise helper:

For example:

```
class WelcomeController < ApplicationController
  before_action :authenticate_user!
  # "authenticate_#{model_name}!" is a method defined by devise so we can use in controllers of our projects.

  # We use before_action to check for some actions to see if users have signed in or not.

  # If users haven't signed in yet, they would be redirected to sign in page.

  def index
  end
end

```



