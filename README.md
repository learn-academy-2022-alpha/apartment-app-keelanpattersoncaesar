
# README

  

## Hello. This is my README for my Apartment Finder App.

  

#### First, we create a Rails App:

```bash
$ rails new apartment-app -d postgresql -T
$ cd apartment-app
$ rails db:create
```

  

#### Then, we install a bunch of different resources:

  

* RSpec
- $ `bundle add rspec-rails`
- $ `rails generate rspec:install`
  
* React
- $ `bundle add webpacker`
- $ `bundle add react-rails`
- $ `rails webpacker:install`
- $ `rails webpacker:install:react`
- $ `yarn add @babel/preset-react`
- $ `yarn add @rails/activestorage`
- $ `yarn add @rails/ujs`
- $ `rails generate react:install`
- $ `rails generate react:component App`

  

* Devise
- $ `bundle add devise`
- $ `rails generate devise:install`
- $ `rails generate devise User`
- $ `rails db:migrate`

#### Changed default route for mailer
* config/environments/development.rb
- Added:
```ruby
config.action_mailer.default_url_options = { host:  'localhost', port:  3000 }
```

#### Changed request type for user logout
* config/initializers/devise.rb
- Replaced:
`config.sign_out_via = :delete`

- With:
`config.sign_out_via = :get`

#### Rails Routing

*  `rails g controller Home`
```ruby
create  app/controllers/home_controller.rb
invoke  erb
create  app/views/home
invoke  rspec
create  spec/requests/home_spec.rb
invoke  helper
create  app/helpers/home_helper.rb
invoke  rspec
create  spec/helpers/home_helper_spec.rb
```

* Added a file in `app/views/home` called `index.html.erb`
```ruby
<%= react_component  'App', {
logged_in:  user_signed_in?,
current_user:  current_user,
new_user_route:  new_user_registration_path,
sign_in_route:  new_user_session_path,
sign_out_route:  destroy_user_session_path
} %>
```

* In `app/views/layouts/application.html.erb`, changed `<%= javascript_importmap_tags %>` to `app/views/layouts/application.html.erb`

  

* In `config/routes.rb`, added routes:

```ruby
get  '*path', to:  'home#index', constraints:  ->(request){ request.format.html? }
root  'home#index'
```

  

#### React Routing
* Added React Router: $ `yarn add react-router-dom@5.3.0`
* In `app/javascript/components/App.js`, imported React Router
  

#### Adding Reactstrap
* $ `bundle add bootstrap`
* $ `mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss`
* $ `yarn add reactstrap`

  

#### app/assets/stylesheets/application.scss

```css
@import  'bootstrap';
```
#### Apartment Resource
* Generating a resource:
- $ `rails g resource Apartment street:string city:string state:string manager:string email:string price:string bedrooms:integer bathrooms:integer pets:string image:text user_id:integer`
- $ `rails db:migrate`

  

#### User and Apartment Associations
 Defining model-class relationship:

* app/models/apartment.rb
```ruby
class  Apartment < ApplicationRecord
belongs_to  :user
end
```
* app/models/user.rb
```ruby
class  User < ApplicationRecord
# Include default devise modules. Others available are:
# :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
devise  :database_authenticatable, :registerable,
:recoverable, :rememberable, :validatable
has_many  :apartments
end
```
#### Getting Started with React
* Created 3 folders in `app/javascript/components`
- ./assets
- ./components
- ./pages

* Foundation set in `app/javascript/components/App.js`
```javascript
import React, { Component } from 'react'

class App extends Component {
  render() {
    const {
      logged_in,
      current_user,
      new_user_route,
      sign_in_route,
      sign_out_route
    } = this.props
    console.log("logged_in:", logged_in)
    console.log("current_user:", current_user)
    console.log("new_user_route:", new_user_route)
    console.log("sign_in_route:", sign_in_route)
    console.log("sign_out_route:", sign_out_route)
    return(
      <>
        <h1>Apartment App</h1>
      </>
    )
  }
}

export default App
```